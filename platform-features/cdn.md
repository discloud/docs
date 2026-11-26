---
description: >-
  Store and serve public files through Discloud CDN. Quota is an add-on
  independent from the bots and sites plan.
tags:
  - new
---

# CDN

## 📦 What is the CDN?

Discloud CDN is **public file storage** for your account. You upload images, assets, documents or any static file and get a public URL on `cdn.discloud.com`.

It does **not** use the RAM or disk of the bots and sites plan. Quota comes from the [CDN add-on](/broken/pages/addons-product): you pay for **stored GB**. Ingress and egress are unlimited — there is no bandwidth charge.

{% hint style="info" %}
File reads are public. Anyone with the URL can download. Do not store secrets, tokens or private backups on the CDN.
{% endhint %}

***

## 📍 Where to find it

[Discloud Dashboard](https://discloud.com/dashboard) → **CDN**.

* Browse account files and folders
* Upload (simple or multipart for large files)
* Create / delete folders
* See add-on usage and quota

Buying and resizing quota is under **Subscription → Add-ons** (**CDN** type). Details: [Add-ons](/broken/pages/addons-product).

To automate uploads and management, see the [CDN API](../api-and-sdks/api-overview/cdn.md).

***

## 📋 Requirements

{% hint style="success" %}
**Active CDN add-on** – Without the add-on (or with 0 GB), the dashboard and API reject writes. Public reads of existing URLs can still work while the object exists.
{% endhint %}

There is no minimum bots/sites plan to use CDN. Free or any plan can buy the add-on.

***

## 💾 Quota

| Item             | Value                         |
| ---------------- | ----------------------------- |
| Unit             | Stored GB                     |
| Purchase minimum | **50 GB**                     |
| Step             | **50 GB**                     |
| Bandwidth        | Unlimited (no traffic charge) |

The dashboard shows **used**, **quota** and **remaining**. If the file does not fit in free space, upload fails.

{% hint style="warning" %}
Canceling the CDN add-on removes write quota. Plan what to do with files before canceling.
{% endhint %}

***

## 🔗 Public URLs

Every file lives under your account ID:

```
https://cdn.discloud.com/{yourUserId}/{relative/path}
```

Examples:

| Path in dashboard / API | Public URL                                            |
| ----------------------- | ----------------------------------------------------- |
| `images/logo.png`       | `https://cdn.discloud.com/{userId}/images/logo.png`   |
| `brand/favicon.ico`     | `https://cdn.discloud.com/{userId}/brand/favicon.ico` |

You do **not** send `userId` in the upload path. Send only the relative path.

***

## 📁 Path rules

| Rule      | Detail                                          |
| --------- | ----------------------------------------------- |
| Format    | Relative, **no** leading `/`                    |
| Segments  | Letters, numbers, `.`, `_`, `-`                 |
| Forbidden | `..`, `//`, spaces, accents, special characters |
| Folders   | Max **8** levels; path ≤ **512** characters     |

Valid: `logo.png`, `images/goto.png`, `a/b/c/file.webp`\
Invalid: `/logo.png`, `../x`, `my folder/a.png`

***

## ⬆️ Upload

{% tabs %}
{% tab title="File ≤ 100 MB" %}
Use simple upload in the dashboard (or `PUT /cdn/upload` in the API).

Provide the destination **path** and the size in **bytes**. The platform checks quota before accepting the stream.
{% endtab %}

{% tab title="File > 100 MB" %}
Use the **multipart** flow (several parts). Intermediate parts are at least \~5 MB; each HTTP body is capped around \~100 MB.

In the dashboard, large uploads are handled by the UI. In the API, see [CDN](../api-and-sdks/api-overview/cdn.md).
{% endtab %}
{% endtabs %}

{% stepper %}
{% step %}
**Buy quota**

In Subscription → Add-ons (or from CDN itself), enable the **CDN** add-on with at least 50 GB.
{% endstep %}

{% step %}
**Open CDN**

Dashboard → **CDN**. Create folders if you want structure (`images/`, `docs/`, …).
{% endstep %}

{% step %}
**Upload the file**

Upload to the desired path. Copy the public URL and use it in your site, bot or app.
{% endstep %}
{% endstepper %}

***

## 🛠️ What you can do

| Action        | Effect                            |
| ------------- | --------------------------------- |
| List          | Browse folders and files          |
| Upload        | Publish the file on the CDN URL   |
| Overwrite     | May replace an existing path      |
| Create folder | Empty folder marker               |
| Delete file   | Removes one path                  |
| Delete folder | Removes everything under a prefix |

***

## 🚫 What CDN is not

* Not the disk of your applications or [VPS](/broken/pages/vps-product).
* Not private S3 Object Storage (separate / not for purchase in the catalog).
* Does not authenticate downloads: the URL is public.
* Does not replace [custom domain](custom-domain.md) or site [Edge](edge.md).

***

## 🧭 Next steps

{% content-ref url="/broken/pages/addons-product" %}
[Broken link](/broken/pages/addons-product)
{% endcontent-ref %}

{% content-ref url="../api-and-sdks/api-overview/cdn.md" %}
[cdn.md](../api-and-sdks/api-overview/cdn.md)
{% endcontent-ref %}
