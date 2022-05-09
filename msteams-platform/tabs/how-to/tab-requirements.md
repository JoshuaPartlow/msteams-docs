---
title: Prerequisites
author: surbhigupta
description: Every tab in Microsoft Teams must adhere to these requirements.
keywords: teams tabs group channel configurable
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
---

# Prerequisites

Ensure that you adhere to the following prerequisites while building your Teams personal and channel or group tab:

* Allow your tab pages to be discovered in an iFrame, using X-Frame-Options and Content-Security-Policy HTTP response headers.
  * Set header: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * For Internet Explorer 11 compatibility, set `X-Content-Security-Policy`.
  * Alternately, set header `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/`. This header is deprecated but still accepted by most browsers.

* Login pages don't render in iFrames, as a safeguard against clickjacking. Your authentication logic needs to use a method other than redirect. For example, use token-based or cookie-based authentication.

    > [!NOTE]
    > It is recommended that you set the intended use for your cookies rather than rely on default browser behavior. For more information, see [SameSite cookie attribute](../../resources/samesite-cookie-update.md).

* Browsers same-origin policy restriction prevents webpages from making requests to different domains than the served web page. So, you can redirect the configuration or content page to another domain or subdomain. Your cross-domain navigation logic needs to allow the Teams client to validate the origin against a static `validDomains` list in the app manifest when loading or communicating with the tab.

* Style your tabs based on the Teams client's theme, design, and intent. Tabs work best when they're built to address a specific need and focus on a small set of tasks or a subset of data that is relevant to the tab's channel location.

* Within your content page, add a reference to [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) using script tags. After your page loads, make a call to `app.initialize()`, otherwise your page is not displayed.

* For authentication to work on mobile clients, you must upgrade to Teams JavaScript SDK 1.4.1 and later.

* If you choose to have your channel or group tab to appear on Teams mobile client, the `setConfig()` configuration must have a value for the `websiteUrl` property.

* Microsoft Teams tab does'nt support the ability to load intranet websites that use self-signed certificates.

[!INCLUDE [sdk-include](msteams-docs/msteams-platform/includes/sdk-include.md)]

## Tools to build tabs

| &nbsp; | Install | For using... |
| --- | --- | --- |
| **Required** | &nbsp; | &nbsp; |
| &nbsp; | [Node.js](https://nodejs.org/en/download/) | Back-end JavaScript runtime environment. Use the latest v14 LTS release.|
| &nbsp; | [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/) | A browser with developer tools. |
| &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript, TypeScript, or SharePoint Framework (SPFx) build environments. |
| &nbsp; | [Visual Studio 2019](https://visualstudio.com/download), **ASP.NET and web development**, or **.NET Core cross-platform development** workload | .NET. You can install the free community edition of Visual Studio 2019. |
| &nbsp; | [Git](https://git-scm.com/downloads) | Git to use the sample apps repo from GitHub. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/en-us/microsoft-teams/download-app) | Microsoft Teams to collaborate with everyone you work with through apps for chat, meetings, call - all in one place. |
| &nbsp; | [ngrok](https://ngrok.com/download) | Ngrok is a reverse proxy software tool. Ngrok creates a tunnel to your locally running web server's publicly available HTTPS endpoints. Your server's web endpoints are available during the current session on your computer. When the computer is shut down or goes to sleep, the service is no longer available. |
| &nbsp; | [Developer Portal for Teams](https://dev.teams.microsoft.com/) | Web-based portal to configure, manage, and distribute your Teams app including to your organization or the Teams store. |

### Build your Teams tab

Now let's build your tab. But first select your choice of tab to build:

> [!div class="nextstepaction"]
> [Build a personal tab](~/tabs/how-to/create-personal-tab.md)
> [!div class="nextstepaction"]
> [Build a channel or group tab](~/tabs/how-to/create-channel-group-tab.md)

## See also

* [Teams tabs](~/tabs/what-are-tabs.md)
* [Tabs on mobile](~/tabs/design/tabs-mobile.md)