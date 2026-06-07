---
description: >-
  Learn what the Discord Application ID (Client ID) is and how to find it in the
  Discord Developer Portal.
---

# How can I get my Discord bot ID?

## 🤖 What is the Discord Application ID?

The **Discord Application ID** (also called **Client ID**) is a unique numeric identifier that Discord assigns to every application created on the [Discord Developer Portal](https://discord.com/developers/applications).

{% hint style="info" %}
This is **not** the same as the **Discloud App ID**, which Discloud generates internally for your hosted application. The **Discord Application ID** comes from Discord itself and identifies your bot on Discord's platform, it's only required for the [Quick Setup flow via the Discloud Discord bot](../../how-to-host-using/discord-bot.md#quick-setup-step-by-step-guide).
{% endhint %}

***

## 📍 How to Get Your Discord Application ID

{% stepper %}
{% step %}
Open the [**Discord Developer Portal**](https://discord.com/developers/applications) and log in with your Discord account.
{% endstep %}

{% step %}
Click on your bot's application from the list.

If you haven't created an application yet, click the **New Application** button, give it a name, and create it.
{% endstep %}

{% step %}
On the **General Information** page (opened by default), copy the **Client ID**, this is your Discord Application ID.

![](../../.gitbook/assets/Discord-Developer-Portal_Copy-ClientID.png)
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
The **Application ID** is **public information**, it's safe to share. However, keep your **Bot Token** (found under the **Bot** tab) **secret**, as anyone with it can control your bot.
{% endhint %}

***

## 🔍 Where Do You Need It?

This ID is specifically required when using the **Quick Setup** method via the [Discloud Bot](../../how-to-host-using/discord-bot.md#quick-setup-step-by-step-guide), during the guided flow, the bot will prompt you to enter the Application ID.

If you're using **Advanced Setup** (with a [`discloud.config`](../../configurations/discloud.config/) file), you don't need to provide this ID, as Discloud handles the configuration automatically.
