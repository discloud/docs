---
description: >-
  Map of the Discloud dashboard: sidebar menus and paths to find apps,
  databases, domains, VPS, CDN, and settings.
icon: map-location-dot
---

# Where to find things in the dashboard?

The dashboard is at [discloud.com/dashboard](https://discloud.com/dashboard). Main navigation is the **sidebar**. Some items only appear after you open an app, database, VPS, or project.

{% hint style="info" %}
Some menus depend on your **plan** or team permission. If an item is locked or missing, check the account plan and access to that resource.
{% endhint %}

***

## 📌 Main menu (always in the sidebar)

| Where     | Path                   | What it is                             |
| --------- | ---------------------- | -------------------------------------- |
| Overview  | `/dashboard/overview`  | Account summary                        |
| Projects  | `/dashboard/projects`  | Group apps and databases               |
| Apps      | `/dashboard`           | Applications list                      |
| Databases | `/dashboard/databases` | Managed databases                      |
| Domains   | `/dashboard/domains`   | Discloud subdomains and custom domains |
| VPS       | `/dashboard/vps`       | VPS quota and machines                 |
| CDN       | `/dashboard/cdn`       | Public CDN files                       |

Storage may appear in the sidebar but is not available yet.

***

## 📱 Inside an application

Open an app from the list (or `/dashboard/app/{id}`). The sidebar then shows **that app’s** menu:

| Item                  | Path                               |
| --------------------- | ---------------------------------- |
| Overview              | `/dashboard/app/{id}`              |
| Logs                  | `/dashboard/app/{id}/logs`         |
| Deploy                | `/dashboard/app/{id}/deploy`       |
| Console               | `/dashboard/app/{id}/console`      |
| Metrics               | `/dashboard/app/{id}/metrics`      |
| Backups               | `/dashboard/app/{id}/backups`      |
| Activity              | `/dashboard/app/{id}/activity`     |
| Environment variables | `/dashboard/app/{id}/env`          |
| Files                 | `/dashboard/app/{id}/files`        |
| Edge                  | `/dashboard/app/{id}/edge` (sites) |
| Settings              | `/dashboard/app/{id}/settings`     |

Use the back link at the top of the app sidebar to return to the apps list.

***

## 🗄️ Inside a database

Open a database at `/dashboard/databases/{id}`:

| Item      | Path                        |
| --------- | --------------------------- |
| Overview  | `/dashboard/databases/{id}` |
| Logs      | `.../logs`                  |
| Metrics   | `.../metrics`               |
| Backups   | `.../backups`               |
| DB Studio | `.../studio`                |
| Settings  | `.../settings`              |

Create a new database: `/dashboard/databases/create`.

***

## 🖥️ Inside a VPS

| Item                 | Path                           |
| -------------------- | ------------------------------ |
| List / buy resources | `/dashboard/vps`               |
| Machine overview     | `/dashboard/vps/{id}`          |
| Settings             | `/dashboard/vps/{id}/settings` |

***

## 📁 Inside a project

| Item        | Path                       |
| ----------- | -------------------------- |
| Overview    | `/dashboard/projects/{id}` |
| Access      | `.../access`               |
| Project env | `.../env`                  |
| Settings    | `.../settings`             |

***

## 🛠️ Tools (sidebar group)

| Item       | Path                   |
| ---------- | ---------------------- |
| Builds     | `/dashboard/builds`    |
| Snapshots  | `/dashboard/snapshots` |
| Activity   | `/dashboard/activity`  |
| Templates  | `/dashboard/templates` |
| API Keys   | `/dashboard/api-key`   |
| Global env | `/dashboard/env`       |

***

## ⚙️ Account, team, and integrations

| Item                   | Where                                      |
| ---------------------- | ------------------------------------------ |
| Teams                  | `/dashboard/teams`                         |
| GitHub                 | `/dashboard/github`                        |
| Account / profile      | user menu → Account (`/dashboard/account`) |
| Subscription / billing | user menu → Billing (`/dashboard/billing`) |

***

## 🔎 Useful shortcuts

| I want to…                 | Go to                                                        |
| -------------------------- | ------------------------------------------------------------ |
| Delete or restart an app   | **Apps** list (`/dashboard`) — select and use the action bar |
| Subdomain or custom domain | **Domains**                                                  |
| API token                  | **API Keys** (tools)                                         |
| Env vars for all apps      | **Global env** (tools) or each app’s env                     |
| Public static files        | **CDN**                                                      |
| Linux server with SSH      | **VPS**                                                      |

{% content-ref url="../general-questions/how-to-delete-an-application.md" %}
[how-to-delete-an-application.md](../general-questions/how-to-delete-an-application.md)
{% endcontent-ref %}
