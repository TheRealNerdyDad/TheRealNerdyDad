+++
date = '2026-04-02'
draft = false
title = 'Project Apex Shield: Implementing Regional Guardrails with Bicep'
tags: ["Azure", "Bicep", "SRE", "Governance"]
+++

# Project Apex Shield: Implementing Regional Guardrails with Bicep

## The Business Problem: Cloud Sprawl

At **Apex Cloud Logistics**, the rapid adoption of Azure led to "Cloud Sprawl." Without strict governance, resources were being spun up in expensive, non-local regions, driving up operational costs.

As part of my transition into Site Reliability Engineering, my first initiative—**Project Apex Shield**—focuses on implementing automated financial governance using Infrastructure as Code.

## The Solution: Policy as Code

Instead of manually policing deployments, I wrote an Azure Policy using **Bicep**. This template acts as an automated guardrail, actively denying any resource creation outside of our designated `southcentralus` region.

Here is the Bicep configuration I deployed:

```bicep
targetScope = 'subscription'

@description('The regions allowed for Apex Cloud Logistics deployments.')
param allowedLocations array = [
  'southcentralus'
]

resource regionPolicy 'Microsoft.Authorization/policyAssignments@2024-05-01' = {
  name: 'apex-region-lock'
  properties: {
    displayName: 'Apex Shield: Restrict Deployments to South Central US'
    description: 'Enforces cost control by preventing resource creation in expensive non-local regions.'
    policyDefinitionId: '/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975a4c'
    parameters: {
      listOfAllowedLocations: {
        value: allowedLocations
      }
    }
  }
}
```
