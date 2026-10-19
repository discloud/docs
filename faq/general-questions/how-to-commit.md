---
description: >-
  Update the files of an application that is already on Discloud, without
  uploading the whole project again.
---

# How to commit?

A **commit** updates the files of an application that is already hosted on Discloud. Instead of uploading the whole project again, you send only what changed.

***

## 🧩 How a commit works

Discloud uses the **path of each file inside the `.zip`** to decide where it goes in your project, starting from the [project root](what-is-the-root-of-the-project.md):

* If a file already exists at that path, it is **replaced**.
* If it doesn't, a **new** file is created.
* Files you didn't send **stay as they are**.

<figure><img src="../../.gitbook/assets/commit-flow.png" alt="A .zip with src/commands/ping.js updates only that file in the application"><figcaption><p>Only <code>ping.js</code> is sent; the rest of the project doesn't change.</p></figcaption></figure>

{% hint style="warning" %}
**Uppercase and lowercase matter.** Discloud runs on Linux, where `commands` and `Commands` are different folders. The same goes for files: `config.json` and `Config.json` are not the same file.
{% endhint %}

***

## 📦 Preparing the `.zip`

{% stepper %}
{% step %}
**Find the file's path.**

Check where the file is in your project, starting from the root. For example: `src/commands/ping.js`.
{% endstep %}

{% step %}
**Recreate the same folders.**

Put the file inside the same folders, with the same names and the same extension:

```
update.zip
└── src/
    └── commands/
        └── ping.js
```
{% endstep %}

{% step %}
**Compress the contents, not the project folder.**

Select the folders and files that changed and compress them. If you compress the whole project folder (for example, `my-bot/`), it becomes part of the path and the files end up in the wrong place.
{% endstep %}

{% step %}
**Check before sending.**

Open the `.zip`: the first thing inside it should be `src/`, not `my-bot/`.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Use [`.discloudignore`](../../configurations/.discloudignore.md) to keep unnecessary files out of your commits.
{% endhint %}

***

## ⚠️ Common mistakes

Imagine the original file is at `src/commands/ping.js`:

<table><thead><tr><th width="260">You sent</th><th>What happens</th></tr></thead><tbody><tr><td>✅ <code>src/commands/ping.js</code></td><td>The original file is updated.</td></tr><tr><td>❌ <code>src/Commands/ping.js</code></td><td>A new <code>Commands/</code> folder is created next to <code>commands/</code>. The bot keeps using the old file.</td></tr><tr><td>❌ <code>my-bot/src/commands/ping.js</code></td><td>A <code>my-bot/</code> folder is created inside the project, with a copy of the file. The original doesn't change.</td></tr><tr><td>❌ <code>ping.js</code></td><td>A <code>ping.js</code> is created at the project root. <code>src/commands/ping.js</code> doesn't change.</td></tr></tbody></table>

{% hint style="info" %}
If the commit had no effect, look for a duplicated folder like the ones in the table. Usually the file went to the wrong path.
{% endhint %}

***

## 🚀 Sending the commit

{% tabs %}
{% tab title="🤖 Discord Bot" %}
{% stepper %}
{% step %}
Go to the [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) channel on the **Discloud Discord Server**.
{% endstep %}

{% step %}
Run the command:

```
.commit
```

The short form `.c` also works.
{% endstep %}

{% step %}
Send your `.zip` when the bot asks for it.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="⌨️ CLI" %}
From the project root, run:

```bash
discloud app commit <APPLICATION_ID>
```

The [CLI](../../how-to-host-using/cli.md) builds the `.zip` for you from the current folder, so run the command from the project root. The short form `discloud app c` also works.
{% endtab %}

{% tab title="🟦 VS Code" %}
{% stepper %}
{% step %}
In the VS Code file explorer, select the files and folders that changed.
{% endstep %}

{% step %}
Right-click and choose **Discloud > Commit**.
{% endstep %}

{% step %}
Choose the application that will receive the commit.
{% endstep %}
{% endstepper %}

See how to install and sign in to the [VS Code extension](../../how-to-host-using/visual-studio-code.md).
{% endtab %}

{% tab title="🐙 GitHub" %}
With the [GitHub Integration](../../api-and-integrations/github-integration.md), your application is updated from your repository, with no `.zip` to build.
{% endtab %}
{% endtabs %}

***

## ✅ Before sending, check

* The path is the same as in the project, starting from the root.
* Folder and file names are identical, with the same uppercase and lowercase letters.
* The extension is right (`ping.js`, not `ping.js.txt`).
* The `.zip` starts directly with the project folders, with no project folder around them.

***

## ❓ Still need help?

See [**Troubleshooting Solutions**](../troubleshooting-solutions/) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
