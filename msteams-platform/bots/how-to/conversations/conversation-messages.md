---
title: Messages in bot conversations
description: Describes ways to have a conversation with a Microsoft Teams bot. Learn about Teams channel data, notification to your message, picture messages, adaptive cards using Code samples.
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
keyword: receive message send message picture message channel data adaptive cards
---

# Messages in bot conversations

Each message in a conversation is an `Activity` object of type `messageType: message`. When a user sends a message, Teams posts the message to your bot. Teams sends a JSON object to your bot's messaging endpoint. Your bot examines the message to determine its type and responds accordingly.

Basic conversations are handled through the Bot Framework connector, a single REST API. This API enables your bot to communicate with Teams and other channels. The Bot Builder SDK provides the following features:

* Easy access to the Bot Framework connector.
* Additional functionality to manage conversation flow and state.
* Simple ways to incorporate cognitive services, such as natural language processing (NLP).

Your bot receives messages from Teams using the `Text` property and it sends single or multiple message responses to the users.

## Receive a message

To receive a text message, use the `Text` property of the `Activity` object. In the bot's activity handler, use the turn context object's `Activity` to read a single message request.

The following code shows an example of receiving a message:

# [C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# [TypeScript](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# [Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# [JSON](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot.Sending bold-italic rich text",
    "attachments": [
      {
            "contentType": "text/html",
            "content": "<div><div>Hello Teams TestBot. Sending <strong>bold</strong>-<em>italic</em> rich text.</div>\n</div>"
      } 
    ],
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## Send a message

To send a text message, specify the string you want to send as the activity. In the bot's activity handler, use the turn context object's `SendActivityAsync` method to send a single message response. Use the object's `SendActivitiesAsync` method to send multiple responses at once.

The following code shows an example of sending a message when a user is added to a conversation:

# [C#](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# [TypeScript](#tab/typescript)

```typescript

    this.onMembersAddedActivity(async (context, next) => {
        await Promise.all((context.activity.membersAdded || []).map(async (member) => {
            if (member.id !== context.activity.recipient.id) {
                await context.sendActivity(
                    `Welcome to the team ${member.givenName} ${member.surname}`
                );
            }
        }));

        await next();
    });
```

# [Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# [JSON](#tab/json)

```json
{
    "type": "message",
    "from": {
        "id": "28:c9e8c047-2a34-40a1-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "conversation": {
        "id": "a:17I0kl8EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-",
        "name": "Convo1"
   },
   "recipient": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB25ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen"
    },
    "text": "My bot's reply",
    "replyToId": "1632474074231"
}

```

---

> [!NOTE]
> Message splitting occurs when a text message and an attachment are sent in the same activity payload. This activity is split into separate activities by Microsoft Teams, one with just a text message and the other with an attachment. As the activity is split, you do not receive the message ID in response, which is used to [update or delete](~/bots/how-to/update-and-delete-bot-messages.md) the message proactively. It is recommended to send separate activities instead of depending on message splitting.

Messages sent between users and bots include internal channel data within the message. This data allows the bot to communicate properly on that channel. The Bot Builder SDK allows you to modify the message structure.

## Teams channel data

The `channelData` object contains Teams-specific information and is a definitive source for team and channel IDs. Optionally, you can cache and use these IDs as keys for local storage. The `TeamsActivityHandler` in the SDK pulls out important information from the `channelData` object to make it easily accessible. However, you can always access the original data from the `turnContext` object.

The `channelData` object isn't included in messages in personal conversations, as these take place outside of a channel.

A typical `channelData` object in an activity sent to your bot contains the following information:

* `eventType`: Teams event type passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `tenant.id`: Microsoft Azure Active Directory (Azure AD) tenant ID passed in all contexts.
* `team`: Passed only in channel contexts, not in personal chat.
  * `id`: GUID for the channel.
  * `name`: Name of the team passed only in cases of [team rename events](subscribe-to-conversation-events.md#team-renamed).
* `channel`: Passed only in channel contexts, when the bot is mentioned or for events in channels in teams, where the bot has been added.
  * `id`: GUID for the channel.
  * `name`: Channel name passed only in cases of [channel modification events](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* `channelData.teamsTeamId`: Deprecated. This property is only included for backward compatibility.
* `channelData.teamsChannelId`: Deprecated. This property is only included for backward compatibility.

### Example channelData object (channelCreated event)

The following code shows an example of channelData object:

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

## Message content

Messages received from or sent to your bot can include different types of message content.

| Format    | From user to bot | From bot to user | Notes                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| Rich text | ✔                | ✔                | Your bot can send rich text, pictures, and cards. Users can send rich text and pictures to your bot.                                                                                        |
| Pictures  | ✔                | ✔                | Maximum 1024×1024 MB and 1 MB in PNG, JPEG, or GIF format. Animated GIF isn't supported.  |
| Cards     | ✖                | ✔                | See the [Teams card reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards. |
| Emojis    | ✔                | ✔                | Teams currently supports emojis through UTF-16, such as U+1F600 for grinning face. |

## Notifications to your message

You can also add notifications to your message using the `Notification.Alert` property. Notifications alert users about new tasks, mentions, and comments. These alerts are related to what users are working on or what they must look at by inserting a notice into their activity feed. For notifications to trigger from your bot message, set the `TeamsChannelData` objects `Notification.Alert` property to *true*. Whether or not a notification is raised depends on the individual user's Teams settings and you can't override these settings. The notification type is either a banner, or both a banner and an email.

> [!NOTE]
> The **Summary** field displays any text from the user as a notification message in the feed.

The following code shows an example of adding notifications to your message:

# [C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# [TypeScript](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# [Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# [JSON](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

To enhance your message, you can include pictures as attachments to that message.

## Picture messages

Pictures are sent by adding attachments to a message. For more information on attachments, see [add media attachments to messages](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments).

Pictures can be at most 1024×1024 MB and 1 MB in PNG, JPEG, or GIF format. Animated GIF isn't supported.

Specify the height and width of each image by using XML. In markdown, the image size defaults to 256×256. For example:

* Use: `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.
* Don't use: `![Duck on a rock](http://aka.ms/Fo983c)`.

A conversational bot can include Adaptive Cards that simplify business workflows. Adaptive Cards offer rich customizable text, speech, images, buttons, and input fields.

## Adaptive Cards

Adaptive Cards can be authored in a bot and shown in multiple apps such as Teams, your website, and so on. For more information, see [Adaptive Cards](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card).

The following code shows an example of sending a simple Adaptive Card:

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

### Form completion feedback

Form completion message appears in Adaptive Cards while sending a response to the bot. The message can be of two types, error or success:

* **Error**: When a response sent to the bot is unsuccessful, **Something went wrong, Try again** message appears.

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="Error message"border="true":::

* **Success**: When a response sent to the bot is successful, **Your response was sent to the app** message appears.

:::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="Success message"border="true":::

You can select **Close** or switch chat to dismiss the message.

**Response on mobile**:

The error message appears at the bottom of the Adaptive Card.

For more information on cards and cards in bots, see [cards documentation](~/task-modules-and-cards/what-are-cards.md).

## Status code responses

Following are the status codes and their error code and message values:

| Status code | Error code and message values | Description |
|----------------|-----------------|-----------------|
| 403 | **Code**: `ConversationBlockedByUser` <br/> **Message**: User blocked the conversation with the bot. | User blocked the bot in 1:1 chat or a channel through moderation settings. |
| 403 | **Code**: `BotNotInConversationRoster` <br/> **Message**: The bot isn't part of the conversation roster. | The bot isn't part of the conversation. |
| 403 | **Code**: `BotDisabledByAdmin` <br/> **Message**: The tenant admin disabled this bot. | Tenant blocked the bot. |
| 401 | **Code**: `BotNotRegistered` <br/> **Message**: No registration found for this bot. | The registration for this bot wasn't found. |
| 412 | **Code**: `PreconditionFailed` <br/> **Message**: Precondition failed, please try again. | A precondition failed on one of our dependencies due to multiple concurrent operations on the same conversation. |
| 404 | **Code**: `ConversationNotFound` <br/> **Message**: Conversation not found. | The conversation wasn't found. |
| 413 | **Code**: `MessageSizeTooBig` <br/> **Message**: Message size too large. | The size on the incoming request was too large. |
| 429 | **Code**: `Throttled` <br/> **Message**: Too many requests. Also returns when to retry after. | Too many requests were sent by the bot. For more information, see [rate limit](~/bots/how-to/rate-limit.md). |

## Code sample

|Sample name | Description | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Teams conversation bot | Messaging and conversation event handling. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## Next step

> [!div class="nextstepaction"]
> [Bot command menus](~/bots/how-to/create-a-bot-commands-menu.md)

## See also

* [Send proactive messages](~/bots/how-to/conversations/send-proactive-messages.md)
* [Subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [Send and receive files through the bot](~/bots/how-to/bots-filesv4.md)
* [Send tenant ID and conversation ID to the request headers of the bot](~/bots/how-to/conversations/request-headers-of-the-bot.md)
