---
description: >-
  Create manual backups of your applications, download the daily automatic
  copies and restore databases from the dashboard.
icon: box-archive
tags:
  - new
---

# Backups

## 💾 What is a backup?

A backup on Discloud is a downloadable copy of an application's or database's data. There are two types:

| Type          | How it's created                          | Where it shows up                           | How long it's kept |
| ------------- | ----------------------------------------- | ------------------------------------------- | ------------------ |
| **Manual**    | You click **Backup** on the app overview. | In the download window, right away.         | You keep the file. |
| **Automatic** | Discloud creates **one copy per day**.    | App → **Backups** or Database → **Backups** | About **7 days**.  |

* **Manual** application backups are available on every plan.
* **Automatic** backups require the [**Diamond plan or higher**](https://discloud.com/plans).

{% hint style="info" %}
Backups are different from **Snapshots**, which keep versions of your apps in your account, even after an app is deleted. See the **Snapshots** page.
{% endhint %}

***

## 🖐️ Manual application backup

{% stepper %}
{% step %}
**Open the application**

In the [Discloud Dashboard](https://discloud.com/dashboard), open the application overview.
{% endstep %}

{% step %}
**Create the backup**

Click **Backup** and wait. The progress shows up in the operations widget (**Builds**).
{% endstep %}

{% step %}
**Download the file**

When the link is ready, the dashboard opens the **Backup download** window:

* **Download** saves the file directly in your browser.
* **Copy link** copies the temporary URL. Use it if the browser blocks the download and open the link in another tab.
{% endstep %}
{% endstepper %}

The file is usually a `.zip` for applications and a `.sql` for databases. Use the file name suggested in the download window. The backup ID is not the file name.

{% hint style="warning" %}
The download link is temporary. If you need the backup for longer, keep the file outside Discloud.
{% endhint %}

***

## 📅 Automatic backups

### Applications

Dashboard → application → **Backups**.

* The page lists the daily copies from the last \~7 days.
* Each copy can be downloaded by the owner or by a Team member with the `backup_app` permission.
* On plans below Diamond, the page shows how to upgrade.

### Databases

Dashboard → database → **Backups**.

Besides listing and downloading, a [database](../../api-and-integrations/databases.md) can be **restored** from an automatic backup.

{% stepper %}
{% step %}
**Choose the backup**

Choose the automatic backup from the day you want to recover.
{% endstep %}

{% step %}
**Open the restore**

Open the backup's restore action.
{% endstep %}

{% step %}
**Confirm the details**

Confirm the name, the RAM and, if you want, the Project of the new database. Follow the progress in the operations widget.
{% endstep %}
{% endstepper %}

<figure><img src="../../.gitbook/assets/database-backup-restore.png" alt="Diagram of a restore creating a new database from a backup"><figcaption></figcaption></figure>

{% hint style="info" %}
A restore **creates a new database** with the data from that backup. The current database is **not overwritten** and stays online.
{% endhint %}

***

## 👥 Team permissions

* On a shared app, downloading a backup requires the `backup_app` permission. Without it, the list may show up, but the download fails with a permission warning.
* The plan that unlocks automatic backups is the resource **owner's**, not the member's.

***

## 🧭 When to use each one

| Situation                                       | Use                                                        |
| ----------------------------------------------- | ---------------------------------------------------------- |
| You're about to make a risky change             | A **manual** backup before the change                      |
| You want the daily history of the last few days | **Automatic** backup (Diamond or higher)                   |
| You deleted the app and need what's left        | **Snapshots**                                              |
| You need a copy of the database from day X      | **Restore** in Database → Backups (creates a new database) |

***

## ⚠️ Limitations

* Automatic backups **don't** replace your own retention policy outside Discloud.
* After \~7 days, the automatic copy leaves the list.
* Don't use backups as the only way to migrate between accounts without testing the restore first.
* If the link expired or was removed, create another backup or choose a more recent copy.
