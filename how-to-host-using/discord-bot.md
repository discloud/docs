---
description: >-
  Learn how to quickly host your applications through our Discord server using
  our bot.
icon: robot
---

# Discord Bot

Discloud allows you to **host applications directly from Discord**, making deployment fast and accessible without needing to use a dashboard or command-line tools.

***

## 🔑 Account Verification

{% hint style="warning" %}
#### **Verification System Under Maintenance**

Our account verification system is temporarily unavailable, and **we are not performing manual verification during this period**.

If you are **already verified**, you can ignore this notice and continue using the Bot normally.

If you are **NOT yet verified**, you can upload and manage your applications using other methods:

* [Control Panel](dashboard.md)
* [CLI](cli.md)
* [Visual Studio Code Extension](visual-studio-code.md)

Need help? Open a **support ticket** by sending a message to the [**Ticket Bot DM**](https://discord.com/channels/@me/930852077045940224/). Make sure you are in the [Discloud Discord Server](https://discord.discloudbot.com/).

Stay in the server to be notified when your ticket is answered and when the verification system is back.
{% endhint %}

***

## 🚀 Hosting Your Application

There are **two ways** to deploy an application using the Discloud Bot:

<table><thead><tr><th width="212">Method</th><th>Best For</th><th>How It Works</th></tr></thead><tbody><tr><td><a href="discord-bot.md#advanced-setup"><strong>⚙️ Advanced Setup</strong></a></td><td>Users who want a <strong>one-command</strong> deployment with pre-configured settings.</td><td>Configure everything in the <a href="../configurations/discloud.config/"><code>discloud.config</code></a> file and use <code>.upconfig</code>.</td></tr><tr><td><a href="discord-bot.md#quick-setup-step-by-step-guide"><strong>⚡ Quick Setup (legacy)</strong></a></td><td>Users who <strong>prefer a guided setup</strong> via the bot’s prompts.</td><td>The bot will ask for the necessary details after running <code>.up</code>.</td></tr></tbody></table>

{% hint style="warning" %}
#### **Important Notes**

* If your [**main file**](../faq/general-questions/what-is-the-main-file.md) **is not in the** [**root directory**](../faq/general-questions/what-is-the-root-of-the-project.md), you **must** use Advanced Setup or move it to the root.
* If you are hosting a **bot without an ID** (e.g., WhatsApp or Telegram), use Advanced Setup and Discloud will generate the ID automatically.
{% endhint %}

{% tabs %}
{% tab title="📝 Advanced Setup" %}
{% stepper %}
{% step %}
Create the [`discloud.config`](../configurations/discloud.config/) file.
{% endstep %}

{% step %}
Compress your project into a [`.zip`](../faq/general-questions/wip-how-to-compress.md) file.
{% endstep %}

{% step %}
Upload your project.

* Go to [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) on the **Discloud Discord Server**.
*   Run the following command:

    ```
    .upconfig
    ```
* Send your [**.zip**](../faq/general-questions/wip-how-to-compress.md) file when prompted.
{% endstep %}

{% step %}
Your application will be deployed automatically.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="⚡ Quick Setup (Step-by-Step Guide)" %}
{% tabs %}
{% tab title="🤖 Bot" %}
{% stepper %}
{% step %}
Prepare your project.

* Ensure your application files are correctly structured.
* Compress your project into a [`.zip`](../faq/general-questions/wip-how-to-compress.md) file.
{% endstep %}

{% step %}
Upload your project.

* Go to [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) on the **Discloud Discord Server**.
*   Run the following command:

    ```
    .up
    ```
{% endstep %}

{% step %}
Provide the Required Information.

* **Enter the** [**Application ID**](../faq/general-questions/wip-how-can-i-get-my-bots-id.md) (for Discord bots).
* **Enter the** [**Main File Name**](../faq/general-questions/what-is-the-main-file.md) (e.g., `index.js`, `main.py`, `main.go`).
* **Specify the RAM** for your bot (e.g., `100` for 100MB).

{% hint style="info" %}
When specifying the amount of RAM, **you do not need** to include units like "MB". Simply enter the numeric value, for example, "100" for 100MB.

```
           BOTs require a minimum of 100MB of RAM.
```
{% endhint %}
{% endstep %}

{% step %}
Send your [`.zip`](../faq/general-questions/wip-how-to-compress.md) file when prompted.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🌐 Website" %}
{% stepper %}
{% step %}
Prepare your project.

* Ensure your application files are correctly structured.
* Compress your project into a [`.zip`](../faq/general-questions/wip-how-to-compress.md) file.
{% endstep %}

{% step %}
Upload your project.

* Go to [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) on the **Discloud Discord Server**.
*   Run the following command:

    ```
    .upsite
    ```
{% endstep %}

{% step %}
Provide the Required Information.

* **Choose a** [**Subdomain**](../faq/general-questions/how-to-create-a-subdomain.md).
* **Enter the** [**Main File Name**](../faq/general-questions/what-is-the-main-file.md) (e.g., `index.html`, `index.php`).
* **Specify the RAM** for your bot (e.g., `512` for 512MB).

{% hint style="info" %}
When specifying the amount of RAM, **you do not need** to include units like "MB". Simply enter the numeric value, for example, "512" for 512MB.

```
           Websites require a minimum of 512MB of RAM.
```
{% endhint %}
{% endstep %}

{% step %}
Send your [`.zip`](../faq/general-questions/wip-how-to-compress.md) file when prompted.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## **❓ Still need help?**

Check the [**FAQ Section**](/broken/pages/XnfTZsmKo9RRBUwNSPYU) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
