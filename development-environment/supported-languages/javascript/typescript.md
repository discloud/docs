---
hiddenn: true
description: Complete guide to host TypeScript applications on Discloud.
hidden: true
---

# TypeScript

## 📁 Preparing the Files

Before uploading your project, you must exclude unnecessary files to optimize the deployment.

#### ❌ Files to Exclude

Ensure the following files and directories are not included in your [`.zip`](../../../faq/general-questions/wip-how-to-compress.md):

```diff
- package-lock.json
- node_modules/
- .cache/
- .git/
```

📌 Use a [`.discloudignore`](../../../configurations/.discloudignore.md) file to automatically exclude these files.

🔗 Need help setting up your [`package.json`](package.json.md) or finding the [main file](../../../faq/general-questions/what-is-the-main-file.md)?

<details>

<summary>📦 About the dist folder (TypeScript: bot and site)</summary>

{% hint style="info" %}
For TypeScript apps, the `dist/` folder is reserved for Discloud's BUILD output on both `TYPE=bot` and `TYPE=site`. If you set `BUILD=...` in your [`discloud.config`](https://github.com/discloud/docs/blob/english/configurations/discloud.config), Discloud generates the `dist/` folder for you. Do not compress `dist/` or upload files into it.
{% endhint %}

**⚙️ Automatic build (recommended)**

1. Add `BUILD` in `discloud.config` (e.g., `BUILD=npm run build`).
2. Configure `tsconfig.json` to output to `dist/` and add scripts to `package.json`.
3. We run `BUILD` before `START` and your app runs from `dist/`.

Example `discloud.config` (bot):

```properties
TYPE=bot
MAIN=dist/index.js
BUILD=npm run build
START=npm run start
RAM=100
VERSION=latest
ID=my-ts-bot
```

Example `discloud.config` (site):

```properties
TYPE=site
ID=mysite
MAIN=dist/server.js
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
```

**👜 Pre-built**

1. Produce output in `build/` (do not use `dist/`).
2. Omit `BUILD` from `discloud.config`.
3. Point `MAIN` to the `build/` folder entry file.

Example (bot):

```properties
TYPE=bot
MAIN=build/index.js
RAM=100
VERSION=latest
ID=my-ts-bot
```

Example (site):

```properties
TYPE=site
ID=mysite
MAIN=build/server.js
RAM=512
VERSION=latest
```

</details>

***

## ⚙️ Project Setup for TypeScript

You will typically compile TypeScript to JavaScript with `tsc` and run the compiled files.

### package.json (scripts)

```json
{
  "name": "my-ts-app",
  "version": "1.0.0",
  "main": "dist/index.js",
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js"
  },
  "dependencies": {},
  "devDependencies": {
    "typescript": "^5.6.0"
  }
}
```

### tsconfig.json (minimal)

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "outDir": "dist",
    "rootDir": "src",
    "esModuleInterop": true,
    "strict": true
  },
  "include": ["src"]
}
```

{% hint style="info" %}
Discloud installs dependencies defined in your project. Ensure `typescript` is present (devDependency is fine) so the `BUILD` step can run `tsc`.
{% endhint %}

***

## 🌐 Hosting Websites & APIs with Express (TypeScript)

Before deploying your website or API on Discloud, ensure you meet the following requirements:

{% hint style="success" %}
[Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](../../../faq/general-questions/how-to-create-a-subdomain.md) before deployment.
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – Applications must listen on this port.
{% endhint %}

### Express (TS) example

```ts
import express from "express";

const app = express();

app.get("/", (_req, res) => {
  res.send("Hello, Discloud from TypeScript!");
});

const PORT = Number(process.env.PORT) || 8080;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

***

## ✍️ Deploying Your Application

Once your project is configured and compressed, you can choose one of the following deployment methods on Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Upload and manage your application via the web interface.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Deploy directly through Discloud’s Discord bot commands.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integrate with VS Code for seamless project management.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use the command-line interface for quick and efficient deployment.</td><td></td><td></td><td></td></tr></tbody></table>

***

## 🔎 Quick recap of TypeScript specifics on Discloud

* `dist/` is reserved for Discloud builds on both `TYPE=bot` and `TYPE=site`.
* If you pre-build locally, output to `build/` and point `MAIN` to `build/...`.
* For TypeScript, always provide `BUILD` and `START` in `discloud.config` when shipping sources; `MAIN` should point to the runtime JS entry (usually `dist/index.js`).
* For websites/APIs, your server must listen on port `8080`.
