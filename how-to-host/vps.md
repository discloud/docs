---
description: >-
  Create Linux servers with root SSH access using a RAM and SSD quota that is
  billed separately from the bots and sites plan.
icon: server
---

# VPS

## 🖥️ What is a VPS on Discloud?

A VPS is a cloud computer that is yours alone, with **root** access over SSH. You install and run whatever you need on it. It does **not** use the RAM or disk of the bots and sites plan: its quota is a separate add-on.

There are two steps, in this order:

1. **Buy a quota** of RAM and SSD.
2. **Create one or more machines** that use that quota.

{% hint style="info" %}
Buying resources does not start a machine on its own. Creating a machine does not charge a new plan either: it only reserves gigabytes you already have.
{% endhint %}

***

## 📍 Where to find it

In the [Discloud Dashboard](https://discloud.com/dashboard), open the **VPS** section.

* **Buy resources** opens the RAM + SSD purchase.
* **New VPS** creates the machine, if there is enough free quota.
* Each machine has an overview (access, IP, restart, recreate) and **Settings** (name, hardware, system, delete).

The same quota also shows up in **Subscription → Add-ons**.

***

## 💾 1. RAM and SSD quota

RAM and SSD are purchased **together**. On the first purchase, both go into the same checkout. You choose how many gigabytes of each and see the monthly total before paying.

| Resource | Minimum | Step            |
| -------- | ------- | --------------- |
| RAM      | 8 GB    | 2 GB at a time  |
| SSD NVMe | 100 GB  | 50 GB at a time |

The quota is an **account pool**, not "a ready-made machine". Example: 16 GB of RAM and 200 GB of SSD can become one 16/200 machine, or two 8/100 machines, as long as the total fits in what you bought.

<figure><img src="../.gitbook/assets/vps-quota-pool.png" alt="Diagram of the RAM and SSD quota split between two VPS"><figcaption></figcaption></figure>

What is already assigned to machines shows as **in use**. The rest is **free** and can go to a new machine or to upgrade an existing one.

You can **increase** the quota whenever you want. You can **decrease** it only down to what your machines are already using. If 10 GB of RAM are in use, the RAM quota cannot go below 10 GB. To go lower, shrink or delete machines first.

{% hint style="danger" %}
**Canceling the VPS quota subscription destroys every machine on the account.** Deleting a machine does not cancel the billing: the quota stays until you change or cancel the resources.
{% endhint %}

IPv4, IPv6 and unlimited traffic come with the machine. You don't buy an IP or a traffic allowance separately.

***

## 🚀 2. Create the machine

With free quota, **New VPS** asks for:

| Field                | What it is                                                                                           |
| -------------------- | ---------------------------------------------------------------------------------------------------- |
| RAM (GB)             | How much of the quota the machine reserves. Minimum 8 GB, and no more than what is free.             |
| Disk (GB)            | Reserved SSD NVMe. Minimum 100 GB, within what is free.                                              |
| vCPU                 | Calculated from the RAM. You don't choose it.                                                        |
| Region               | Where the machine is created. Currently: **North America**. Creation needs a free IP in that region. |
| System               | List of systems available at the moment (Ubuntu and others the platform offers).                     |
| Name and description | Just your own label. They don't change price or hardware.                                            |

### How the vCPU is set

| Machine RAM                  | vCPU                            |
| ---------------------------- | ------------------------------- |
| Less than 8 GB               | Not created. Below the minimum. |
| From 8 GB to less than 16 GB | 4 vCPU                          |
| 16 GB or more                | 8 vCPU                          |

The screen shows a preview ("4 vCPU with this configuration") before you confirm. The final value is the one the platform sets at creation time.

While the machine is starting up, its status is **Provisioning**. It is usually ready in about 45 seconds. When it finishes, the status changes to **Online** and the IP appears. If the region has no free IP, creation fails and the quota is not held by a machine that doesn't exist: try again later.

### Machine status

| Status           | Meaning                                               |
| ---------------- | ----------------------------------------------------- |
| Awaiting payment | The quota tied to this machine has not been paid yet. |
| Provisioning     | The platform is creating the server.                  |
| Online           | The machine is up.                                    |
| Suspended        | Offline because of billing or an account block.       |
| Error            | Creation or an operation failed.                      |

***

## 🔑 SSH access

In the machine's overview:

* **IPv4** and **IPv6**
* **User** (root)
* **Password**
* A ready-to-copy **SSH** command

{% hint style="warning" %}
The password is **not stored in billing**. Copy it as soon as it appears. When the machine starts, Discloud also sends the IP, user and password to the account's email. If the password disappears from the screen, use that email.

There is no way to "reveal again" a password you didn't save: the options are to recreate the machine (this wipes the disk) or to change the password yourself, from inside SSH.
{% endhint %}

Connect with any SSH client. From then on the server is yours: packages, firewall, services, users.

***

## 🛠️ What you can do afterwards

| Action               | What happens to the data                                       | Quota and IP                                                                                                                   |
| -------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Restart              | The disk is kept.                                              | Kept.                                                                                                                          |
| Increase RAM or disk | The disk is kept. Only goes up, and only up to the free quota. | The machine takes up more of the pool.                                                                                         |
| Recreate             | **Wipes the whole disk** and reinstalls the same system.       | Quota and IP are kept.                                                                                                         |
| Change the system    | **Wipes the disk** and reinstalls with the new OS.             | Quota and IP are kept.                                                                                                         |
| Delete the machine   | The machine no longer exists.                                  | The quota **stays on the account** and becomes free again. Monthly billing continues until you reduce or cancel the resources. |
| Cancel the VPS quota | **Every VPS on the account is destroyed.**                     | The RAM/SSD subscription ends.                                                                                                 |

Name and description can be edited freely. This doesn't restart or charge anything.

{% hint style="warning" %}
You can't decrease the RAM or disk of a machine that already exists. If you need a smaller machine, delete this one (or shrink others) and create it again within the free quota.

Recreating and changing the OS are reinstalls: backing up what matters on the disk beforehand is your responsibility.
{% endhint %}

***

## 🔀 VPS and the rest of the platform

| Item         | App plan                                       | VPS                    |
| ------------ | ---------------------------------------------- | ---------------------- |
| What you get | Managed bot or site (deploy, logs, app domain) | Linux server with root |
| Billing      | Discloud plan                                  | RAM + SSD add-on       |
| Limit        | Plan RAM, per app                              | The GB pool you bought |
| Access       | Discloud Dashboard                             | SSH                    |

A VPS does not appear in the applications list. A site on Discloud doesn't turn into a VPS. They are independent products on the same account.
