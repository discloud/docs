---
description: Learn how to host your JavaScript bot on the DisCloud
---

# 📦 JavaScript

## :file\_folder: Files

**Do not send all the files** at once, you need to put only the necessary files from your bot into a `.zip` file.

```diff
Minimum Files Required
+ Main File (Example: index.js, bot.js...)
+ File package.json
+ Other (If your bot depends on other files it should include)
Not Required
- Folder node_modules
- File package-lock.json
- Folder .git
- File LICENSE
```

> * Have trouble finding your main file? [Click here](../../faq/arquivo-principal.md#arquivos-principais-gerais)
> * Doubts about creating your `package.json` file? [Click here](package.json.md)

{% content-ref url="package.json.md" %}
[package.json.md](package.json.md)
{% endcontent-ref %}

### :compression: Compressing the Files

Select only the necessary files as mentioned above and create your `.zip`

![](<../../../.gitbook/assets/image (36).png>)

For more details on how to **Compress your Files** according to your **Operating System**, you can see below:

{% content-ref url="../../faq/zip.md" %}
[zip.md](../../faq/zip.md)
{% endcontent-ref %}

## ✍ Hosting your bot

{% hint style="info" %}
Choose the method for hosting your bot in the Discloud:
{% endhint %}

{% content-ref url="../../host/bots/via-dashboard.md" %}
[via-dashboard.md](../../host/bots/via-dashboard.md)
{% endcontent-ref %}

{% content-ref url="../../host/bots/discord.md" %}
[discord.md](../../host/bots/discord.md)
{% endcontent-ref %}

## :earth\_americas: Hosting Your Site

{% hint style="info" %}
This feature needs some basic requirements to be able to be used, please check the requirements [here](../../host/sites/#requirements) before continuing
{% endhint %}

Using Express

**Express** is a widely used framework for building Web sites and APIs.

By default **Express** is configured to listen to port `3000`, you need to configure it to listen to port `8080`, look for the following line usually found in your [main file](../../faq/arquivo-principal.md).

```javascript
app.listen(8080);
```

