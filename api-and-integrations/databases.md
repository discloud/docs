---
description: >-
  Create managed databases (PostgreSQL, MySQL, MongoDB, Redis, and Valkey) from
  the Discloud Dashboard or use an external MongoDB Atlas.
icon: database
---

# Databases

## 🧭 Overview

Discloud applications can connect either to:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="databases.md#managed-databases">#managed-databases</a></td><td>Managed databases you create from the Discloud Dashboard.</td><td></td><td></td><td></td></tr><tr><td><a href="databases.md#external-mongodb-atlas">#external-mongodb-atlas</a></td><td>External MongoDB Atlas database-as-a-Service provider that you configure manually.</td><td></td><td></td><td></td></tr></tbody></table>

***

## 🗄️ Managed Databases <a href="#managed-databases" id="managed-databases"></a>

You choose the engine, the version and the RAM. Discloud starts the database, shows the credentials and lets your applications connect to it over the **private network** (VLAN), on the same cluster.

{% hint style="info" %}
Database RAM counts toward your plan's RAM limit, together with your applications.
{% endhint %}

### Requirements

| Feature                                | Minimum plan                              |
| -------------------------------------- | ----------------------------------------- |
| Create a managed database              | [**Diamond**](https://discloud.com/plans) |
| Hostname on the private network (VLAN) | **Diamond**                               |
| Daily automatic backup                 | **Diamond**                               |
| DB Studio                              | **Ruby**                                  |

On a database shared through a Team, members access it according to their permissions. The plan that unlocks Studio, VLAN and automatic backups is the database **owner's**.

### Where to find it

[Discloud Dashboard](https://discloud.com/dashboard/databases) → **Databases**. Inside each database:

| Page         | What it's for                                                                       |
| ------------ | ----------------------------------------------------------------------------------- |
| **Overview** | Status, credentials, connection URL and the start, stop, restart and delete actions |
| **Logs**     | The database's output, live and as history                                          |
| **Metrics**  | Memory, CPU, disk and network                                                       |
| **Backups**  | Daily copies, on-demand backup, download and restore                                |
| **Studio**   | Visual editor and queries (Ruby or higher)                                          |
| **Settings** | Display name, VLAN hostname, RAM and deletion                                       |

### Available engines

| Engine         | Minimum RAM | Credentials at creation          | Optional extensions       |
| -------------- | ----------- | -------------------------------- | ------------------------- |
| **PostgreSQL** | 512 MB      | Database name, user and password | **pgvector**, **PostGIS** |
| **MySQL**      | 512 MB      | Database name, user and password | None                      |
| **MongoDB**    | 512 MB      | Database name, user and password | None                      |
| **Redis**      | 100 MB      | Password only                    | None                      |
| **Valkey**     | 100 MB      | Password only                    | None                      |

The available versions show up on the creation screen and can change. Always check what the dashboard shows.

* **pgvector** adds vector similarity search to PostgreSQL.
* **PostGIS** adds geographic data and spatial queries to PostgreSQL.

{% hint style="info" %}
#### **Need Another Engine?**

Open a [support ticket](https://discord.com/channels/@me/930852077045940224/) in the [Discord server](https://discord.discloudbot.com/) with the engine name, version, and use case. The team evaluates feasibility.
{% endhint %}

***

## 🚀 Create a database

{% stepper %}
{% step %}
**Open the creation screen**

Open the **Databases** section and click [**Create database**](https://discloud.com/dashboard/databases/create).
{% endstep %}

{% step %}
**Choose the engine and version**

Choose the **engine** and **version**. For PostgreSQL, enable **pgvector** and **PostGIS** if you need them.
{% endstep %}

{% step %}
**Fill in the details**

* **Service name:** the database's name on Discloud. 2 to 32 characters, starting with a letter or number. Allows letters, numbers, `_` and `-`.
* **Credentials:** database name, user and password. The user **can't** be `root`. Redis and Valkey only ask for a password, with at least 8 characters.
{% endstep %}

{% step %}
**Project and RAM**

If you want, link the database to a **Project**. Adjust the **RAM** without going below the engine's minimum.
{% endstep %}

{% step %}
**Create**

Click **Create database** and follow the logs. The database can take a few moments to become **Online** after the success message.
{% endstep %}
{% endstepper %}

### Status and actions

On the overview, the status can be **Online**, **Offline**, **Error** or **RAM** (the database stopped because it ran out of memory). From there you can **start**, **stop**, **restart** or **delete** the database.

{% hint style="danger" %}
Deleting a database is **permanent**. The data and the service are erased.
{% endhint %}

***

## 🔌 Private connection (VLAN)

The database is **not on the public internet**. Only applications on Discloud, on the **same cluster** and with [**VLAN**](../configurations/discloud.config/vlan.md) enabled, can reach it.

<figure><img src="../.gitbook/assets/database-private-connection.png" alt="Diagram of the application reaching the database over the private network"><figcaption></figcaption></figure>

In the overview's **Private connection** card you can copy:

| Field                          | Content                                                                |
| ------------------------------ | ---------------------------------------------------------------------- |
| **Host**                       | The VLAN hostname, or `{id}.discloud` if no hostname has been set yet. |
| **Port**                       | The engine's port on the private network.                              |
| **Database / User / Password** | The engine's credentials. On Redis and Valkey, the user is `default`.  |
| **URL**                        | The ready-made connection string, in the engine's format.              |

URL formats the dashboard builds:

{% code title="Connection URL" %}
```
postgresql://USER:PASS@HOST:PORT/DB
mysql://USER:PASS@HOST:PORT/DB
mongodb://USER:PASS@HOST:PORT/DB?authSource=admin
redis://default:PASS@HOST:PORT
```
{% endcode %}

### Connect an application

{% stepper %}
{% step %}
**Enable VLAN**

In the application's settings, enable the **private network (VLAN)**. This requires the Diamond plan or higher on the application owner.
{% endstep %}

{% step %}
**Use the same cluster**

The application must be on the same cluster as the database. A **Project** helps keep both together.
{% endstep %}

{% step %}
**Store the URL in variables**

Paste the host, port or URL into the application's **environment variables**, never into Git.
{% endstep %}

{% step %}
**Rebuild or deploy**

Rebuild or deploy the application again so it gets the variables.
{% endstep %}
{% endstepper %}

### Access from outside Discloud

Direct public access to the database is **not** available yet. To reach it from your computer or manage it, use the Dashboard's [**Templates**](https://discloud.com/dashboard/templates):

* [**Tailscale**](https://discloud.com/dashboard/templates/tailscale-discloud), to reach the private network from your machine.
* **Tunnel TCP**, which connects your PC to a database on Discloud.
* **Adminer Painel SQL** and **SQLPad editor**, to manage the database from the browser.

***

## 📊 Logs and metrics

* **Logs:** the database's output live and by time range, with search, severity filter, copy, download and clear. Helps diagnose startup failures, out-of-memory issues and engine errors.
* **Metrics:** charts of memory (with the limit), CPU, disk reads and writes and network, over periods of 1 to 30 days. Use them to size the RAM and notice when the database is at its limit.

***

## 💾 Backups

Database → **Backups**.

| Action                   | Details                                                                         |
| ------------------------ | ------------------------------------------------------------------------------- |
| **Automatic backup**     | One copy per day, kept for about **7 days** (Diamond or higher).                |
| **Create backup**        | Creates a copy right away. The progress shows up on the page itself.            |
| **Download / Copy link** | Opens the download window with a temporary link.                                |
| **Restore**              | **Creates a new database** from the backup. The current one is not overwritten. |

During a restore you can set the new database's name, the RAM (at least 100 MB) and the Project. Follow the creation until the new database shows up in the list.

<figure><img src="../.gitbook/assets/database-backup-restore.png" alt="Diagram of a restore creating a new database from a backup"><figcaption></figcaption></figure>

***

## 🧪 DB Studio

Database → **Studio**. It's an editor inside the dashboard and requires the **Ruby plan or higher** on the database owner.

| Feature                                    | PostgreSQL / MySQL                         | MongoDB              | Redis / Valkey        |
| ------------------------------------------ | ------------------------------------------ | -------------------- | --------------------- |
| List tables or collections                 | Yes                                        | Yes                  | No                    |
| **Data** tab (create, edit, delete)        | Yes                                        | Yes (JSON documents) | No                    |
| **Structure** tab                          | Columns, primary key and indexes           | Collection metadata  | No                    |
| **Query** tab                              | SQL                                        | Commands and `find`  | Limited to the engine |
| Create, delete or empty a table/collection | Yes                                        | Yes                  | No                    |
| Import SQL                                 | Yes, from a file or text, up to **100 MB** | No                   | No                    |
| Export                                     | CSV, SQL or JSON                           | Yes                  | No                    |

{% hint style="warning" %}
* The database must be **online**.
* SQL import blocks dangerous commands such as `DROP DATABASE`, `GRANT`, `REVOKE` and `CREATE USER`.
* Without a known primary key, editing or deleting a row requires the **Query** tab.
* Exports are limited per batch. For large volumes, use the **Query** tab.
* Queries have a usage limit and a timeout of about 30 seconds. If one fails, simplify the query.
{% endhint %}

***

## ⚙️ Settings

Database → **Settings**.

| Field                               | Effect                                                                                                     |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Name in the list**                | Only changes the display name.                                                                             |
| **Hostname · private network**      | The host name on the VLAN. Requires Diamond or higher on the owner. Changing it **rebuilds** the database. |
| **Total RAM (MB)**                  | Between **100** and **16384**. Counts toward the owner's quota. Changing it can also rebuild.              |
| **Start / Stop / Restart / Delete** | The same actions as the overview.                                                                          |

When you save a hostname or RAM change, the dashboard shows the rebuild progress. Wait for it to finish before pointing your applications at it again.

On a database shared through a Team, changing settings or rebuilding requires the `commit_app` permission, and changing the RAM requires `edit_ram`.

To automate it, see the [Database API](api-overview/database.md).

***

## 🌍 Using External MongoDB Atlas <a href="#external-mongodb-atlas" id="external-mongodb-atlas"></a>

If you opt for MongoDB Atlas instead of a managed database:

{% stepper %}
{% step %}
Create a free or paid cluster at [https://www.mongodb.com/](https://www.mongodb.com/)
{% endstep %}

{% step %}
In Network Access, add IP: `0.0.0.0/0` (Allow from Anywhere) so Discloud containers can connect.
{% endstep %}

{% step %}
Copy the cluster's connection string (**Connect → Drivers**) and store it as an environment variable (e.g. `MONGODB_URI` in your [`.env`](../faq/general-questions/.env-file.md)).
{% endstep %}

{% step %}
Test connectivity locally before deploying if possible.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
With Atlas, Discloud's managed database pages (Studio, Backups and Metrics) don't apply.
{% endhint %}

{% tabs %}
{% tab title="Recommended video walkthrough" %}
{% embed url="https://youtu.be/kGPY9ZuJ0b0" %}
{% endtab %}
{% endtabs %}
