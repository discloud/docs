---
description: >-
  Inventory of dash v4 how-tos: what to teach, status, and links. Source for
  users and AI agents (with images when a how-to exists).
icon: table-columns
---

# Dashboard Guide

## 🎯 Purpose

This catalog lists **everything we can teach about the dashboard** (dash v4 at `/dashboard`).

* **Users** — find the right how-to with steps and images.
* **AI agents** — read this page to know what is documented, what is missing, the real route, and the UI pattern.

UI source of truth: **dash v4 only** (`sitev3` → `routes/dashboard` + `$lib/v4`). Do not use legacy `/v3/`.

{% hint style="info" %}
How-tos with images use **packs** (3–4 UI-faithful mockups). Published: [How to delete an application?](faq/general-questions/how-to-delete-an-application.md).
{% endhint %}

***

## ✅ Published (with images)

| How-to                                                                                 | Route                                                                 | Pack                |
| -------------------------------------------------------------------------------------- | --------------------------------------------------------------------- | ------------------- |
| [How to delete an application?](faq/general-questions/how-to-delete-an-application.md) | `/dashboard` → AppsTable → bulk Delete → type `delete` / PT `excluir` | list + bulk + modal |

***

## 📦 Apps (list `/dashboard`)

| How-to                        | Route / UI                     | Priority | Status   |
| ----------------------------- | ------------------------------ | -------- | -------- |
| Delete application            | AppsTable + type-confirm modal | High     | **Done** |
| Start / stop / restart app(s) | bulk-bar                       | High     | Pending  |
| Upload / create app           | `/dashboard/app/create`        | High     | Pending  |
| Filter apps                   | AppsTable filters              | Medium   | Pending  |
| Open app overview             | `/dashboard/app/{id}`          | High     | Pending  |

***

## 📱 App context (`/dashboard/app/{id}`)

| How-to                          | Route                 | Priority | Status              |
| ------------------------------- | --------------------- | -------- | ------------------- |
| Logs                            | `.../logs`            | High     | Partial (older FAQ) |
| Deploy / GitHub deploy          | `.../deploy`          | High     | Pending             |
| Web console                     | `.../console`         | Medium   | Pending             |
| Metrics                         | `.../metrics`         | Medium   | Pending             |
| App backups                     | `.../backups`         | High     | Partial             |
| App activity                    | `.../activity`        | Low      | Pending             |
| App env vars                    | `.../env`             | High     | Partial             |
| File explorer                   | `.../files`           | High     | Pending             |
| Edge                            | `.../edge`            | High     | Partial             |
| App domains                     | `.../domains`         | High     | Pending             |
| Settings / delete from overview | settings + name modal | High     | Pending             |

***

## 🌐 Domains

| How-to                    | Route                | Priority | Status  |
| ------------------------- | -------------------- | -------- | ------- |
| Create Discloud subdomain | `/dashboard/domains` | High     | Partial |
| Custom domain + DNS       | `/dashboard/domains` | High     | Partial |
| Remove subdomain / domain | type-confirm         | Medium   | Pending |

***

## 🗄️ Databases

| How-to                  | Route                         | Priority | Status  |
| ----------------------- | ----------------------------- | -------- | ------- |
| Create database         | `/dashboard/databases/create` | High     | Pending |
| List / bulk actions     | `/dashboard/databases`        | Medium   | Pending |
| Overview, logs, metrics | `/dashboard/databases/{id}/…` | Medium   | Pending |
| Backups and restore     | `.../backups`                 | High     | Partial |
| DB Studio               | `.../studio`                  | High     | Pending |
| Settings / delete       | `.../settings`                | High     | Pending |

***

## 🖥️ VPS

| How-to                        | Route                 | Priority | Status  |
| ----------------------------- | --------------------- | -------- | ------- |
| Buy RAM/SSD quota             | `/dashboard/vps`      | High     | Partial |
| Create machine                | create sheet          | High     | Pending |
| SSH / overview                | `/dashboard/vps/{id}` | High     | Pending |
| Restart / recreate / settings | overview + settings   | High     | Pending |
| Delete VPS                    | settings type-confirm | High     | Pending |

***

## ☁️ CDN and add-ons

| How-to                        | Route            | Priority | Status  |
| ----------------------------- | ---------------- | -------- | ------- |
| Buy / resize CDN add-on       | billing / CDN    | High     | Partial |
| Upload / folders / public URL | `/dashboard/cdn` | High     | Pending |
| Delete file/folder            | CDN modal        | Medium   | Pending |

***

## 📁 Projects and teams

| How-to                      | Route                   | Priority | Status  |
| --------------------------- | ----------------------- | -------- | ------- |
| Create project              | `/dashboard/projects`   | High     | Pending |
| Add apps/DBs to project     | project detail          | High     | Pending |
| Access / project env        | `.../access`, `.../env` | Medium   | Pending |
| Create team and permissions | `/dashboard/teams`      | High     | Partial |

***

## 🛠️ Tools

| How-to           | Route                  | Priority | Status  |
| ---------------- | ---------------------- | -------- | ------- |
| Builds           | `/dashboard/builds`    | Medium   | Pending |
| Snapshots        | `/dashboard/snapshots` | High     | Partial |
| Account activity | `/dashboard/activity`  | Low      | Pending |
| Templates        | `/dashboard/templates` | Medium   | Pending |
| API token        | `/dashboard/api-key`   | High     | Partial |
| Global env       | `/dashboard/env`       | High     | Pending |
| Connect GitHub   | `/dashboard/github`    | High     | Pending |
| Overview / tour  | `/dashboard/overview`  | Low      | Pending |

***

## 👤 Account and billing

| How-to                       | Route                | Priority | Status  |
| ---------------------------- | -------------------- | -------- | ------- |
| Account / profile            | `/dashboard/account` | Medium   | Pending |
| Subscription, plans, add-ons | `/dashboard/billing` | High     | Partial |

***

## 🧭 Sidebar nav

Main: Overview · Projects · Apps · Databases · Domains · VPS · CDN · (Storage soon).

Tools: Builds · Snapshots · Activity · Templates · API Keys · Global env.

Settings: Teams · GitHub · Account · Billing.

***

## 📐 Image pack pattern

1. Read the dash v4 Svelte route.
2. HTML mockup with Newman tokens.
3. Screenshot (browser + local http.server).
4. GitBook `insert_files` + stepper page.
5. Update **this table** (Status → Done + link).

{% hint style="success" %}
Suggested next packs: **start/stop/restart** → **upload app** → **create subdomain** → **custom domain** → **create database** → **CDN upload** → **create VPS**.
{% endhint %}
