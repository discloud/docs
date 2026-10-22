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

Create a database directly in the [Discloud Dashboard](https://discloud.com/dashboard/databases):

{% stepper %}
{% step %}
Open the **Databases** section and click [**Create database**](https://discloud.com/dashboard/databases/create).
{% endstep %}

{% step %}
Choose the **engine** and **version**. For PostgreSQL, you can enable the optional **pgvector** and **PostGIS** extensions.
{% endstep %}

{% step %}
Set the **service name** and the **credentials** (database name, user, and password). Redis and Valkey only ask for a password.
{% endstep %}

{% step %}
Optionally, pick a **project** and adjust the **RAM**. Then click **Create database**.
{% endstep %}
{% endstepper %}

### Available engines

| Engine     | Default version | Minimum RAM |
| ---------- | --------------- | ----------- |
| PostgreSQL | 17              | 512 MB      |
| MySQL      | 9.0             | 512 MB      |
| MongoDB    | 8.0             | 512 MB      |
| Redis      | 8.0             | 100 MB      |
| Valkey     | 7.2             | 100 MB      |

{% hint style="info" %}
Database RAM counts toward your plan's RAM limit, together with your applications.
{% endhint %}

### Tools to manage databases

The Dashboard's [**Templates**](https://discloud.com/dashboard/templates) section has ready-made tools to work with databases, such as **Adminer Painel SQL**, **SQLPad editor**, and **Tunnel TCP**, which connects your PC to a database on Discloud.

{% hint style="info" %}
#### **Need Another Engine?**

Open a [support ticket](https://discord.com/channels/@me/930852077045940224/) in the [Discord server](https://discord.discloudbot.com/) with the engine name, version, and use case. The team evaluates feasibility.
{% endhint %}

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
Test connectivity locally before deploying if possible.
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="Recommended video walkthrough" %}
{% embed url="https://youtu.be/kGPY9ZuJ0b0" %}
{% endtab %}
{% endtabs %}
