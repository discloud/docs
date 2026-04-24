---
description: Practical guide to hosting Vite applications on Discloud.
icon: bolt
---

# Vite

## 🧭 Introduction

This step-by-step guide shows you how to prepare, configure, and deploy a **Vite** application on Discloud.

The process involves compiling your project to the `dist` folder and serving the static files using `vite preview` on port `8080`. Vite is known for its build speed and native support for multiple frameworks and syntaxes, including **React (JSX/TSX)**, **Vue**, **Svelte**, **Solid**, and **Preact**.

***

## 📋 Requirements

{% hint style="success" %}
[Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](../../faq/general-questions/how-to-create-a-subdomain.md) before deploying.
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – Applications must listen on this port.
{% endhint %}

***

## 🧱 Local prerequisites

Before continuing, you will need:

* **Node.js** installed on your machine.
* A **Vite project** created (e.g.: `npm create vite@latest my-app`).
* A **Discloud account** with a **subdomain configured**.
* Optionally: **Git**, **VSCode** and/or the **Discloud CLI** to ease the workflow.

If you're not yet familiar with the environment, check out:

{% content-ref url="../../development-environment/local-environment/nodejs.md" %}
[nodejs.md](../../development-environment/local-environment/nodejs.md)
{% endcontent-ref %}

***

## 🧹 Preparing project files

Before compressing your project into a `.zip`, create a [**`.discloudignore`**](../../configurations/.discloudignore.md) file at the project root to exclude unnecessary files and folders from the upload:

```
node_modules/
dist/
.git
.vscode/
package-lock.json
```

{% hint style="info" %}
The `.discloudignore` file works similarly to `.gitignore`, but is used by Discloud to ignore files at upload time.
{% endhint %}

***

## 📦 `package.json` – recommended scripts

Inside your [`package.json`](../../development-environment/supported-languages/javascript/package.json.md), make sure the build and preview scripts are correctly defined:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview --port 8080 --host"
  }
}
```

{% hint style="info" %}
* `build` – compiles the project to the `dist` folder.
* `preview` – serves the compiled files on port `8080`. On Discloud, the site is automatically available via your subdomain.
* `--host` – exposes the server on the machine's IP, allowing access from other devices on the same network during local testing. You can omit this if you don't need it.
* `dev` – runs in local development mode on port `5173` by default (not needed for Discloud).
{% endhint %}

***

## ⚙️ `vite.config.ts` – required configuration

For Vite to work correctly on Discloud, you need to configure `allowedHosts` in the config file. This ensures the preview server accepts requests coming from your subdomain or custom domain.

```ts
import { defineConfig } from "vite";

export default defineConfig({
  build: {
    outDir: "dist",
  },
  preview: {
    allowedHosts: [
      "mysubdomain.discloud.app", // your Discloud subdomain
      // "mydomain.com",          // custom domain (if applicable)
    ],
  },
});
```

{% hint style="warning" %}
Replace `mysubdomain.discloud.app` with the actual subdomain registered in the Discloud panel. If you have a custom domain, add it to the array as well, for example `"mydomain.com"`.
{% endhint %}

{% hint style="danger" %}
If `allowedHosts` is not configured correctly, Vite will reject requests and your application will not open.
{% endhint %}

***

## 📄 Main file (MAIN)

Discloud requires the `MAIN` field to point to a `.ts` file to correctly identify and build the project. This applies to **any framework** — React (`.tsx`), Vue (`.vue`), Svelte (`.svelte`), or any other.

Even if your project uses JSX, TSX, Svelte, or another syntax, **you still need a `.ts` file** in `MAIN`. The `vite.config.ts` is the most natural and recommended choice, since every Vite project typically has this file.

If your project has no `.ts` file at all, create one at the root — it can be a simple file like `entry.ts`, which will only serve to satisfy this requirement.

{% hint style="danger" %}
The `MAIN` field must always point to a `.ts` file. Pointing to a `.tsx`, `.vue`, `.svelte`, or `.jsx` is not supported.
{% endhint %}

***

## ⚙️ `discloud.config` – example

Here is a typical configuration for a Vite application:

```
MAIN=vite.config.ts
TYPE=site
BUILD=npm run build
START=npm run preview
RAM=512
VERSION=latest
ID=mysubdomain.discloud.app
```

For detailed information about each configuration parameter and all available options, refer to the full guide:

{% content-ref url="../../configurations/discloud.config/" %}
[discloud.config](../../configurations/discloud.config/)
{% endcontent-ref %}

{% hint style="warning" %}
The `ID` field must be your full subdomain, for example `mysubdomain.discloud.app`.
{% endhint %}

***

## 🧪 Testing locally (production build)

Before sending to Discloud, verify that your app compiles and runs correctly:

{% stepper %}
{% step %}
Compile the project locally:

```bash
npm run build
```

This generates the `dist` folder with static files ready for production.
{% endstep %}

{% step %}
Test the production build:

```bash
npm run preview
```

Check if the server starts and responds to requests (e.g.: via `curl http://localhost:8080` or by opening it in the browser).
{% endstep %}

{% step %}
Stop the server and proceed with the deploy.
{% endstep %}
{% endstepper %}

***

## 🔐 Environment variables

If your project needs environment variables, you can include a `.env` file directly in the `.zip` sent to the platform.

{% hint style="warning" %}
Do not add `.env` to `.discloudignore` if you need it to be uploaded with the project.
{% endhint %}

In Vite, public environment variables must start with `VITE_` to be accessible in the client bundle:

```env
VITE_API_URL=https://my-backend.discloud.app
```

Using in components:

```ts
const apiUrl = import.meta.env.VITE_API_URL;
```

{% hint style="danger" %}
Never expose sensitive secrets in the frontend. Only variables prefixed with `VITE_` are accessible in the client bundle — the rest are only available during build time.
{% endhint %}

***

## 🗂️ Recommended final project structure

A typical Vite project structure for Discloud might look like:

```
my-vite-app/
├─ discloud.config
├─ .discloudignore
├─ .env                 # optional, if you need variables
├─ package.json
├─ vite.config.ts
├─ tsconfig.json
├─ index.html
├─ public/
└─ src/
   ├─ main.ts
   ├─ App.vue           # or App.tsx, App.svelte, etc.
   └─ ...
```

***

## 🚀 Deploying on Discloud

You can deploy your Vite app using any of the supported methods.

{% content-ref url="../../how-to-host-using/dashboard.md" %}
[dashboard.md](../../how-to-host-using/dashboard.md)
{% endcontent-ref %}

{% content-ref url="../../how-to-host-using/discord-bot.md" %}
[discord-bot.md](../../how-to-host-using/discord-bot.md)
{% endcontent-ref %}

{% content-ref url="../../how-to-host-using/visual-studio-code.md" %}
[visual-studio-code.md](../../how-to-host-using/visual-studio-code.md)
{% endcontent-ref %}

{% content-ref url="../../how-to-host-using/cli.md" %}
[cli.md](../../how-to-host-using/cli.md)
{% endcontent-ref %}

***

## 🛠️ Troubleshooting (common errors)

|                                          |                                                                                                                                                                                                                    |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **App not opening / wrong port**         | Check that the `preview` script uses `--port 8080` and that `allowedHosts` is configured in `vite.config.ts`.                                                                                                      |
| **Unauthorized host error**              | Confirm that your subdomain (e.g.: `mysubdomain.discloud.app`) is listed in `preview.allowedHosts` in `vite.config.ts`.                                                                                            |
| **`dist` folder not found**              | Check that `build.outDir` is set to `"dist"` in `vite.config.ts` and run `npm run build` locally to confirm.                                                                                                       |
| **Plan / permission error**              | Confirm that your account has the **correct plan** for websites/APIs.                                                                                                                                              |
| **Subdomain not configured**             | Make sure you followed the **subdomain** guide before deploying.                                                                                                                                                   |
| **No `.ts` file in the project**         | Create a `.ts` file at the root (e.g.: `entry.ts`) and point to it in the `MAIN` field of `discloud.config`.                                                                                                       |
| **Build errors**                         | <ul><li>Run locally: `npm run build` and fix any errors before uploading.</li><li>Check that all **dependencies** are listed in `package.json`.</li></ul>                                                          |
| **Startup errors (`START`)**             | <ul><li>Check that the `preview` script is correct in `package.json`.</li><li>Monitor the **Discloud logs** to see the exact error message.</li></ul>                                                              |
