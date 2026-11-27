---
description: >-
  Quick VPS intro: first buy quota (Buy resources), then create the machine (New
  VPS).
icon: server
tags:
  - new
---

# VPS

## 🖥️ Summary

A VPS is cloud Linux with **root** over SSH. It does **not** use bots/sites plan RAM.

**Required order:**

1. **Buy resources** — RAM + SSD quota (add-on).
2. **New VPS** — create the machine only **after** quota is paid and has free GB.

Buying quota does **not** start a server. Creating a machine does **not** open a new plan: it only uses quota.

| Step              | Dashboard button        | Where               |
| ----------------- | ----------------------- | ------------------- |
| 1. Buy quota      | **Buy resources**       | Dashboard → **VPS** |
| 2. Create machine | **New VPS**             | Dashboard → **VPS** |
| 3. Access         | SSH (`root` + password) | Machine overview    |

{% hint style="info" %}
Usual minimums: **4 GB** RAM and **50 GB** SSD. Full walkthrough (checkout, fields, vCPU, status, canceling quota): product page.
{% endhint %}

{% hint style="danger" %}
Canceling VPS quota **destroys every machine** on the account.
{% endhint %}

***

## 📖 Full documentation

{% content-ref url="../platform-features/vps.md" %}
[vps.md](../platform-features/vps.md)
{% endcontent-ref %}

{% content-ref url="../platform-features/addons.md" %}
[addons.md](../platform-features/addons.md)
{% endcontent-ref %}
