---
description: >-
  View your application's logs on Discloud to understand errors and follow what
  is happening.
---

# How to access the application logs?

**Logs** show everything your application writes to the terminal: startup messages, warnings and errors. They are the first place to look when your application doesn't start, goes offline, or doesn't behave as expected.

***

## 📋 Where to see the logs

{% tabs %}
{% tab title="🖥️ Dashboard" %}
{% stepper %}
{% step %}
Open the [**Discloud Dashboard**](https://discloud.com/dashboard) and go to your applications.
{% endstep %}

{% step %}
Click your application.
{% endstep %}

{% step %}
In the side menu, click **Logs**.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
On the logs page you can:

* **Search** for text in the logs.
* Choose the **time range** you want to see (for example, the last hour).
* Turn on **live** mode to see new logs as they come in.
* Show or hide the **timestamp** of each line.
* Filter by level: **Trace**, **Debug**, **Info**, **Warn**, **Error** and **Fatal**.
{% endhint %}
{% endtab %}

{% tab title="🤖 Discord Bot" %}
{% stepper %}
{% step %}
Go to the [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) channel on the **Discloud Discord Server**.
{% endstep %}

{% step %}
Run the command:

```
/logs
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="⌨️ CLI" %}
Run:

```bash
discloud app logs <APPLICATION_ID>
```

See how to install and sign in to the [CLI](../../how-to-host-using/cli.md).
{% endtab %}

{% tab title="🟦 VS Code" %}
{% stepper %}
{% step %}
Open the **Discloud** tab in the VS Code sidebar.
{% endstep %}

{% step %}
In the **Apps** list, right-click the application and choose **Get app logs**.
{% endstep %}
{% endstepper %}

See how to install and sign in to the [VS Code extension](../../how-to-host-using/visual-studio-code.md).
{% endtab %}

{% tab title="🔌 API" %}
Send a `GET` request to:

```
/app/{appID}/logs
```

See the endpoint details in [**Applications**](../../api-and-integrations/api-overview/applications.md).
{% endtab %}
{% endtabs %}

***

## 🔍 What to look for in the logs

* **Errors on startup:** check that your [main file](what-is-the-main-file.md) and [`discloud.config`](../../configurations/discloud.config/) are correct.
* **Missing dependencies:** check that they're all listed in your language's dependency file (for example, `package.json` or `requirements.txt`).
* **The application stops on its own:** see [**Diagnosing Offline Applications**](../troubleshooting-solutions/diagnosing-offline-applications.md).

{% hint style="info" %}
When asking for help in support, include the part of the logs with the error. It makes finding the problem much faster.
{% endhint %}

***

## ❓ Still need help?

See [**Troubleshooting Solutions**](../troubleshooting-solutions/) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
