---
description: >-
  Control your site's traffic at the Discloud edge with rules and redirects,
  before the request reaches the application.
icon: shield-halved
tags:
  - new
---

# Edge

## 🛡️ What is Edge?

Edge controls your site's traffic **before** the request reaches the application. Blocks, maintenance, headers, URL rewrites and redirects happen at the Discloud edge, on the app's [custom domain](custom-domain.md).

It doesn't replace the site's code. Whatever Edge handles, the app never even processes.

***

## 📍 Where to find it

[Discloud Dashboard](https://discloud.com/dashboard) → application (site) → **Edge**.

There are two tabs:

| Tab           | What it is for                                                                                                        |
| ------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Rules**     | Conditions + actions. Block, respond at the edge, redirect by rule, rewrite the URL, change headers or response text. |
| **Redirects** | Simple redirect from a path on your domain to another URL.                                                            |

***

## 📋 Requirements

To use Edge, you must meet these criteria:

{% hint style="success" %}
**Site** – The application must be a site. Bots don't have Edge.
{% endhint %}

{% hint style="success" %}
[**Custom domain**](custom-domain.md) – The site needs an active custom domain. A `*.discloud.app` [subdomain](../faq/general-questions/how-to-create-a-subdomain.md) doesn't count.
{% endhint %}

{% hint style="warning" %}
**Domain not in the legacy format** – If the domain is in the legacy format, open the app's **Domains** and migrate it first.
{% endhint %}

{% hint style="success" %}
[**Ruby plan or higher**](https://discloud.com/plans) – The site owner's plan is what counts. For an app shared through a Team, the member's plan doesn't count.
{% endhint %}

{% hint style="info" %}
**Permission to configure the app** – Owner, admin or developer. A viewer can only look, if the screen opens.
{% endhint %}

***

## 🔀 Traffic order

Every visit goes through this order:

<figure><img src="../.gitbook/assets/edge-traffic-flow.png" alt="Diagram of traffic going through Rules and Redirects before the application"><figcaption></figcaption></figure>

1. **Rules.** The platform checks the **active** rules, from highest to lowest priority. The **first** one that matches all its conditions is the one that applies. The ones below it don't run for that visit.
2. **Redirects.** If no rule stopped the request, the domain's active redirects are evaluated.
3. **Application.** Whatever is left goes on to the site as usual.

{% hint style="info" %}
A "block `/admin`" rule at the top keeps a redirect or the app from ever seeing that path.
{% endhint %}

***

## 📜 Rules

A rule has a name, a status (active or paused), one or more **conditions** and one or more **actions**.

* **Conditions are an AND.** All of them must be true. "Path starts with `/admin`" and "country is Brazil" only fires when both match.
* **Actions run in the order** they appear in the rule.
* **Priority** is the order of the list. Moving a rule up makes it be checked earlier.

### Conditions

| Condition       | Example                          |
| --------------- | -------------------------------- |
| URL path        | starts with `/admin`             |
| HTTP method     | is `POST`                        |
| Header          | `User-Agent` contains `bot`      |
| Query string    | the `debug` key exists           |
| Visitor country | is `BR`, or is not `BR` nor `PT` |

Operators: is, is not, starts with, ends with, contains, does not contain, has any value, is unknown.

### Actions

| Action                   | What it does                                                                                  |
| ------------------------ | --------------------------------------------------------------------------------------------- |
| Respond at the edge      | Returns a status and a body without calling the app. E.g. `403` Forbidden, `503` maintenance. |
| Redirect                 | Sends the visitor to a URL (`301` permanent or `302` temporary).                              |
| Rewrite URL              | Changes the path the app receives. The visitor still sees the original URL.                   |
| Set response header      | Adds a header, for example `X-Frame-Options: DENY`.                                           |
| Remove response header   | Removes headers such as `Server` and `X-Powered-By`.                                          |
| Replace text in response | Replaces a part of the HTML/text the app returned.                                            |

In redirect URLs and rewrites you can reuse the original request:

* `{http.request.uri.path}`: path (`/blog/post`)
* `{http.request.uri.query}`: query string, without the `?`

Example of a redirect that keeps the path: `https://new.example.com{http.request.uri.path}`.

### Ready-made templates

When creating a rule you can start from a template and adjust it:

* Block a path, a method, a User-Agent or a country
* Allow only some countries (blocks the rest)
* Maintenance page (`503`)
* Conditional redirect and URL rewrite
* Security header, header removal, text replacement
* Block when the `debug` query exists

{% hint style="warning" %}
A template is just a draft. Save it after reviewing the name, conditions and actions.
{% endhint %}

***

## ↪️ Redirects

Use them when the rule is just "this path on this domain goes to this URL". You don't need to repeat the source host: the redirect applies to the app's domain.

| Field                 | How to fill it in                                                                                                                      |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Destination URL       | Full address, with `https://`.                                                                                                         |
| Source path           | `*` for the whole domain, or a path. The `*` can only be **at the end** (`/docs*`). It must start with `/`, except for `*` on its own. |
| Type                  | **301** permanent (a definitive move, good for SEO) or **302** temporary (campaign, test).                                             |
| Preserve path         | The part of the URL after the match is passed on to the destination.                                                                   |
| Preserve query string | `?utm=...` and the rest are kept on the destination.                                                                                   |

### Examples

| Source                               | Destination                    | Effect                                                                            |
| ------------------------------------ | ------------------------------ | --------------------------------------------------------------------------------- |
| `*` + preserve path                  | `https://www.example.com`      | `example.com/pricing?plan=pro` becomes `https://www.example.com/pricing?plan=pro` |
| `/docs*` without preserving the path | `https://docs.example.com`     | Everything under `/docs...` lands on the documentation home                       |
| `/promo*` type 302                   | `https://campaign.example.com` | Temporary campaign redirect                                                       |

Redirects can also be paused. Pausing doesn't delete the rule.

***

## 🚫 What Edge doesn't do

* It doesn't protect bots, [databases](databases.md) or [VPS](../how-to-host/vps.md).
* It doesn't work on a free Discloud subdomain.
* It doesn't edit the app's code. A rewrite changes the internal URL. Replacing text only changes the response already generated.
* It isn't an IP firewall or a generic WAF. The control is whatever you configured in Rules and Redirects.
* A Team viewer can't create or edit.
