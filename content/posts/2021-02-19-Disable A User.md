---
title: Disable A User
date: 2021-02-12T17:00:00-05:00
categories: [general,it,activedirectory,powershell]
tags: [general,it,activedirectory,powershell,user-administration,security]
---
# Disable A User
It’s hard to create a user, but its REALLY easy to disable a user’s account. That is exactly what this script does. Well…it doesn’t “disable” the user’s account, but it does make it impossible for the user to login to the network without help from IT. Basically, this script will ask 4 things from you. It will ask you who you are disabling, who their manager is, who you are, and a password to change the user’s account to. It will then create an email to be sent to you and HR, informing HR of who has changed the user’s password, and when. That way they can be assured that all technical resources owned by the company are kept safe as the user is leaving the network, if not the company.

This script assumes a few things:

1. You at least have Exchange Admin rights in order to connect and send the email.
2. You have Domain Admin rights in order to change the user’s password.
3. You have 2 distribution groups (HR & IT) with the necessary personnel in each group.
4. Your Exchange server is on premises.

As usual, everything is commented and sterilized for your usage.
```powershell
Import-Module activedirectory

$un = Read-Host "Who are we disabling today? (Login Credentials)" #username
$man = Read-Host "Who are we forwarding mail to? (Login Credentials)" #manager's username
$auth = Read-Host "Who are you? (Login Credentials)"

#Resets the old user's password
Set-ADAccountPassword -Identity $un -Reset -NewPassword (Read-Host -AsSecureString "Account Password")

#Connects to the Exchange box, forwards the users email account to their supervisor/manager, then disconnects from the Exchange box
$mail = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://Exchange/powershell -name Exchange -Authentication Kerberos -Credential $cred
Import-PSSession $mail -WarningAction SilentlyContinue | Out-Null
Set-Mailbox $un -ForwardingAddress $man -RemovePicture #Sets the forwarding address to the manager and removes their picture
Remove-PSSession -Session $mail #Disconnects from the Exchange box

$dt = get-date #Gets Date & Time
$authn = Get-ADUser $auth -Properties DisplayName | select -ExpandProperty DisplayName #Gets the administrators name
$unn = Get-ADUser $un -Properties DisplayName | select -ExpandProperty DisplayName #Gets the disabled users name
$mann = Get-ADUser $man -Properties DisplayName | select -ExpandProperty DisplayName #Gets the managers name

$report = "Human Resources,

The user account for $unn ($un) has been disabled from the company network as of $dt. All email messages will be forwarded to $mann ($man) for now on.

Regards,

$authn ($auth)"

Send-MailMessage -To HR@MyCompany.com, IT@MyCompany.com -Subject "Disconnected User Report" -Body $report -From IT@MyCompany.com -SmtpServer Exchange
```