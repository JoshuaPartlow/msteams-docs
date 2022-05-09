---
title: Designing your personal app
description: Learn how to design a Teams personal app and get the Microsoft Teams UI Kit, create components, such as, dashboard, form, task board for Mobile and Desktop experience. Learn the best practices for developing personal apps.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
keywords: ui kit personal app webview navigation bot tab iframe dashboard form template
--- 
# Designing your personal app for Microsoft Teams

A personal app can be a bot, private workspace, or both. Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.

To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.

## Microsoft Teams UI Kit

You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit. The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.

> [!div class="nextstepaction"]
> [Get the Microsoft Teams UI Kit (Figma)](https://www.figma.com/community/file/916836509871353159)

## Add a personal app

Users can add a personal app from the Teams store or app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="Example shows how to add a personal app from the app flyout." border="false":::

## Use a personal app (private workspace)

With a private workspace, users can view app content that's meaningful to them in a central location without leaving Teams.

(Implementation note: The private workspace is based on the [*personal tab*](../../tabs/how-to/create-personal-tab.md) capability.)

### Anatomy: Personal app (private workspace)

#### Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="Example shows personal tab's component anatomy." border="false":::

|Counter|Description|
|----------|-----------|
|A|**App attribution**: Your app name.|
|B|**Tabs**: Provides navigation for your personal app.|
|C|**More menu**: Includes additional app options and information.|
|D|**Primary navigation**: Provides navigation to your app other main Teams features.|

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="Example shows personal tab's structural anatomy." border="false":::

|Counter|Description|
|----------|-----------|
|A|**Tabs**: Provides navigation for your personal app.|
|1|**webview**: Displays your app content.|

#### Desktop

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="This example shows personal tab's component anatomy." border="false":::

|Counter|Description|
|----------|-----------|
|A|**App attribution**: Your app logo and name.|
|B|**Tabs**: Provides navigation for your personal app.|
|C|**Popout view**: Pushes your app content from a parent window to a standalone child window.|
|D|**More menu**: Includes additional app options and information. (You could alternatively make **Settings** a tab.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="This example shows personal tab's structural anatomy." border="false":::

|Counter|Description|
|----------|-----------|
|A|**Tabs**: Provides navigation for your personal app.|
|1|**iframe**: Displays your app content.|

### Design with UI templates and advanced components

Use one of the following Teams templates and components to help design your personal tab:

* [List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.
* [Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.
* [Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.
* [Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.
* [Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.
* [Left nav](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your personal app requires some navigation. In general, you should keep navigation to a minimum.

## Use a personal app (bot)

Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on artboard). Users interact with the bot in a tab you specify.

### Anatomy: Personal app (bot)

#### Mobile

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="Example shows the personal bot component anatomy." border="false":::

|Counter|Description|
|----------|-----------|
|A|**Bot entry point**: Entry point for users to access the bot feature in your personal app.|
|B|**Back button**: Takes users back to the private workspace.|
|C|**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).|
|D|**Compose box**: Input field for sending messages to the bot.|

#### Desktop

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="Example shows the anatomy of the personal bot component." border="false":::

|Counter|Description|
|----------|-----------|
|A|**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.|
|B|**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).|
|C|**Compose box**: Input field for sending messages to the bot.|

## Manage a personal tab

On the left side of Teams, users can right-click the personal app to pin, remove, and configure other app options.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="Example shows options for managing a personal app." border="false":::

## Best practices

Use these recommendations to create a quality app experience.

### Tab priority

#### Do: Show the most relevant content in the first tab

With responsive sizing, tabs on the right may become truncated or out of view.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="Example shows a personal app displaying the most relevant content in the first tab." border="false":::

#### Don’t: Lead with secondary content or metadata

Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="Example shows a personal app leading with secondary content or metadata." border="false":::

### Tab hierarchy

#### Do: Tabs should be of equal hierarchy and represent key app pages

Your tabs should categorize your app’s primary features and content. With responsive sizing, content on the right may become truncated or out of view.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="Example shows a personal app with tabs of equal hierarchy." border="false":::

#### Don't: Include different levels of hierarchy

Your content should progress in a logical order that helps users make sense of it. If you have two tabs that are closely related, consider combining them into one tab.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="Example shows a personal app with different levels of hierarchy." border="false":::

### First-run experience

#### Do: Include a first-run experience

There should be at least a welcome screen the first time you use a personal app. For bots, describe what your bot can do and provide quick actions, such as a sign-in button.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="Example shows what to do during a personal app first-run experience." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="Another example shows what to do during a personal app first-run experience." border="false":::

#### Don't: Start with a blank screen

Users might be confused if nothing displays the first time they run your app.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="Example shows what not to do during a personal app first-run experience." border="false":::

### Personalized content

#### Do: Aggregate app content relevant to a user

Whether it's a personal tab or bot, display content related to only a user's activity in your app.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="Example shows what to do with a personal app and personalized content." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="Another example shows what to do with a personal app and personalized content." border="false":::

#### Don’t: Show unrelated or overly broad content

In personal contexts, don’t display content for teams a user isn't part of. Personal bot content should focus on the individual—not a group.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="Example shows what not to do with a personal app and personalized content." border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="Another example shows what not to do with a personal app and personalized content." border="false":::

### Complex app features

#### Do: Allow users to access complex features in a browser

Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="Example shows how to handle complex app features with a personal app." border="false":::

#### Don’t: Include your entire app

Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="Example shows how not to handle complex app features with a personal app." border="false":::

## See also

These other design guidelines may help depending on the scope of your personal app:

* [Designing your tab](../../tabs/design/tabs.md)
* [Designing you bot](../../bots/design/bots.md)
