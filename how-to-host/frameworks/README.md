---
description: Complete guides to host different frameworks on Discloud.
icon: window
---

# Frameworks

## 🎯 Overview

Guides for deploying your favorite frameworks on Discloud. Each one covers what you need to do locally and how to get it running on our platform.

Whether it's a simple API, a full app, or something real-time – you'll find the steps tailored to your framework.

***

## 📚 Available Guides

Pick your framework from the list and follow along:

* **Step-by-step setup** – Project structure, config files, environment variables
* **Local testing** – How to verify everything works before uploading
* **Deployment** – Get your app online and accessible
* **Troubleshooting** – Common issues and how to fix them

***

## 🚀 The basics

1. Pick your framework
2. Follow the guide to set up locally
3. Test the production build
4. Deploy to Discloud

***

## 💡 What's required

No matter what framework you use:

* **Port 8080** – Your app listens here. That's how traffic gets routed.
* **Subdomain** – [Create one following this guide](../../faq/general-questions/how-to-create-a-subdomain.md).
* **`discloud.config`** – Goes in your project root. [See the config guide](https://github.com/discloud/docs/blob/english/configurations/discloud.config).
* **Dependencies file** – `package.json`, `requirements.txt`, whatever your framework uses.

***

## 🔗 Helpful links

* 📖 [Development Environment](../../development-environment/supported-languages/) – Set up Node, Python, etc. locally
* ⚙️ [discloud.config](https://github.com/discloud/docs/blob/english/configurations/discloud.config) – All the config options
* 🚀 [How to deploy](../../how-to-host-using/dashboard.md) – Dashboard, Bot, CLI, or VSCode
* 🌐 [Custom domains](../../api-and-integrations/custom-domain.md) – Use your own domain instead
