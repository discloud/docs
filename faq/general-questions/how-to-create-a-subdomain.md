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

***

## ✅ Requirements

To register and use a Discloud subdomain, you must meet the following requirements:

{% hint style="success" %}
[Platinum Plan or Higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
**Port 8080** – Your application must listen on port 8080 for external traffic
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
Click on the `Subdomain` tab at the top of the application page.

<figure><img src="../../.gitbook/assets/dashboard-subdomain-tab.png" alt="Dashboard Subdomain tab"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
Click the `+ Subdomain` button to create a new subdomain.

<figure><img src="../../.gitbook/assets/dashboard-subdomain-button.png" alt="Add Subdomain button"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
Enter your desired subdomain name (e.g., `myapp`, `dashboard`, `api`).

{% hint style="info" %}
#### **Subdomain naming rules**

* Maximum **20 characters**
* Only alphanumeric characters (A–Z, 0–9) and hyphens (-)
* No spaces, underscores, or special characters allowed
{% endhint %}
{% endstep %}

{% step %}
Your subdomain is now registered and its state will show as **Available**.
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

Use only the subdomain name, **not** the full domain (e.g., use `myapp`, not `myapp.discloud.app`).

Example:

<pre class="language-ini" data-title="discloud.config"><code class="lang-ini"><strong>ID=myapp
</strong>TYPE=site
<a data-footnote-ref href="#user-content-fn-1"># ...</a>
</code></pre>
{% endhint %}

After updating `discloud.config`, **deploy your application** for the changes to take effect.

{% content-ref url="https://app.gitbook.com/s/ETNoAt35DpCBhinHpaRx/how-to-host-using" %}
[How to Host, Using](https://app.gitbook.com/s/ETNoAt35DpCBhinHpaRx/how-to-host-using)
{% endcontent-ref %}

***

## 🔄 Subdomain States

Your registered subdomain can have two states:

{% hint style="info" %}
#### **🔵 Active**

* The subdomain is **registered and in use**.
* An app is currently deployed and accessible at `https://yoursubdomain.discloud.app`.
* Traffic is being routed to your app on port 8080.
{% endhint %}

{% hint style="info" %}
#### **🟢 Available**

* The subdomain is **registered and available**.
* No app is currently using it.
* You can deploy an app to activate it at any time.
{% endhint %}

***

## 🌍 Access Your Site

Once your subdomain is **Active**, you can access it via:

```
https://yoursubdomain.discloud.app
```

***

## ⚙️ Custom Domain

If you want to use your own domain (e.g., `yourdomaind.com`) instead of a Discloud subdomain, check:

{% content-ref url="../../api-and-integrations/custom-domain.md" %}
[custom-domain.md](../../api-and-integrations/custom-domain.md)
{% endcontent-ref %}

[^1]: **Note:** The ... only indicate the continuation of other previous or subsequent options that are not relevant to mention on this page.
