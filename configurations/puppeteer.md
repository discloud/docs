---
description: >-
  Learn how to configure Puppeteer on Discloud, including dependencies and RAM
  adjustments, to ensure proper operation in container environments.
icon: toolbox
---

# Puppeteer

## 📌 **Requirements**

To use **Puppeteer** on Discloud, a minimum of **512 MB RAM** is recommended for basic tasks. However, depending on the complexity of your application, **more RAM** may be required.

{% hint style="warning" %}
**If Puppeteer does not function correctly (e.g., no QR code in logs, crashes), increase the allocated RAM!**
{% endhint %}

***

## 📦 **Adding Puppeteer**

Puppeteer requires additional system dependencies. You must add **`puppeteer`** to the [`APT`](discloud.config/apt.md) field in your [**`discloud.config`**](discloud.config/) file.

<pre class="language-ini" data-title="discloud.config"><code class="lang-ini"><a data-footnote-ref href="#user-content-fn-1"># ...</a>
APT=tools, puppeteer
# ...
</code></pre>

***

## ⚙️ **Configuring Puppeteer**

Since **Puppeteer runs in a containerized environment**, you must add the `--no-sandbox` argument to ensure it works correctly.

```javascript
const puppeteer = require("puppeteer");

(async () => {
    const browser = await puppeteer.launch({
        args: ["--no-sandbox"]
    });

    const page = await browser.newPage();
    await page.goto("https://example.com");

    console.log(await page.title());
    await browser.close();
})();
```

{% hint style="info" %}
#### **Why `--no-sandbox`?**

Running Puppeteer inside a container **requires disabling the sandbox** to prevent security restrictions from blocking execution.
{% endhint %}

***

## ⚙️ **Using Puppeteer with `whatsapp-web.js`**

Since [**`whatsapp-web.js`**](https://wwebjs.dev/) also uses **Puppeteer** for QR code generation and background interactions, you must **include `--no-sandbox`** in its configuration.

```javascript
const { Client } = require("whatsapp-web.js");

const client = new Client({
    puppeteer: {
        args: ["--no-sandbox"],
    }
});

client.initialize();
```

{% hint style="info" %}
#### **Troubleshooting QR Code Issues:**

* If the **QR code does not appear** in Discloud logs, **increase the allocated RAM**.
* The more complex your interactions with WhatsApp, **the more RAM Puppeteer will need** to function properly.
{% endhint %}

[^1]: **Note:** The **`...`** only indicate the continuation of other previous or subsequent options that are not relevant to mention on this page.
