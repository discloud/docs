---
description: >-
  Learn how to create your project's .zip file the right way before uploading it
  to Discloud.
---

# How to compress?

To upload an application to Discloud, you need a **`.zip`** file with your project. What matters most is **what's inside it**: when you open the `.zip`, your project files should be right there, with no extra folder around them.

***

## 📂 What goes inside the `.zip`

The `.zip` must start directly at the [project root](what-is-the-root-of-the-project.md), where your `discloud.config` and [main file](what-is-the-main-file.md) are.

{% tabs %}
{% tab title="✅ Correct" %}
```
my-bot.zip
├── discloud.config
├── package.json
└── src/
    └── index.js
```

When you open the `.zip`, the project files are right at the first level.
{% endtab %}

{% tab title="❌ Incorrect" %}
```
my-bot.zip
└── my-bot/
    ├── discloud.config
    ├── package.json
    └── src/
        └── index.js
```

The `my-bot/` folder ended up around everything. Because of it, `discloud.config` and the main file are not at the root of the `.zip`.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Compress the folder's contents, not the folder.** Open your project folder, select the files and folders inside it, and compress them. If you compress the whole project folder, it becomes part of the `.zip` and the entire project ends up one level down.
{% endhint %}

***

## 🗑️ What to leave out

Don't send files that aren't needed to run the application. This keeps the upload smaller and faster.

```diff
- node_modules
- venv
- .git
- .DS_Store
- __pycache__
```

{% hint style="info" %}
Use a [`.discloudignore`](../../configurations/.discloudignore.md) file to list the files and folders that should be left out of your uploads.
{% endhint %}

***

## 🛠️ How to create the `.zip`

{% tabs %}
{% tab title="🪟 Windows" %}
{% stepper %}
{% step %}
Open your project folder and select all of its contents (`Ctrl` + `A`).
{% endstep %}

{% step %}
Right-click the selection and choose **Compress to ZIP file** (Windows 11) or **Send to > Compressed (zipped) folder** (Windows 10).
{% endstep %}

{% step %}
Name the file, for example `my-bot.zip`.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🍎 macOS" %}
{% stepper %}
{% step %}
Open your project folder in Finder and select all of its contents (`Cmd` + `A`).
{% endstep %}

{% step %}
Right-click the selection and choose **Compress**.
{% endstep %}

{% step %}
macOS creates an `Archive.zip` file. Rename it if you like, for example `my-bot.zip`.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🐧 Linux" %}
In a terminal, inside your project folder, run:

```bash
zip -r ../my-bot.zip . -x "node_modules/*" ".git/*"
```

The `.zip` is created in the parent folder, with the project contents right at its root. Use `-x` to leave out any other folders that don't need to be uploaded.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Always upload a **`.zip`** file. Other formats, such as `.rar` or `.7z`, are not accepted.
{% endhint %}

***

## 🔄 Updating an application

To change only a few files of an application that's already on Discloud, you don't need to upload the whole project again. See [**How to commit?**](how-to-commit.md).

***

## ❓ Still need help?

See [**Troubleshooting Solutions**](../troubleshooting-solutions/) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
