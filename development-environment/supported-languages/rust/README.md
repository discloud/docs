---
description: Complete guide to host Rust applications on Discloud.
icon: rust
---

# Rust

## 📁 **Preparing the Files**

Before uploading your project, you must **exclude unnecessary files** to optimize the deployment.

#### ❌ **Files to Exclude**

Ensure the following files and directories are **not** included in your [`.zip`](../../../faq/general-questions/wip-how-to-compress.md):

```diff
- Cargo.lock
- target/
- git
```

📌 **Use a** [**`.discloudignore`**](../../../configurations/.discloudignore.md) **file** to automatically exclude these files.

🔗 **Need help setting up your** [**`Cargo.toml`**](cargo.toml.md) **or find** [**main file**](../../../faq/general-questions/what-is-the-main-file.md)**?**

***

## 🌐 Hosting Your Site with Rocket

Before deploying your website or API on Discloud, ensure that you meet the following **requirements**:

{% hint style="success" %}
[Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](/broken/pages/tOZppdIRGABWAzzGcvLs) before deployment.
{% endhint %}

{% hint style="success" %}
Use the nightly version of Rust (Rocket requires nightly).
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – Applications must listen on this port.
{% endhint %}

***

## 🚀 Configuring `Rocket`

[Rocket](https://rocket.rs/) is a web framework for Rust that requires the nightly version of Rust. To set up and deploy a Rocket project on Discloud, follow these steps:

{% stepper %}
{% step %}
Set the Nightly Version of Rust.

Run the following command in the terminal to ensure your project is using the nightly version:

```bash
rustup override set nightly
```
{% endstep %}

{% step %}
Create the `rust-toolchain.toml` File.

To make sure the nightly version of Rust is used, create a file named `rust-toolchain.toml` in the project’s root directory with the following content:

{% code title="rust-toolchain.toml" %}
```ini
[toolchain]
channel = "nightly"
```
{% endcode %}

This file tells rustup to use the nightly version of Rust.
{% endstep %}
{% endstepper %}

***

## ✍️ Deploying **Your Application**

Once your project is **configured and compressed**, you can choose one of the following **deployment methods** on Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Upload and manage your application via the web interface.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Deploy directly through Discloud’s Discord bot commands.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integrate with VS Code for seamless project management.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use the command-line interface for quick and efficient deployment.</td><td></td><td></td><td></td></tr></tbody></table>
