---
description: Connect your GitHub repository to Discloud and deploy directly from your code.
icon: github
---

# GitHub Integration

### 🧭 Overview

The **GitHub Integration** allows you to deploy applications directly from a GitHub repository to Discloud, no manual ZIP uploads required. Discloud pulls the code from your repository, reads the [`discloud.config`](https://github.com/discloud/docs/blob/english/configurations/discloud.config) at the root, and builds and starts your application automatically.

This is the recommended workflow for teams and anyone using version control as part of their development process.

***

### ✅ Prerequisites

Before connecting GitHub, make sure the following are in place:

{% hint style="success" %}
[**`discloud.config`**](https://github.com/discloud/docs/blob/english/configurations/discloud.config) **at the root** - This file must exist at the root of your repository. Without it, the upload will fail validation. Learn more about the root of the project.
{% endhint %}

{% hint style="danger" %}
**Never commit** [**`.env`**](../faq/general-questions/.env-file.md) **files** - Your `.env` file must be listed in `.gitignore`. Production secrets are set directly in Discloud during the upload step, not through the repository.
{% endhint %}

***

### 🔗 Connect your GitHub account

{% stepper %}
{% step %}
**🔑 Open the GitHub Integration tab**

Go to the [Discloud Dashboard](https://discloud.com/dashboard) and open the **GitHub Integration** tab.

Click **Login** and authorize Discloud via GitHub OAuth. This allows Discloud to read your repositories.

<figure><img src="../.gitbook/assets/GitHub-Integration_Login.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**⚙️ Configure repository access**

After authorizing, click **Configure** on the GitHub Integration page. GitHub will ask you to choose which repositories Discloud can access:

* 🔓 **All repositories** - Discloud can access every repository in your account
* 🔒 **Selected repositories** - Choose only the specific repositories you want to deploy

{% hint style="info" %}
You can change this at any time by returning to the **GitHub Integration** tab and clicking **Configure** again, or by managing the Discloud GitHub App directly from your GitHub account settings.
{% endhint %}
{% endstep %}
{% endstepper %}

***

### 🚀 Deploy from GitHub

{% stepper %}
{% step %}
**🚀 Start a new upload**

Go to the [Discloud Dashboard](https://discloud.com/dashboard), click **+ Upload** in the top-right corner, and select **GitHub** from the menu.

<figure><img src="../.gitbook/assets/GitHub-Integration_Upload-Menu.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**🛠️ Configure your deployment**

**Repository & branch** - Choose the repository and the branch you want to deploy from. Discloud will pull the latest commit from that branch.

**Environment variables** - Add your production secrets here as `KEY=VALUE` pairs, one per line.

<figure><img src="../.gitbook/assets/GitHub-Integration_Repository-Select.png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
**This is the only place to set production secrets.** `.env` files must not be committed to GitHub. Discloud stores these values securely and generates a `.env` file at the root of your application at runtime, keeping them out of your repository entirely.
{% endhint %}

{% hint style="warning" %}
If you forget to add a variable here, your application will start without it and may crash or behave incorrectly. To update environment variables later, you can edit them directly in the dashboard if you have a [paid plan](https://discloud.com/plans). Otherwise, you will need to do a new commit manually upload with the complete updated `.env` content.
{% endhint %}
{% endstep %}

{% step %}
**✅ Confirm and deploy**

Review your settings and click **Upload**. Discloud will:

1. Pull the code from your selected repository and branch
2. Validate your `discloud.config`
3. Install dependencies and run the build command (if configured)
4. Start your application

<figure><img src="../.gitbook/assets/GitHub-Integration_Upload.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

***

### 🔁 Updating your application

Discloud automatically redeploys your application whenever you push new commits to the branch configured during the initial upload. No manual action is required.
