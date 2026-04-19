---
description: Practical guide to host Next.js applications on Discloud.
icon: 'n'
---

# Next.js

## 🧭 Introduction

This step-by-step guide shows how to prepare, configure, and deploy a **Next.js** application on Discloud.

There are two main approaches:

* [**Option A (recommended)**](nextjs.md#option-a-deploy-without-custom-server-next.js-built-in) – use `next build` + `next start` **without a custom server** (only the built-in Next.js server).
* [**Option B**](nextjs.md#option-b-custom-server-with-express) – use a **custom server** with **Express**, useful when you need **extra routes, custom middleware, or specific integrations**.

Additionally, we show an [**alternative with static export**](nextjs.md#alternative-static-export-next.js-as-a-static-site), ideal for purely static websites.

{% hint style="info" %}
This guide assumes you already have a Next.js project running locally.
{% endhint %}

***

## 📋 Requirements

{% hint style="success" %}
A [Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](../../faq/general-questions/how-to-create-a-subdomain.md) before deployment.
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – applications must listen on this port.
{% endhint %}

***

## 🧱 Local prerequisites

Before continuing, you will need:

* **Node.js** installed on your machine.
* A **Next.js project** created (e.g. `npx create-next-app`).
* A **Discloud account** with a **configured subdomain**.
* Optionally: **Git**, **VSCode**, and/or the **Discloud CLI** to make the workflow easier.

If you are not yet familiar with the local environment, check:

{% content-ref url="../../development-environment/local-environment/nodejs.md" %}
[nodejs.md](../../development-environment/local-environment/nodejs.md)
{% endcontent-ref %}

***

## 🧹 Preparing project files

Before compressing your project into a `.zip`, create a [**`.discloudignore`**](../../configurations/.discloudignore.md) file in the project root to exclude unnecessary files and folders from the upload:

```
node_modules/
dist/
.next/
.env
.env.local
.git
package-lock.json
```

{% hint style="info" %}
The `.discloudignore` file works similarly to `.gitignore`, but it is used by Discloud to ignore files at upload time.
{% endhint %}

***

## 📦 `package.json` – recommended scripts

Inside your [`package.json`](../../development-environment/supported-languages/javascript/package.json.md), make sure the main Next.js scripts are defined. A basic example:

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start -p 8080",
    "export": "next export"
  }
}
```

{% hint style="danger" %}
It is important that the **`start` script uses port `8080`** (`next start -p 8080`), as this is the default port required by Discloud for websites.
{% endhint %}

***

## 📦 Changing Next.js build folder (`.next` → `dist`)

By default, Next.js outputs build files into the `.next` directory.\
In some cases (deployment, conventions, integrations), you may want to use a folder like `dist` instead.

#### 1. Edit `next.config.js`

```js
const nextConfig = {
  distDir: 'dist',
}
```

#### 2. Run the build

```bash
npm run build
```

#### 📁 Result

Before:

```
.next/
```

After:

```
dist/
```

***

### 📦 TypeScript requirement (important)

If your project uses TypeScript, make sure it is installed under `dependencies` instead of `devDependencies`.

Some deployment environments only install production dependencies, which can cause build failures if TypeScript is missing.

#### ✅ Correct example

```json
{
  "dependencies": {
    "typescript": "^5.0.0"
  }
}
```

#### ❌ Incorrect example

```json
{
  "devDependencies": {
    "typescript": "^5.0.0"
  }
}
```

***

<details open>

<summary>✅  Deploy without custom server (Next.js "built-in")</summary>

In this option you only use the internal Next server (`next start`), without needing a `server.js`.

**🔁 Basic flow**

1.  Run the build locally (optional but recommended):

    ```bash
    npm run build
    ```
2.  Test locally:

    ```bash
    npm run start
    ```
3. If everything works, prepare the `.zip` and upload it to Discloud.

**⚙️** [**`discloud.config`**](../../configurations/discloud.config/) **(example)**

```
MAIN=index.ts
TYPE=site
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
ID=my-nextjs-app
```

</details>

<details>

<summary>🧾 Alternative – Static export (Next.js as a static site)</summary>

If your project does not depend on **SSR** or **API Routes**, you can use `next export` to generate a fully **static** site.

**📦** [**`package.json`**](../../development-environment/supported-languages/javascript/package.json.md) **(static export)**

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build && next export",
    "start": "npx serve -s out -l 8080"
  }
}
```

**⚙️** [**`discloud.config`**](../../configurations/discloud.config/) **(static)**

```
MAIN=out/index.html
TYPE=site
BUILD=npm run build
START=npm run start
RAM=256
ID=my-static-site
```

{% hint style="success" %}
Static sites usually consume **less RAM** and are ideal for blogs, landing pages, and simple documentation.
{% endhint %}

</details>

***

## 🔐 Environment variables

In Next.js, public environment variables must start with `NEXT_PUBLIC_`.

* Define variables via the **Discloud Dashboard**, **CLI**, or **API**.
* Everything that starts with `NEXT_PUBLIC_` is embedded into the bundle during the **build**.

Example:

```env
NEXT_PUBLIC_API_URL=https://my-backend.discloud.app
API_SECRET_TOKEN=do-not-put-in-frontend
```

Using in components:

```js
const apiUrl = process.env.NEXT_PUBLIC_API_URL;
```

***

## 🗂️ Recommended final project structure

A typical Next.js project structure for Discloud might look like:

```
my-next-app/
├─ discloud.config
├─ .discloudignore
├─ package.json
├─ next.config.js
├─ index.ts
├─ server.js        # optional (only in Option B)
├─ public/
└─ app/ or pages/
	 ├─ page.js
	 └─ api/
			└─ hello.js
```

***

## 🚀 Deploying to Discloud

You can deploy your Next.js app using any of the supported methods.

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

|                                    |                                                                                                                                                                                              |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **App does not open / wrong port** | Check if Next is using port `8080` (`next start -p 8080` or `PORT=8080`).                                                                                                                    |
| **Plan / permission error**        | Confirm that your account has the **correct plan** for websites/APIs.                                                                                                                        |
| **Subdomain not configured**       | Make sure you followed the **subdomain guide** before deploying.                                                                                                                             |
| **Build errors**                   | <ul><li>Run locally: <code>npm run build</code> and fix any errors before uploading.</li><li>Check that all <strong>dependencies</strong> are listed in <code>package.json</code>.</li></ul> |
| **Errors when starting (`START`)** | <ul><li>Verify that the <code>start</code> script is correct.</li><li>Follow the <strong>Discloud logs</strong> to see the exact error message.</li></ul>                                    |
