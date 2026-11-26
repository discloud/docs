---
description: >-
  Add-ons are billed separately from your plan: extra quota you buy when you
  need it, without changing plans.
tags:
  - new
---

# Add-ons

## ➕ What is an add-on?

An **add-on** on Discloud is an **additive** resource, **independent from the plan** (Free, Platinum, Diamond, …).

* The **plan** defines what the account can do with bots, sites, app RAM, managed databases, and so on.
* The **add-on** is a separate subscription: you pick how many GB you want and pay for that, on top of the plan you already have.

Changing plans does **not** automatically include CDN or VPS quota. Buying an add-on does **not** change the plan.

{% hint style="info" %}
Purchasable add-ons today are **CDN** (public storage) and **VPS quota** (RAM + SSD for machines). Other types may exist in the system, but the UI only sells what the catalog enables.
{% endhint %}

***

## 📍 Where to find it

[Discloud Dashboard](https://discloud.com/dashboard) → **Subscription** / **Billing** → **Add-ons**.

* **CDN** appears in the add-ons grid to buy and resize GB.
* **VPS quota** (RAM + SSD) is bought and adjusted under **VPS → Buy resources** (both enter the same checkout).

***

## 📦 Available add-ons

### CDN

|                |                                                    |
| -------------- | -------------------------------------------------- |
| Purpose        | Store and serve public files on `cdn.discloud.com` |
| Unit           | Stored GB                                          |
| Minimum / step | 50 GB / 50 GB                                      |
| Bandwidth      | Unlimited                                          |

Usage details: [CDN](/broken/pages/cdn-product).

### VPS quota (RAM + SSD)

|                |                                                                          |
| -------------- | ------------------------------------------------------------------------ |
| Purpose        | Memory and disk pool to create [VPS machines](/broken/pages/vps-product) |
| Unit           | GB of RAM and GB of NVMe SSD                                             |
| Minimum / step | RAM 4 GB (step 4) · SSD 50 GB (step 50)                                  |
| Billing        | Both are purchased **together**                                          |

Buying quota does **not** create a machine. Creating a machine does **not** open a new plan: it only reserves GB you already have in the pool.

{% hint style="danger" %}
Canceling the VPS quota subscription **destroys every VPS machine** on the account.
{% endhint %}

Details: [VPS](/broken/pages/vps-product).

***

## 💳 How billing works

| Concept        | Plan                               | Add-on                                       |
| -------------- | ---------------------------------- | -------------------------------------------- |
| What it limits | Apps, sites, databases, tier perks | Only that product's quota                    |
| Subscription   | One (plan)                         | Another (or items in the add-on checkout)    |
| Increase       | Plan upgrade                       | Increase quantity (GB)                       |
| Decrease       | Plan downgrade rules               | Only down to what is already **in use**      |
| Cancel         | Affects apps/sites per plan rules  | Affects only that add-on (VPS: destroys VMs) |

Proration and renewal follow the dashboard Subscription flow (card, PIX, etc., as available on the account).

***

## 🧭 Plan vs add-on — examples

| Situation                             | What to do                                            |
| ------------------------------------- | ----------------------------------------------------- |
| Host a site on a Discloud subdomain   | **Platinum+** plan — not an add-on                    |
| Attach your own domain to the site    | **Diamond+** plan + [custom domain](custom-domain.md) |
| Serve static images with a public URL | **CDN** add-on                                        |
| Want Linux with root over SSH         | **VPS quota** add-on + create the machine             |

***

## 🚫 What an add-on does not do

* It does not replace the plan (it alone does not unlock sites, managed DBs, Edge, etc.).
* Quotas do not mix: CDN GB are not bot RAM; VPS RAM is not app RAM.
* It is not generic credit: each add-on has its own type and rules.
