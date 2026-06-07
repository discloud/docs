---
description: Complete guide to host JavaScript applications on Discloud.
icon: square-js
---

# Javascript

## 📁 **Preparing the Files**

Before uploading your project, you must **exclude unnecessary files** to optimize the deployment.

#### ❌ **Files to Exclude**

Ensure the following files and directories are **not** included in your [`.zip`](../../../faq/general-questions/wip-how-to-compress.md):

```diff
- package-lock.json
- node_modules/
- .cache/
- .git/
```

📌 **Use a** [**`.discloudignore`**](../../../configurations/.discloudignore.md) **file** to automatically exclude these files.

🔗 **Need help setting up your** [**`package.json`**](package.json.md) **or find** [**main file**](../../../faq/general-questions/what-is-the-main-file.md)**?**

<details>

<summary>📦 About the dist folder (TYPE=site only)</summary>

{% hint style="info" %}
For apps with `TYPE=site`, the `dist/` folder is reserved for BUILD output. If you set `BUILD=...` in your [`discloud.config`](../../../configurations/discloud.config/), we generate the `dist/` folder for you. Do not compress `dist/` or upload files into it.
{% endhint %}

#### ⚙️ Automatic build

1. Add `BUILD` in `discloud.config` (e.g., `BUILD=npm run build`).
2. Your build script outputs files to `dist/` (Vite, Vue, etc. already do this).
3. We run `BUILD` before `START` and serve the `dist/` folder.

Example:

```properties
TYPE=site
MAIN=server/index.js
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
ID=mysite
```

#### 👜 Pre-built

1. Produce output in `build/` (do not use `dist/`).
2. Omit `BUILD` from `discloud.config`.
3. Point `MAIN` to the `build/` folder.

Example:

```properties
TYPE=site
MAIN=build/server.js
RAM=512
VERSION=latest
ID=mysite
```

</details>

***

### 🌐 **Hosting Websites & APIs with Express**

Before deploying your website or API on Discloud, ensure that you meet the following **requirements**:

{% hint style="success" %}
[Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](../../../faq/general-questions/how-to-create-a-subdomain.md) before deployment.
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – Applications must listen on this port.
{% endhint %}

### ⚙️ **Configuring Express**

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
    res.send("Hello, Discloud!");
});

const PORT = process.env.PORT || 8080;
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

***

## ✍️ Deploying **Your Application**

Once your project is **configured and compressed**, you can choose one of the following **deployment methods** on Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Upload and manage your application via the web interface.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Deploy directly through Discloud’s Discord bot commands.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integrate with VS Code for seamless project management.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use the command-line interface for quick and efficient deployment.</td><td></td><td></td><td></td></tr></tbody></table>
