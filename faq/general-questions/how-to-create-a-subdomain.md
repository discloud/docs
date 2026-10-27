---
description: >-
  Learn how to register and manage custom Discloud subdomains for your
  applications.
---

# How to create a subdomain?

## 🌐 What is a Discloud Subdomain?

On **Discloud**, any app that uses a **port** and requires **external access** through it to be accessed is considered a site. This includes bots with dashboards, dashboards, APIs, static and dynamic sites, and many others…

To allow external access to your app, Discloud offers the option to create a **custom subdomain**. This subdomain redirects traffic through the Discloud proxy to **port 8080** of your app, allowing you and users to access your site **securely and reliably**.

### 📡 How it Works

<figure><img src="../../.gitbook/assets/subdomain-flow.png" alt="Discloud subdomain flow"><figcaption></figcaption></figure>

{% hint style="info" %}
#### **`.discloud.app` or `.discloud.dev`?**

Your subdomain ends up on `.discloud.app` or on `.discloud.dev`. You don't choose which: Discloud chooses the domain automatically when the subdomain is created, depending on the demand on each domain. In `discloud.config`, you always use only the subdomain name.
{% endhint %}

***

## ✅ Requirements

To register and use a Discloud subdomain, you must meet the following requirements:

{% hint style="success" %}
[Platinum Plan or Higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
**Port 8080 and host 0.0.0.0** – Your application must listen on port 8080 and host `0.0.0.0` for external traffic
{% endhint %}

{% hint style="success" %}
**Discloud Config** – Your app must include a properly configured [`discloud.config`](../../configurations/discloud.config/) file
{% endhint %}

***

## 🚀 Register Your Subdomain

{% stepper %}
{% step %}
Open the [**Discloud Dashboard**](https://discloud.com/dashboard).
{% endstep %}

{% step %}
Click the `Domains` tab in the side menu of your account page.

<figure><img src="../../.gitbook/assets/dashboard-subdomain-tab.png" alt="Dashboard Subdomain tab"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
Click the `+ Create subdomain` button to create a new subdomain.

<figure><img src="../../.gitbook/assets/dashboard-subdomain-button.png" alt="Add Subdomain button"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
Enter your desired subdomain name (e.g., `myapp`, `dashboard`, `api`).

{% hint style="info" %}
#### **Subdomain naming rules**

* Between **2 and 20 characters**
* Only lowercase letters (a–z), numbers (0–9), and hyphens (-)
* No spaces, underscores, or special characters allowed
{% endhint %}
{% endstep %}

{% step %}
Your subdomain is now registered and its state will show as **Free**.
{% endstep %}
{% endstepper %}

***

## 📝 Configure Your [discloud.config](../../configurations/discloud.config/)

Once your subdomain is registered, you **must** add it to your `discloud.config` file so Discloud routes traffic to the correct app.

Open your `discloud.config` file and locate the `ID` field:

```ini
ID=yoursubdomain
```

{% hint style="warning" %}
#### **How to specify the subdomain in the `discloud.config` file?**

Use only the subdomain name, **not** the full domain (e.g., use `myapp`, not `myapp.discloud.app` or `myapp.discloud.dev`).

Example:

<pre class="language-ini" data-title="discloud.config"><code class="lang-ini"><strong>ID=myapp
</strong>TYPE=site
<a data-footnote-ref href="#user-content-fn-1"># ...</a>
</code></pre>
{% endhint %}

After updating `discloud.config`, **deploy your application** for the changes to take effect.

{% content-ref url="https://app.gitbook.com/s/ETNoAt35DpCBhinHpaRx/how-to-host" %}
[How To Host](https://app.gitbook.com/s/ETNoAt35DpCBhinHpaRx/how-to-host)
{% endcontent-ref %}

***

## 🔄 Subdomain States

Your registered subdomain can have two states:

{% hint style="info" %}
#### **🔵 In use**

* The subdomain is **registered and in use**.
* An app is currently deployed and accessible at `https://yoursubdomain.discloud.app` or `https://yoursubdomain.discloud.dev`, depending on the domain chosen when the subdomain was created.
* Traffic is being routed to your app on port 8080.
{% endhint %}

{% hint style="info" %}
#### **🟢 Free**

* The subdomain is **registered and available**.
* No app is currently using it.
* You can deploy an app to activate it at any time.
{% endhint %}

***

## 🌍 Access Your Site

Once your subdomain is **In use**, you can access it at one of these addresses, depending on the domain chosen when the subdomain was created:

```
https://yoursubdomain.discloud.app
https://yoursubdomain.discloud.dev
```

***

## ⚙️ Custom Domain

If you want to use your own domain (e.g., `yourdomain.com`) instead of a Discloud subdomain, check:

{% content-ref url="../../api-and-integrations/custom-domain.md" %}
[custom-domain.md](../../api-and-integrations/custom-domain.md)
{% endcontent-ref %}

[^1]: **Note:** The ... only indicate the continuation of other previous or subsequent options that are not relevant to mention on this page.
