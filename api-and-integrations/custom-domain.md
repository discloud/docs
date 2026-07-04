---
description: Configure your domain for your Discloud hosted application.
icon: globe
---

# Custom Domain

## 🧭 Overview

You can map your own domain (e.g. `yourdomain.com`) or a subdomain (e.g. `dash.yourdomain.com`) to an application hosted on Discloud. The platform serves traffic through your app's [Discloud subdomain](../faq/general-questions/how-to-create-a-subdomain.md) using two A records pointing to our IPv4 addresses and validates ownership via TXT records.

<figure><img src="../.gitbook/assets/custom-domain-flow.png" alt="Custom domain flow diagram"><figcaption></figcaption></figure>

***

## 📋 Requirements

{% hint style="success" %}
[Diamond plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[App already hosted](../how-to-host/websites-and-apis.md) using a Discloud subdomain (e.g. `example.discloud.app`)
{% endhint %}

{% hint style="success" %}
A registered domain you control (Cloudflare, Hostinger, GoDaddy, Namecheap, etc.)
{% endhint %}

{% hint style="success" %}
Ability to add / modify A records
{% endhint %}

***

## 🏗️ Add Your Domain (Dashboard)

{% stepper %}
{% step %}
Open the [Discloud Dashboard](https://discloud.com/dashboard) → [`Domains`](https://discloud.com/dashboard/domains) section.
{% endstep %}

{% step %}
Enter your domain (e.g. `yourdomain.com`). Optionally specify a subdomain (e.g. `dash`).
{% endstep %}

{% step %}
Click **Add** and then the **DNS** button. When you click it, you will see the records you need to configure.
{% endstep %}
{% endstepper %}

<div data-full-width="false"><figure><img src="../.gitbook/assets/Website-Custom-Domain.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Website-Custom-Domain-DNS-A.png" alt="List of A records showing 75.2.96.173 and 99.83.186.151"><figcaption></figcaption></figure></div>

***

## ✅ Verify & Configure DNS

Although any DNS provider works, below are tabbed scenarios for clarity.

{% tabs %}
{% tab title="Root Domain" %}
**Records**

| Type | Name                   | Value           |
| ---- | ---------------------- | --------------- |
| A    | `@` (or provider root) | `75.2.96.173`   |
| A    | `@` (or provider root) | `99.83.186.151` |
{% endtab %}

{% tab title="Subdomain" %}
**Example: `dash.yourdomain.com`**

<table><thead><tr><th width="144">Type</th><th width="353">Name</th><th>Value</th></tr></thead><tbody><tr><td>A</td><td><code>dash</code></td><td><code>75.2.96.173</code></td></tr><tr><td>A</td><td><code>dash</code></td><td><code>99.83.186.151</code></td></tr></tbody></table>

Multiple subdomains (e.g. `api`, `app`) repeat this pattern independently.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
#### **Cloudflare Proxy**

If you use **Cloudflare**, it is mandatory to disable the **Proxy** (ensure it is set to **DNS Only** / **Grey Cloud**, not the Orange one). This ensures correct SSL certificate issuance.
{% endhint %}

<figure><img src="../.gitbook/assets/Cloudflare-Custom-Domain-DNS.png" alt="Cloudflare dashboard showing DNS Only (Grey Cloud) for A records"><figcaption></figcaption></figure>

***

## 🔄 Rebuild the App

After DNS resolves and tokens validate, open the linked app and trigger Rebuild so the binding becomes active.

<div data-full-width="false"><figure><img src="../.gitbook/assets/Website-Applications_Subdomain.png" alt="App list showing custom domain"><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Website-Applications_Rebuild.png" alt=""><figcaption></figcaption></figure></div>

***

### 📡 **DNS Propagation**

* DNS changes typically propagate within a few minutes.
* However, **TTL values** and **resolver cache** may cause some delays.
* To verify changes worldwide, check [dnschecker.org](https://dnschecker.org/)
* If some POPs still display old records, wait and re-check later.

<figure><img src="../.gitbook/assets/dns-check-propagation.png" alt=""><figcaption></figcaption></figure>
