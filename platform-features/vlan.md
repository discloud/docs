---
description: >-
  Connect Discloud applications and databases over an internal network, without
  exposing ports to the public internet.
icon: network-wired
---

# Private Network (VLAN)

## 🧭 Overview

The VLAN connects Discloud applications and databases over an **internal network**. Traffic never leaves for the public internet: a backend talks to a PostgreSQL or a Redis through the internal hostname, without opening any external port.

The VLAN does **not** replace the domain, the subdomain or the website's public network. They are different paths:

| Network            | What it's for                                                                                                                                                   |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Public**         | Website or API reachable on the internet, through the [subdomain](../faq/general-questions/how-to-create-a-subdomain.md) or a [custom domain](custom-domain.md) |
| **Private (VLAN)** | Application ↔ application or application ↔ database **inside** Discloud, on the same cluster                                                                    |

<figure><img src="../.gitbook/assets/vlan-private-network.png" alt="Private network (VLAN) diagram: the website gets the public traffic and talks to the internal API and the database on the same cluster"><figcaption></figcaption></figure>

***

## 📋 Requirements

To use the private network, you must meet these criteria:

{% hint style="success" %}
[**Diamond plan or higher**](https://discloud.com/plans) – The plan that counts is the one of the **owner** of the application or database.
{% endhint %}

{% hint style="success" %}
**Same cluster** – The VLAN doesn't cross clusters. The applications and databases that talk to each other must be on the same cluster.
{% endhint %}

{% hint style="info" %}
On an application shared through a [Team](teams-and-permissions.md), the member needs the `config_app` permission to change the private network. The plan that unlocks the VLAN is still the owner's.
{% endhint %}

***

## ⚙️ Configure

{% tabs %}
{% tab title="Dashboard" %}
[Discloud Dashboard](https://discloud.com/dashboard) → application → **Settings** → **Private Network (VLAN)** card.

1. Turn on the **Private network** switch.
2. Set the **Internal hostname** (e.g. `internal-api`, `my-cache`).
3. Click **Save**.

Below the Diamond plan, the card is disabled and shows "Available from the Diamond plan".
{% endtab %}

{% tab title="discloud.config" %}
On upload or commit, use the `VLAN` and `HOSTNAME` keys in [`discloud.config`](../configurations/discloud.config/):

{% code title="discloud.config" %}
```properties
NAME=My Mongo Service
VLAN=true
HOSTNAME=mymongoserver
```
{% endcode %}

| Key        | Required    | Purpose                                                          |
| ---------- | ----------- | ---------------------------------------------------------------- |
| `VLAN`     | Yes         | Turns on the private network for this application                |
| `HOSTNAME` | Recommended | Name the **other** applications on the VLAN use to find this one |
{% endtab %}

{% tab title="Database" %}
[Discloud Dashboard](https://discloud.com/dashboard/databases) → database → **Settings** → **Hostname · private network**.

The database overview already shows the host, port and URL of the **private connection**. That host only answers applications on the same cluster with the VLAN turned on. The URL formats are on [Databases](databases.md).
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Changing the VLAN or the hostname triggers a **rebuild** of the application. Follow the progress until it finishes.
{% endhint %}

{% hint style="info" %}
If the dashboard and `discloud.config` have different values, what was applied on the last deploy or rebuild is what counts. Use only one of the two to avoid confusion.
{% endhint %}

***

## 🧵 Hostname rules

### Applications

| Rule       | Value                                                                       |
| ---------- | --------------------------------------------------------------------------- |
| Characters | `a-z`, `A-Z`, `0-9`, underscore (`_`) and hyphen (`-`)                      |
| Length     | Up to **25** characters                                                     |
| Uniqueness | Don't use the same hostname on two applications. The behavior is undefined. |
| Case       | Prefer all lowercase                                                        |

Valid examples: `billing-api`, `my_cache`, `internal_api`.

### Databases (when editing the hostname)

| Rule           | Value                                                                                 |
| -------------- | ------------------------------------------------------------------------------------- |
| Format         | **1 or 2** segments of `a-z`, `0-9` and `_`, joined by **at most one** hyphen (`-`)   |
| Length         | Up to **25** characters (the value is normalized to lowercase)                        |
| Valid examples | `postgres`, `my_db`, `cache-redis`                                                    |
| Invalid        | `a-b-c` (more than one hyphen), special characters, empty hostname after sanitization |

If the database hostname hasn't been set yet, the dashboard shows `{id}.discloud`. Prefer setting a clear and stable hostname.

***

## 🔗 Connect two applications

For an application A to talk to an application or database B:

1. A and B must be on the **same cluster**.
2. The VLAN must be on for the sides that need to be reached, on the application that connects and on the service that listens, as the case may be.
3. The credentials and URL go in the [environment variables](environment-variables.md), never in Git.
4. After changing the VLAN, the hostname or the variables, rebuild or deploy again.

{% hint style="info" %}
If the application is on another cluster, linking it to a [Project](projects.md) can migrate it to the Project's cluster. Applications with a **Dockerfile** don't migrate automatically.
{% endhint %}

***

## 🧷 Examples

### 🗄️ Application → managed database

1. Create the database (PostgreSQL, MySQL, MongoDB, Redis or Valkey). This requires the Diamond plan or higher.
2. Copy the private URL from the database overview.
3. On the application, on the same cluster, turn on the VLAN and store the URL in a variable, like `DATABASE_URL`.
4. Rebuild the application and check the connection in the logs.

<figure><img src="../.gitbook/assets/database-private-connection.png" alt="Diagram of the application reaching the database over the private network"><figcaption></figcaption></figure>

### 🔁 Application → application (internal API)

The service turns on the VLAN and sets the hostname:

{% code title="discloud.config" %}
```properties
VLAN=true
HOSTNAME=billing-api
```
{% endcode %}

Another application, on the same VLAN and cluster, calls the service by its hostname:

```
http://billing-api:8080/internal/...
```

The port is the one the process listens on **inside** the application, not the website's public port.

The same goes for a database hosted in an application. With a MongoDB in the application with `HOSTNAME=mymongoserver`, the backend connects like this:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import mongoose from "mongoose";

const uri = "mongodb://mymongoserver:27017/mydatabase";
//                            ^
//                            HOSTNAME of the MongoDB application

async function main() {
  try {
    await mongoose.connect(uri);
    console.log("Connected to MongoDB successfully");
  } catch (error) {
    console.error("MongoDB connection error:", error);
    process.exit(1);
  }
}

main();
```
{% endtab %}

{% tab title="Node (Native Driver)" %}
```javascript
import { MongoClient } from "mongodb";
const uri = "mongodb://mymongoserver:27017/mydatabase";
const client = new MongoClient(uri);
await client.connect();
console.log("Ping:", await client.db().command({ ping: 1 }));
```
{% endtab %}

{% tab title="Python" %}
```python
from pymongo import MongoClient
client = MongoClient('mongodb://mymongoserver:27017/mydatabase')
print(client.admin.command('ping'))
```
{% endtab %}
{% endtabs %}

### ⚡ Redis cache between bots

1. Create a managed Redis, or host Redis in an application with `VLAN=true` and `HOSTNAME=cache`.
2. In the bots, on the same cluster and with the VLAN on, use `REDIS_URL=redis://default:PASSWORD@cache:PORT`, or the host and port the dashboard shows.

***

## 🚫 What the VLAN doesn't do

* It doesn't publish the service on the internet.
* It doesn't give your computer access to the database. For that, use the dashboard [Templates](https://discloud.com/dashboard/templates) (Tailscale, Tunnel TCP, Adminer or SQLPad). Direct public access to the database isn't in the dashboard yet.
* It doesn't replace authentication. Keep using a user, a password and secrets in the environment variables.
* It doesn't connect applications from different accounts or different clusters.

***

## 🛡️ Security

* Only your applications, or your Team's in the Project, with the VLAN on and on the same cluster can reach each other.
* Turn off the VLAN on applications that don't need to be reached internally.
* Change the database passwords if they leak. The VLAN reduces exposure, but it doesn't replace good credentials.
* Public websites stay on the public network. Use the VLAN only for the internal path, like API → database or bot → cache.
