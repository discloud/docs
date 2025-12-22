---
description: >-
  Learn how to host websites, APIs, and dashboards on Discloud using subdomains
  and custom domains.
icon: globe-pointer
---

# Websites & APIs

## 🌐 What is a "Site" on Discloud?

On **Discloud**, any application that uses a **network port** and requires **external access** is considered a **Site**. This includes:

* 🖥️ **Websites** (Static or Dynamic)
* 🔌 **APIs** (REST, GraphQL, etc.)
* 📊 **Dashboards** (for Bots or standalone)
* 🤖 **Bots with Web Interfaces**

To allow external access, Discloud routes traffic through a proxy to **port 8080** and **host 0.0.0.0** of your application using a **subdomain** (e.g., `myapp.discloud.app`).

***

## ✅ Requirements

To host a website or API, you must meet these criteria:

{% hint style="success" %}
**Platinum Plan or Higher** – Required for all `TYPE=site` applications.
{% endhint %}

{% hint style="success" %}
**Port 8080 & Host 0.0.0.0** – Your application **must** listen on port `8080` and host `0.0.0.0` to be accessible externally.
{% endhint %}

{% hint style="success" %}
[**Subdomain**](../faq/general-questions/how-to-create-a-subdomain.md) – You must register a unique subdomain on Discloud.
{% endhint %}

{% hint style="success" %}
[**`discloud.config`**](../configurations/discloud.config/) – Required for most deployment methods. If using the Discord Bot's [**Quick Setup**](../how-to-host-using/discord-bot.md#quick-setup-step-by-step-guide), the bot will guide you through the configuration.
{% endhint %}

{% hint style="success" %}
**RAM** – A minimum of **512MB** is recommended for web applications.
{% endhint %}

***

## 🚀 Step-by-Step Hosting Guide

{% stepper %}
{% step %}
#### 📡 Register a Subdomain

Before deploying, you need to reserve your unique address on the `.discloud.app` domain.
{% endstep %}

{% step %}
#### 📝 Configure `discloud.config`

Your [`discloud.config`](../configurations/discloud.config/) file tells Discloud how to handle your site. You must set `TYPE=site` and include your `ID`.

{% hint style="info" %}
If you are using the Discord Bot's **Quick Setup**, you don't need to create this file manually, the bot will ask for the subdomain and other details during the process.
{% endhint %}

```ini
NAME=MyAwesomeAPI
TYPE=site
ID=my-unique-subdomain
MAIN=src/index.js
RAM=512
VERSION=latest
```

* **`TYPE=site`**: Identifies the app as a web service.
* **`ID`**: Your registered subdomain name. **Do not** include `.discloud.app` (e.g., use `my-app`, not `my-app.discloud.app`).
* **`MAIN`**: The entry point of your application.
* **`RAM`**: Allocated memory (min. 512MB for sites).
{% endstep %}

{% step %}
#### 🏗️ Handling Build Processes

If your application requires a build step (like React, Next.js, or TypeScript), you have two options:

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

In this case, ensure your `MAIN` or `START` points to the correct entry point within your build folder.
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
* ⌨️ [**CLI**](../how-to-host-using/cli.md) (`discloud up`)
* 🟦 [**VS Code Extension**](../how-to-host-using/visual-studio-code.md)
* 🤖 [**Discord Bot**](../how-to-host-using/discord-bot.md)
* 🐙 [**GitHub Integration**](../api-and-integrations/github-integration.md)
{% endstep %}
{% endstepper %}
