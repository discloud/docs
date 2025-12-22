---
description: Learn how to host Discord bots on Discloud.
icon: robot
---

# Bots

## 🤖 What is a "Bot" on Discloud?

On **Discloud**, a **Bot** is any application that runs continuously but does **not** require an external port for access. This typically includes:

* 🤖 **Discord Bots** (discord.js, discord.py, JDA, etc.)
* 💬 **Telegram Bots**
* ⚙️ **Automation Scripts**

***

## ✅ Requirements

To host a bot, you must meet these criteria:

{% hint style="success" %}
**Any Plan** – Bots can be hosted on any plan, including the Free plan (with limitations).
{% endhint %}

{% hint style="success" %}
[**`discloud.config`**](../configurations/discloud.config/) – Required for most deployment methods. If using the Discord Bot's [**Quick Setup**](../how-to-host-using/discord-bot.md#quick-setup-step-by-step-guide), the bot will guide you through the configuration.
{% endhint %}

{% hint style="success" %}
**RAM** – Ensure you allocate enough RAM for your bot's needs (min. 100MB).
{% endhint %}

***

## 🚀 Step-by-Step Hosting Guide

{% stepper %}
{% step %}
#### 📝 Configure `discloud.config`

{% hint style="info" %}
If you are using the Discord Bot's **Quick Setup**, you don't need to create this file manually, the Discord bot will ask for the information during the process.
{% endhint %}

```ini
NAME=MyCoolBot
TYPE=bot
MAIN=index.js
RAM=100
VERSION=latest
```

* **`TYPE=bot`**: Identifies the app as a bot/background service.
* **`MAIN`**: The entry point of your application. [Learn more about the main file.](../faq/general-questions/wip-what-is-the-main-file.md)
* **`RAM`**: Allocated memory (min. 100MB).
{% endstep %}

{% step %}
#### 🏗️ Handling Build Processes

If your bot requires a build step (like TypeScript or Java), you have two options:

{% tabs %}
{% tab title="Discloud Build (Recommended)" %}
Let Discloud handle the build process during deployment. Add the `BUILD` command to your `discloud.config`.

```ini
BUILD=npm run build
START=npm run start
```
{% endtab %}

{% tab title="Local Build" %}
Build your project locally and upload the resulting files.

{% hint style="danger" %}
**Do not use a folder named `dist`** for your local build output. Discloud reserves the `dist` directory for its internal build process. Use a different name like `build`, `out`, or `output`.
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
For Java applications, you **must** build locally and upload the `.jar` file. [See the Java build guide](../faq/general-questions/how-to-build-and-package-a-java-application.md).
{% endhint %}
{% endstep %}

{% step %}
#### 🚀 Upload and Deploy

You can upload your project using any of our supported methods:

* 🖥️ [**Dashboard**](../how-to-host-using/dashboard.md)
* ⌨️ [**CLI**](../how-to-host-using/cli.md)
* 🟦 [**VS Code Extension**](../how-to-host-using/visual-studio-code.md)
* 🤖 [**Discord Bot**](../how-to-host-using/discord-bot.md)
* 🐙 [**GitHub Integration**](../api-and-integrations/github-integration.md)

{% hint style="info" %}
Before uploading, make sure to [compress your project correctly](../faq/general-questions/wip-how-to-compress.md) and exclude unnecessary files using a [`.discloudignore`](../configurations/.discloudignore.md) file.
{% endhint %}
{% endstep %}
{% endstepper %}
