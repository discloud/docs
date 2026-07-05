---
description: Complete guide to host Java applications on Discloud.
icon: java
---

# Java

## 📁 **Preparing Your Project Files**

Before deploying, **your project must be** [**compiled into an executable JAR file**](../../faq/general-questions/how-to-build-and-package-a-java-application.md). When compressing your project, ensure that **the `.jar` file is placed at the** [**root**](../../faq/general-questions/what-is-the-root-of-the-project.md) **of the** [**`.zip`**](../../faq/general-questions/wip-how-to-compress.md) **archive.**

#### ❌ **Files to Exclude**

Ensure the following files and directories are **not** included in your [`.zip`](../../faq/general-questions/wip-how-to-compress.md):

```diff
- package-lock.json
- node_modules/
- .cache/
- .git/
```

📌 **Use a** [**`.discloudignore`**](../../configurations/.discloudignore.md) **file** to automatically exclude these files.

🔗 **Need help with compilation?** Check the FAQ on [**How to Build and Package a Java Application?**](../../faq/general-questions/how-to-build-and-package-a-java-application.md)

***

## 📦 **Compiling Your Java Application**

To **deploy your Java application**, it must be compiled into an **executable JAR file**.

{% tabs %}
{% tab title="Maven" %}
📄 **Maven Official Documentation** → [https://maven.apache.org/guides/index.html](https://maven.apache.org/guides/index.html)

```bash
mvn clean package
```
{% endtab %}

{% tab title="Gradle" %}
📄 **Gradle Official Documentation** → [https://docs.gradle.org/current/userguide/userguide.html](https://docs.gradle.org/current/userguide/userguide.html)

```bash
gradle clean build
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### **Recommendation**

Rename your JAR file to a simple name like `app.jar` to avoid issues with special characters.​
{% endhint %}

***

## 📝 **Setting the Main File**

The `MAIN` parameter in your [`discloud.config`](https://github.com/discloud/docs/blob/english/configurations/discloud.config) file should point to your executable JAR file. For example:

```ini
MAIN=app.jar
```

Ensure that `app.jar` matches the name of your compiled JAR file.​

**Note:** For detailed information on setting the main file, refer to Discloud's FAQ on the main file.

***

## ✍️ **Deploying Your Applicaton**

Once your project is **configured and compressed**, you can choose one of the following **deployment methods** on Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Upload and manage your application via the web interface.</td><td></td><td></td><td></td></tr><tr><td><a href="../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Deploy directly through Discloud’s Discord bot commands.</td><td></td><td></td><td></td></tr><tr><td><a href="../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integrate with VS Code for seamless project management.</td><td></td><td></td><td></td></tr><tr><td><a href="../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use the command-line interface for quick and efficient deployment.</td><td></td><td></td><td></td></tr></tbody></table>
