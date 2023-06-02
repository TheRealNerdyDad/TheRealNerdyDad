---
title: Protecting The Jewel
date: 2021-02-06 17:00:00 -500
categories: [general,it]
tags: [general,it,security]
---
# Protecting The Jewel
So, in the last post, we discussed the biggest asset IT can have, the data. But, does the Queen of England keep her jewels out for everybody to be able to touch? Nope. Do banks let people walk right into the vaults to touch all of the money? No. So, what do we need to do to protect the data?

There are 2 big things that IT people do to protect their data, and they go hand-in-hand:

- Least Privileges (aka JITJEA, Just-In-Time, Just-Enough-Access)
- Backups

## Least Privileges
Does you remember when Edward Snowden released the NSA documents back in 2013? Regardless of which political party you most identify with, Snowden made big news and made companies rethink their internal IT security strategies. Basically, he had access to a LOT of documents, some he probably didn’t need access to. Was this his fault? No, it was the NSA’s for giving him access to all of the jewels instead of limiting his access to just what he needed to know and needed access to.

This is where the Least Privileges philosophy comes in. Give the user or administrator just enough access to do their job. If the user needs more access to fulfill their job requirements, then it is the responsibility of their supervisor to request access on behalf of the user. This access request also needs to be documented, preferably by a helpdesk ticket, in order to protect the IT department and the user in the event of an audit or investigation.

The least amount of people that have access to the data to manipulate the data, the safer the data is from losing its integrity. Does everybody need to have the ability to store files on the file server? No? Then look at the permissions of the file server and begin taking people out that have no business in that particular folder. If they truly need access, then they will ask their supervisor, who will then submit a ticket asking for permission on behalf of the user.

## Backups
Backups are **CRITICAL** to an organization. If a critical system within the organization accidentally corrupts the data, then how would the data or system be recovered without a backup? It can’t. Like I said before, without that data, it could be catastrophic to the organization. Backups needs to have the ability of doing 3 things:

## Restore
What good is a backup if you cannot get data out of the backup? Its not. This is why it is imperative for the administrator to check their backups and make sure that they are reliable backups.

## Restore data back in time
Time travel is great, in backups. I have had users come back to me and tell me that they accidentally deleted a file (eh, it happens, we’re all human, but it took away availability) from last week and they need it restored. What if you only had one set of backups that were taken last night? That file that the user needed could be critical to the organization, and now it is gone because last night’s backup just overwrote the backup from before that the file was on. This is why it is necessary to have incremental backups in different points in time for critical systems.

## Survive a real world catastrophe
There have been a number of natural disasters, from the tsunami of Sri Lanka to Hurricane Katrina to Superstorm Sandy to Hurricane Harvey. Natural disasters can happen anywhere. What happens if it is at your location? Will your backups survive the devastation or will it be safe at another location outside of harms way? Could your organization survive without the data? If not, then it probably needs to also be stored offsite of your production location.

This is where the 3-2-1 rule comes into play. Many people have different philosophies on this rule, but this is my take on it. It is not hard and fast, but has helped me in the past. You need to have 3 copies of your critical data (1 in production, 1 onsite, and 1 offsite). Production data is just as it sounds, the data that the company is currently running on. Onsite backups can be on the same physical site as the production system, but are not at a risk of being lost if the production system was to fail for some reason. This allows for quick recovery, less downtime, and less production revenue loss. Offsite data is the set of backups that are offsite. As mentioned before, if the production facility was to be destroyed by whatever means necessary, the organization could rebuild (from insurance money, etc) and restore the data from the offsite data.

## Backup Management
Find a way to manage these backups and how you plan on keeping up with them. There are a lot of good management platforms out there. Depending on your environment and needs will determine the strategy and management of the system that you need.   Test your backups.   Make sure you can rely on them in the event of an emergency.   Then, when disaster does happen, you will know you can rely on them and not hope that they will still work.