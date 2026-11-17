---
description: >-
  Best practices for storing your application's tokens and passwords, and what
  to do if one of them leaks.
---

# How do I protect my tokens?

Tokens, passwords and API keys give access to your application and your accounts. Anyone with your bot's token can control it.

***

## ✅ Best practices

* Keep secrets in the dashboard's [**environment variables**](../../platform-features/environment-variables.md), never directly in your code.
* Read the values in your code from the variables, for example `process.env.TOKEN` or `os.getenv("TOKEN")`.
* Don't push the [`.env`](.env-file.md) file to GitHub. Add it to `.gitignore`.
* Don't keep secrets in [`discloud.config`](../../configurations/discloud.config/).
* Don't show tokens in screenshots, videos or support messages.
* Give access to your applications through [Teams](../../platform-features/teams-and-permissions.md), with the right role for each person, instead of sharing your account.

{% hint style="warning" %}
A public repository with a token, even for a short time, should be treated as a leak. There are bots that scan GitHub for tokens all the time.
{% endhint %}

***

## 🚨 If a token leaked

{% stepper %}
{% step %}
**Generate a new token**

Generate the token again at its source. For a Discord bot, use **Reset Token** in the [Developer Portal](https://discord.com/developers/applications). The old token stops working immediately.
{% endstep %}

{% step %}
**Update the variables**

Put the new token in the application's environment variables and rebuild or deploy again.
{% endstep %}

{% step %}
**Deleting the file isn't enough**

If the token ended up in Git, deleting the file isn't enough: it stays in the history. Generating a new token is what fixes it.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
The same applies to the [Discloud API token](how-can-i-get-my-discloud-api-token.md). If it leaks, generate a new one.
{% endhint %}
