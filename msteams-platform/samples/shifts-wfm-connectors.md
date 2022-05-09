---
title: Production-ready Shifts Connectors
description: Learn about the benefits of using Workforce management Shifts connectors for Teams, such as Kronos-to-Teams Shifts connector and JDA-to-Teams Shifts connector
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
ms.localizationpriority: high
keywords: Microsoft Teams connectors kronos
ms.author: lajanuar
---

# Production-ready Shifts Connectors  

Teams Shifts Workforce management (WFM) connectors are production-ready, open-source, and community-driven integrations, useful for first-line workers. They offer a seamless experience and quick process for the digital transformation of first-line workers with Teams Shifts.

Each connector provides detailed guidance for deployment and integration to your organization. The complete source code is available in GitHub repository. You can explore in detail or fork, and customize to meet your specific needs.

This document gives an overview of key benefits of Teams Shifts WFM connectors, Kronos-to-Teams Shifts connector, and JDA-to-Teams Shifts connector.

## Key benefits of Teams Shifts WFM connectors

Following are the key benefits of Teams Shifts WFM connectors:

* **Plug and play experience:** All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure. No coding is required to deploy the apps.

* **Production-ready code:** All Shifts connectors conform to the recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.

* **Customizable and extensible:** While all Shifts WFM connectors are ready to deploy for immediate use, with the entire code base and deployment scripts readily available. You can easily customize or extend them to fit your unique needs.

* **Detailed documentation & support:** All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps. The connector repositories are monitored, so that you can report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.

* **Seamless integration:** The integration between WFM solutions and Teams Shifts allows first-line workers to use the Teams Shifts app to view or manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.  

Open shifts view in Teams:

The shifts view in Teams is shown in the following image:

![Open shifts in Teams](../assets/images/teams-open-shifts-view.png)

## Kronos-to-Teams Shifts connector

With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts such as, desktop or mobile Teams app for the following first-line worker and manager scenarios:

* View schedule.

* Publish and request open shifts.

* Swap shifts.

* Request time off.

* Offer shifts.

For more information on deployment of Kronos-to-Teams Shifts connector, see [Get it on GitHub](https://aka.ms/KronosShiftsConnector).

## JDA-to-Teams Shifts connector

With open-source code, you can integrate JDA, such as BlueYonder Version 17.2 and above, with Teams Shifts  such as, desktop or mobile Teams app for the following first-line worker and manager scenarios:

* Publish shifts and schedule groups in JDA and view them in Teams.

* Enable rich scheduling scenarios, including requesting shift swaps and time off.

* Set user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).

For more information on contribution and suggestion, see [Get it on GitHub](https://aka.ms/JDAShiftsConnector).

## See also

[Integrate web apps](~/samples/integrate-web-apps-overview.md)
