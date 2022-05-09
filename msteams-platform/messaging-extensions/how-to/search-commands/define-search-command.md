---
title: Define message extension search commands
author: surbhigupta
description: Learn about message extension search commands for Microsoft Teams apps, to create a search command through app manifest and manually using code examples and sample.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
---
# Define message extension search commands

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

Message extension search commands allow users to search external systems and insert the results of that search into a message in the form of a card. This document guides you on how to select  search command invoke locations, and add the search command to your app manifest.

> [!NOTE]
> The result card size limit is 28 KB. The card is not sent if its size exceeds 28 KB.

## Select search command invoke locations

The search command is invoked from any one or both of the following locations:

* Compose message area: The buttons at the bottom of the compose message area.
* Command box: By @mentioning in the command box.

  When search command is invoked from the compose message area, the user sends the results to the conversation. When it is invoked from the command box, the user interacts with the resulting card, or copies it for use elsewhere.

The following image displays the invoke locations of the search command:

:::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-locations.png" alt-text="Search command invoke locations":::

## Add the search command to your app manifest

To add the search command to your app manifest, you must add a new `composeExtension` object to the top level of your app manifest JSON. You can add the search command either with the help of App Studio, or manually.

### Create a search command using App Studio

The prerequisite to create a search command is that you must already have created a message extension. For information on how to create a message extension, see [create a message extension](~/messaging-extensions/how-to/create-messaging-extension.md).

To create a search command:

1. Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.
1. If you already created your app package in **App Studio**, select from the list. If you have not created an app package, import an existing one.
1. After importing app package, select **Message extensions** under **Capabilities**. You get a pop-up window to set up the message extension.
1. Select **Set up** in the window to include the message extension in your app experience. The following image displays the message extension set up page:

    :::image type="content" source="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt-text="Messaging extension set up":::

1. To create the message extension, you need a Microsoft registered bot. You can either use an existing bot or create a new bot. Select **Create new bot** option, give a name for the new bot, and select **Create**. The following image displays bot creation for message extension:

    :::image type="content" source="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt-text="Create bot for messaging extension":::

1. To use an existing bot, select **Use existing bot** and select **Select from one of my existing bots** to choose the existing bots from the dropdown, give a **Bot name** and select **Save** or select **Connect to a different bot id** if you have a bot id created already, give a **Bot name** and select **Save**.

    :::image type="content" source="~/assets/images/messaging-extension/use-existing-bot.png" alt-text="Use existing bot for messaging extension":::

1. Select **Add** in the **Command section** of the message extensions page to include the commands which decides the behaviour of message extension.
The following image displays command addition for message extension:

    :::image type="content" source="~/assets/images/messaging-extension/include-command.png" alt-text="Include command":::

1. Select **Allow users to query your service for information and insert that into a message**. The following image displays the search command parameter selection:

    :::image type="content" source="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt-text="Search command parameter selection":::

1. Add a **Command Id** and a **Title**.
1. Select the location from where your search command must be invoked. The following image displays the search command invoke location:

    :::image type="content" source="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt-text="Search command invoke location selection":::

1. Add your search parameter and select **Save**.

### Create a search command manually

To manually add your message extension search command to your app manifest, you must add the following parameters to your `composeExtension.commands` array of objects:

| Property name | Purpose | Required? | Minimum manifest version |
|---|---|---|---|
| `id` | This property is an unique ID that you assign to search command. The user request includes this ID. | Yes | 1.0 |
| `title` | This property is a command name. This value appears in the user interface (UI). | Yes | 1.0 |
| `description` | This property is a help text indicating what this command does. This value appears in the UI. | Yes | 1.0 |
| `type` | This property must be a `query`. | No | 1.4 |
|`initialRun` | If this property is set to **true**, it indicates this command should be executed as soon as the user selects this command in the UI. | No | 1.0 |
| `context` | This property is an optional array of values that defines the context the search action is available in. The possible values are `message`, `compose`, or `commandBox`. The default is `["compose", "commandBox"]`. | No | 1.5 |

You must add the details of the search parameter, that defines the text visible to your user in the Teams client.

| Property name | Purpose | Is required? | Minimum manifest version |
|---|---|---|---|
| `parameters` | This property defines a static list of parameters for the command. | No | 1.0 |
| `parameter.name` | This property describes the name of the parameter. This is sent to your service in the user request. | Yes | 1.0 |
| `parameter.description` | This property describes the parameter’s purposes or example of the value that must be provided. This value appears in the UI. | Yes | 1.0 |
| `parameter.title` | This property is a short user-friendly parameter title or label. | Yes | 1.0 |
| `parameter.inputType` | This property is set to the type of the input required. Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`. Default is set to `text`. | No | 1.4 |

#### Example

Following section is an example of the simple app manifest of the `composeExtensions` object defining a search command:

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```

For the complete app manifest, see [App manifest schema](~/resources/schema/manifest-schema.md).

## Code sample

| Sample Name           | Description | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams message extension search   |  Describes how to define search commands and respond to searches.        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## Step-by-step guide

Follow the [step-by-step guide](../../../sbs-messagingextension-searchcommand.yml) to build a search based message extension.

## Next step

> [!div class="nextstepaction"]
> [Respond to the search commands](~/messaging-extensions/how-to/search-commands/respond-to-search.md).
