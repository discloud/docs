---
description: >-
  What to check when the bot shows as online on Discord but doesn't respond to
  commands or messages.
---

# Why isn't my bot responding?

If the bot shows as **online** on Discord but ignores commands and messages, the application is running. The problem is almost always in Discord's permissions or in the bot's configuration, not on Discloud.

***

## 🔎 Start with the logs

Open the application's [logs](../general-questions/how-to-access-the-application-logs.md) and look for errors right after startup. Some common messages:

| Message in the logs                       | What it means                                                           |
| ----------------------------------------- | ----------------------------------------------------------------------- |
| `Used disallowed intents`                 | The code asks for an intent that isn't enabled in the Developer Portal. |
| `An invalid token was provided`           | The bot token is wrong, expired or was regenerated.                     |
| `Missing Access` or `Missing Permissions` | The bot doesn't have permission in the server or channel.               |

***

## ⚙️ Intents

Discord only delivers the events the bot declares in its **intents**. Some of them, the **privileged** ones, also need to be enabled in the [Discord Developer Portal](https://discord.com/developers/applications), under **Bot → Privileged Gateway Intents**:

* **Message Content Intent**, to read message content (prefix commands like `!ping`).
* **Server Members Intent**, for member events and member lists.
* **Presence Intent**, for user status and activities.

After enabling them in the portal, declare the same intents in your code:

{% tabs %}
{% tab title="discord.js" %}
```javascript
const { Client, GatewayIntentBits } = require("discord.js");

const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.MessageContent,
  ],
});
```
{% endtab %}

{% tab title="discord.py" %}
```python
import discord

intents = discord.Intents.default()
intents.message_content = True

client = discord.Client(intents=intents)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If the bot only uses **slash commands**, the Message Content Intent isn't needed.
{% endhint %}

***

## 🧩 Slash commands

If slash commands don't show up or don't respond:

* Check that your code **registers** the commands. Global commands can take a while to show up.
* Check that the bot was invited with the **`applications.commands`** scope, in addition to the `bot` scope.
* Respond to the interaction within **3 seconds**. If the action takes longer, call `deferReply` (discord.js) or `defer` (discord.py) first.

***

## 🔐 Server permissions

* Check the bot's role in the server settings and in each channel's permissions.
* The bot needs **View Channel** and **Send Messages** in the channel where it should respond.
* If you changed the permissions in the invite, invite the bot again with the updated link.

***

## 🔑 Token

If the token was regenerated in the Developer Portal, the old one stops working. Update the token in the application's [environment variables](../../platform-features/environment-variables.md) and rebuild or deploy again.

***

## ❓ Still need help?

See [**Troubleshooting Solutions**](./) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
