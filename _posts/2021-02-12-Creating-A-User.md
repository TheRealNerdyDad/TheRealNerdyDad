---
layout: post
title:  "Creating A User"
date:   2021-02-12 09:00:00 -0600
categories: PowerShell
---

User Management is important in any organization, especially when they have ActiveDirectory deployed in their environment. Any way of automation can be very helpful in saving time, reducing errors, and making sure that all of the tasks that are involved with creating a user are completed.

I understand that this whole script will not suite everybody, but I know that there are pieces in here that are going to be more valuable to some than others. If there is anything in here that would provide a value to you, by all means, you are more than welcome to use it. The whole script is commented and are sectioned off into modules that relates to a flowchart for this script. Maybe one day I can post the flowchart as well. This one is designed to interact with an Exchange server that is on-premises (in house, not O365/Exchange Online). I do have another script similar to this one but is written for O365/Exchange Online instead of Exchange On-Premises.

```Powershell
#Imports the AD
Import-Module activedirectory

#Sets Variables
$fn #First Name
$ln #Last Name
$title
$dep #Department
$loc #Location
$man #Manager
$un #Username
$officePhone
$streetAdd
$city
$ZIP
$fi #First Name Initial, will be used to figure out Username

#Getting information
$fn = Read-host "First Name?"
$ln = Read-Host "Last Name?" #Special characters have not been tested. I would suggest not using special characters in last names in AD. In theory, its probably okay, but I have not yet tested it.
$title = Read-Host "Title?"
$dep = Read-Host "Department?"
$man = Read-Host "Manager (Username)?"
$loc = Read-Host "Loc1 or Loc2?" #If you need to add locations, make sure that you also edit modules 1.06 - 1.08 to conform to the new logic.

#Finding out the Username
$fi = $fn.Substring(0,1)
$un = -join ($ln, $fi)

#Sets Location information (Module 1.06)
if ($loc -eq "Loc1") { #If the user is in Loc1 (Module 1.07)
    $officePhone = "(999) 999-9999";
    $streetAdd = "123 Anywhere Drive";
    $city = "YourTown";
    $ZIP = "12345";
}
Else { #If the user is in Loc2 (Module 1.08)
    $officePhone = "(987) 654-3210";
    $streetAdd = "987 Nothere Blvd";
    $city = "Somewhere Else";
    $ZIP = "98765";
}

#Sets Password
$passwd = (Read-Host -AsSecureString "Account Password")
$password = ConvertFrom-SecureString -SecureString $passwd

$userParams = @{
    'Name' = $un;
    'Enabled' = $true;
    'AccountPassword' = $passwd;
    'UserPrincipalName' = -join ($un, "@.com");
    'SamAccountName' = $un;
    'ChangePasswordAtLogon' = $false;
    'GivenName' = $fn;
    'Surname' = $ln;
    'DisplayName' = -join ($fn," ",$ln);
    'Description' = $title;
    'OfficePhone' = $officePhone;
    'StreetAddress' = $streetAdd;
    'City' = $city;
    'State' = "Texas";
    'PostalCode' = $ZIP;
    'Title' = $title;
    'Department' = $dep;
    'Company' = '';
    'Manager' = $man;
}

#Creates the user in AD
New-ADUser @userParams

#Wait for the account to be created before doing anything else
Start-Sleep -Seconds 10

#Makes the user's network drive, scan folder, and sets the permissions to their folders and files
if ($loc -eq "Loc1") { #If the user is in Loc1
    New-Item -Name $un -ItemType directory -Path "\\server\folder" #Creates users network drive
    New-Item -Name scans -ItemType directory -Path "\\server\folder\$un" #Creates users scan folder
}
Else { #If the user is in Loc2
    New-Item -Name $un -ItemType directory -Path "\\server\folder" #Creates users network drive
    New-Item -Name scans -ItemType directory -Path "\\server\folder\$un" #Creates users scan folder
}

#Adds the user to the correct Security Group for permissions and other network drives
if ($dep -eq "Accounting"){
    Add-ADGroupMember -Identity 'Accounting' -Members $un
} #Adds the user to the Accounting Group
Elseif ($dep -eq "Customer Service") {
    Add-ADGroupMember -Identity 'Customer Service' -Members $un
} #Adds the user to the Customer Service Group
Elseif ($dep -eq "HR") {
    Add-ADGroupMember -Identity 'Human Resources' -Members $un
} #Adds the user to the Human Resources Group
Elseif ($dep -eq "Human Resources") {
    Add-ADGroupMember -Identity 'Human Resources' -Members $un
} #Adds the user to the Human Resources Group
Elseif ($dep -eq "IT") {
    Add-ADGroupMember -Identity 'Domain Admins' -Members $un
} #Adds the user to the Domain Admins Group for IT
Elseif ($dep -eq "Maintenance") {
    Add-ADGroupMember -Identity 'MaintGroup' -Members $un
} #Adds the user to the Maintenance Group
Elseif ($dep -eq "Shipping") {
    Add-ADGroupMember -Identity 'SHIP' -Members $un
} #Adds the user to the Shipping Group
Else {
    Add-ADGroupMember -Identity 'Domain Users' -Members $un
} #Dumps the user to the Domain Users Group

#Connects to the Exchange box, creates the users email account, then disconnects from the Exchange box
$mail = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://exchange/powershell -name -Authentication Kerberos -Credential $cred
Import-PSSession $mail -WarningAction SilentlyContinue | Out-Null
Enable-Mailbox -Identity $un -Alias $un -DisplayName (-join($fn,$ln)) #Creates the users mailbox
Remove-PSSession -Session $mail #Disconnects from the Exchange box

$manfn = Get-ADUser $man -Properties GivenName | select GivenName #Gets the managers first name
$manln = Get-ADUser $man -Properties SurName | select SurName #Gets the managers last name

#Create a report of the User's information
$report = "Hello $fn $ln,

From the IT Department, welcome to <YourCompanyNameHere>. We
are here to help you connect to the resources that you need for
your job. If you need assistance with technology, please feel
free to contact us at either the help page, which is set as your
home page in Internet Explorer, email us at
helpdesk@<YourDomainHere>.com, or call us at extension ####.

Below you will find your information so that you can login to
the network and get started:

Your username is \$un
Your password is
Your email address is $fn$ln@<YourDomainHere>.com
Your phone number is $officePhone Ext. ####

It is suggested that you change your password to something that
you can remember but difficult enough that somebody else cannot
figure out. The requirement is only 6 characters, but we do
advise on making it longer, throw some numbers and special
characters in there as well to make it stronger. Best advice
would be to use a pass-PHRASE instead of a pass-WORD.

Your computer should already be setup with your email loaded and
your network drives. At <YourCompanyHere>, we use Microsoft
Outlook as the email client. Depending on what department you
are in will depend on what drives you have available.
Generally, everybody will have an <Letter>: drive and a <Letter>: drive. The
<Letter>: drive is your network folder. Place in there the documents
that you feel you cannot do your job without. In the <Letter>: drive
will be a scan folder. When you go to the Xerox to scan in
documents, then you will find them in your scan folder. The <Letter>:
drive is a company-wide shared folder. As for your department
drives, it would be best to talk with $($manfn.name),
your supervisor/manager about the nature and uses of these drives.

The use of the equipment and resources provided are a privilege
to you for use and should not be taken advantage of. There are
measures set in place that allows us to manage the network. Do
not assume that there is any personal privacy on this network.
The only privacy that you can assume is for the nature of your
work. All information (including emails, documents,
spreadsheets, pictures, etc.) contained on the equipment
provided and on the network is the sole property of <YourCompanyHere>.

If you have problems with your equipment or network resources,
please feel free to ask. We do not mind helping, but we cannot
help if we do not know, so please ask!

Sincerely,

Your IT Department"

if ($loc -eq "Loc1") {
    Write-Output $report | Out-Printer \\server\Printer
}
Else {
    Write-Output $report | Out-Printer \\server\Printer
}
```