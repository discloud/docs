---
description: >-
  How to fix dependency installation and build errors when uploading an
  application to Discloud.
---

# Why won't my dependencies install?

During the deploy, Discloud installs the dependencies listed in your language's dependency file. If that step fails, the application doesn't start. The [logs](../general-questions/how-to-access-the-application-logs.md) show which package failed.

***

## 📄 The dependency file

Check that the right file is in the [project root](../general-questions/what-is-the-root-of-the-project.md) and that it lists everything your code uses:

| Language   | File                                                                                                                    |
| ---------- | ----------------------------------------------------------------------------------------------------------------------- |
| JavaScript | [`package.json`](../../development-environment/supported-languages/javascript/package.json.md)                          |
| Python     | [`requirements.txt`](../../development-environment/supported-languages/python/requirements.txt.md)                      |
| Java       | An already compiled `.jar`. See [how to build it](../general-questions/how-to-build-and-package-a-java-application.md). |

{% hint style="warning" %}
Don't upload folders like `node_modules` or `venv`. Discloud installs the dependencies from the file. Use a [`.discloudignore`](../../configurations/.discloudignore.md) to leave them out.
{% endhint %}

***

## 🔍 Common causes

{% hint style="warning" %}
#### **Package that doesn't exist or has the wrong name**

A typo in the name or a version that doesn't exist makes the install fail. Test locally with `npm install` or `pip install -r requirements.txt` before uploading.
{% endhint %}

{% hint style="warning" %}
#### **Incompatible language version**

Some packages require a minimum Node.js or Python version. Set the right version with the `VERSION` option in [`discloud.config`](../../configurations/discloud.config/). See the [available versions](../../configurations/discloud.config/versions.md).
{% endhint %}

{% hint style="warning" %}
#### **Package that needs system libraries**

Packages like `canvas` or audio and video libraries depend on Linux libraries. Install them with the [`APT`](../../configurations/discloud.config/apt.md) option in `discloud.config`, for example `APT=canvas` or `APT=ffmpeg`.
{% endhint %}

{% hint style="warning" %}
#### **Package that only works on Windows or macOS**

Discloud runs on Linux. Packages made only for another system won't install. Look for a Linux-compatible alternative.
{% endhint %}

{% hint style="warning" %}
#### **Lockfile from another package manager**

An outdated `package-lock.json`, or one generated on another system, can cause conflicts. Generate it again locally or leave it out of the upload.
{% endhint %}

***

## 🛠️ How to test before uploading

{% stepper %}
{% step %}
**Install from scratch**

Delete `node_modules` or the virtual environment and install again, only from the dependency file.
{% endstep %}

{% step %}
**Run the application**

Start the application locally with the same command Discloud will use.
{% endstep %}

{% step %}
**Upload again**

If it worked locally, upload again and follow the [logs](../general-questions/how-to-access-the-application-logs.md) during the deploy.
{% endstep %}
{% endstepper %}

***

## ❓ Still need help?

See [**Troubleshooting Solutions**](./) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
