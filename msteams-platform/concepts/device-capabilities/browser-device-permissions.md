---
title: Device permissions for the browser
keywords: teams apps capabilities permissions
description: Securely bring back device permissions support for apps in our web client
localization_priority: high
ms.topic: how-to
---

# Device permissions for the browser

Teams app that require device permissions, such as camera or microphone access, now require users to manually grant permission at a per app level in the web browser. Previously, the browser handled how to grant access permissions, but now these permissions are handled in Microsoft Teams. This has implications on how you design your application and if they require these permissions in the browser.

## Enable app's device permissions

If your Teams app has declared in the [application manifest](native-device-permissions.md#specify-permissions) that it needs device permissions, then the **App permissions** option appears for the users to enable the app's device permissions. The **App permissions** option is available in the following capabilities:

* **Personal apps and task module dialogs**: The **App permissions** option is available in the upper-right corner of the page.
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **Chats, channel, or meeting tabs**: The **App permissions** option is available in the dropdown of the tab.
![App permissions drop-down](../../assets/images/tabs/drop-downapppermissions.png)

After the **App permissions** option is selected, a popup appears where the user can enable the permissions button.

A user will need to enable these permissions in the browser for these permissions to take effect. After user changes the app’s device permissions in the browser, they're prompted to reload the application in Teams.

> [!IMPORTANT]
> You must make users aware of where to go to enable these **App permissions** in Microsoft Teams.

## Recommendation

Teams app that require device permissions in the browser must show instructions to users on where to find and enable these permissions in the Teams UI. Depending on the context in which your application is running, you need to ensure that your instructions are pointing the user to correct location to access these permissions, as they differ for personal apps, task module dialogs, tabs in chats, and channels or meetings.

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## Code sample

|Sample name | Description | Node.js |
|----------------|-----------------|--------------|
| Tab device permissions for browser | The sample code demonstrates how to show the device permissions for browser. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## Step-by-step guide

Follow the [step-by-step guide](../../sbs-tab-device-permissions.yml) to grant tab device permission in Microsoft Teams.

## See also

* [Device capabilities overview](device-capabilities-overview.md)
* [Request device permissions](native-device-permissions.md)
