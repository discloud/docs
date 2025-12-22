---
description: How to host your application via the Discloud extension in Visual Studio Code.
icon: plug
---

# Visual Studio Code

The [**Discloud VSCode Extension**](https://marketplace.visualstudio.com/items?itemName=discloud.discloud) allows you to **deploy and manage your applications** directly from [**Visual Studio Code**](https://code.visualstudio.com/), eliminating the need to use a web dashboard or Discord bot commands.

***

## 🛠️ Installing the Discloud Extension

{% stepper %}
{% step %}
Open VSCode on your computer.
{% endstep %}

{% step %}
Go to the Extensions Tab (`Ctrl + Shift + X`).

* In the search bar, type: **"Discloud"** then click **"Install"**.
{% endstep %}
{% endstepper %}

***

## 🔑 Logging into Discloud

Before deploying, you need to log into your **Discloud account.**

{% stepper %}
{% step %}
Click on the **Discloud Extension Tab** in the **VSCode sidebar**.
{% endstep %}

{% step %}
Click **"Submit your Discloud token"** and enter your [**Discloud API Token**](../faq/general-questions/how-can-i-get-my-discloud-api-token.md).

<figure><img src="../.gitbook/assets/VSCode-Extension_Login.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
Once logged in, your **Discloud applications** will appear inside the extension tab.
{% endstep %}
{% endstepper %}

***

## 🚀 Deploying Your Application

With the **VSCode Extension**, you can deploy your app in just a few clicks!

{% stepper %}
{% step %}
Preparing your project.

* Ensure your project contains all required files:
  * [**`discloud.config`**](../configurations/discloud.config/) (configuration file).
  * Necessary **dependencies** for your programming language (e.g., `package.json` for Node.js, `requirements.txt` for Python).
* **Check the** [**Languages Guide**](../development-environment/supported-languages/) to make sure your project is properly structured.
{% endstep %}

{% step %}
Uploading your application.

<figure><img src="../.gitbook/assets/VSCode-Extension_Upload.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

***

## 📌 Tips & Tricks

### 📂 **Using `.discloudignore` to Exclude Files**

If you want to **exclude certain files or directories** from being uploaded, you can create a [`.discloudignore`](../configurations/.discloudignore.md) file in the root of your project.

***

## **❓ Still need help?**

Check the [**FAQ Section**](/broken/pages/XnfTZsmKo9RRBUwNSPYU) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
