---
tags: [Getting Started, Developer Portal, API Keys]
---

# Getting Started with Exchange

The developer studio allows users to view and use documentation for Exchange. This is seperated into two sections, the [Documentation](?path=/docs/introduction/exchange-intro.md) and the specs + schema on the [API Explorer](../api/?type=post&path=/boarding/add_application)

---

## Boarding APIs

Building your Exchange integration

<!-- type: row -->

<!-- type: card
title: Add Application
description: Adds a merchant, and a subgroup. Offerings can be retrieved with the offering APIs, and settings can be used for funding/billing settings when not using defaults. Returns identifiers Application reference, and internal MID. Application data will typically be the legal entity for the business.
link: ../api/?type=post&path=/boarding/add_application
-->

<!-- type: card
title: Add Outlet 
description: Adds an outlet to the parent mid and reference. Parent MID should be the internal_mid of the subgroup returned in add application or add subgroup, with reference that is also returned. Outlet will typically be the data of the trading location, and multiple outlets can be added for submission if they share the same 'Merchant' level data (ie. under the same legal entity + info)
link: ../api/?type=post&path=/boarding/outlet/add
-->

<!-- type: card
title: Submit Application
description: Submits an application to its next step in the workflow.
link: ../api/?type=post&path=/boarding//application
-->

<!-- type: row-end -->

---