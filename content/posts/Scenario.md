+++
date = '2025-09-10T17:19:50-05:00'
draft = false
title = 'Scenario'
+++

## Scenario

You and I work for an apparel manufacturing company called Citizenry Apparel (CA) as a part of their IT team.   This company hosts an internal artists and design teams to come up with the graphics, along with manufacturing teams and shipping teams.

## Current Situation

Citizenry Apparel has experienced a major surge success with its products in recent months, shipping products all across the US.   The problem is, the current IT infrastructure cannot keep up with what the business needs to keep up with demand.   The current hardware is running out of storage and faces frequent outages due to hardware failures, which impacts the production and operation aspects of the company.   Leadership has asked the IT team to come up with a plan to overcome these obstacles without major spending on capital investments while ensuring the company's applications remain available and secure for production and operations, while following PCI DSS regulations, since we sell to the public and process credit card information.

Your current computer environment is predominantly Windows Server 2016 and Windows Server 2019 OS, with an ActiveDirectory environment for user authentication.  ActiveDirectory is connected an M365/Exchange Online presence with EntraSync.

CA has purchased an ERP system called InkPress that tracks raw materials (tape, ink, shirts, stencil materials), manufacturing processes of screen printing and tagging, and inventorying the finished product from packaging through shipping.   The InkPress also handles order handling/tracking, design management, and accounting.

The InkPress system has a backend database and several web-based applications, depending on the function of CA's manufacturing process.

We receive updates for InkPress through it's manufacturer DevOps CI/CD pipelines.   We simply pull down their latest Production updates and deploy to our servers.

## Our Goal

Since leadership has determined that we are not to make any major capital investments into a server refresh (which would be very expensive in materials and labor), the IT Team is researching this Microsoft Azure cloud technology offerings.   We could look at Amazon's AWS or Google Cloud Platform, but we already have connections to M365, which leads us to consider Azure over AWS or GCP.

Our solution must:

1) Consist of no major capital expenditures
2) Be reliable for Production and Operations
3) Secure to comply to PCI DSS standards and Best Business Standards, such as securing company and customer information

## Next post

Before we deploy one server, we need to secure our working environment (the Azure tenant).   This is the topic of the next post.
