---
description: >-
  Group applications and databases that work together, share variables between
  them and give a Team access.
icon: folder-tree
tags:
  - new
---

# Projects

## 📂 What is a Project?

A Project groups applications and databases that work together. It helps you organize your account, centralize shared variables and, if you want, give a Team access.

A Project is **not** a new plan and does **not** create a server. Apps and databases are still the real resources. The Project only defines the grouping and who has access.

***

## 📋 Requirements

* Creating Projects requires the [**Diamond plan or higher**](https://discloud.com/plans).
* Members of a Team with a linked Project also see that Project in their list, even if they don't own it. What each person can do depends on their role in the Team.

***

## 📍 Where to find it

[Discloud Dashboard](https://discloud.com/dashboard) → **Projects**.

Inside a Project you will find:

| Area               | What it's for                                                    |
| ------------------ | ---------------------------------------------------------------- |
| **Overview**       | List of the Project's apps and databases, shortcuts and metadata |
| **Access manager** | Link or unlink a Team                                            |
| **Variables**      | Variables shared by every app in the Project                     |
| **Settings**       | Name, description and deletion                                   |

***

## 🧩 What a Project contains

| Item                      | Details                                            |
| ------------------------- | -------------------------------------------------- |
| **Applications**          | The apps linked to the Project.                    |
| **Databases**             | The databases linked to the Project.               |
| **Cluster**               | Every app in the Project must run on this cluster. |
| **Environment variables** | Values shared by the Project's apps.               |
| **Team**                  | Optional. At most one per Project.                 |

<figure><img src="../../.gitbook/assets/project-structure.png" alt="Diagram of a Team with access to a Project and what it contains"><figcaption></figcaption></figure>

Without a linked Team, only the owner manages the Project and everything in it.

***

## 🚀 Create a Project

{% stepper %}
{% step %}
**Open Projects**

In the dashboard, open **Projects** and click **New project**.
{% endstep %}

{% step %}
**Fill in the details**

Enter the **name** (required, 3 to 50 characters). The description and icon are optional.
{% endstep %}

{% step %}
**Confirm**

The cluster is assigned automatically. You can link a Team later in the **Access manager**.
{% endstep %}
{% endstepper %}

***

## 🔗 Link applications

In the Project, use **Add app** (or **Link app**).

* Apps that are already in another Project **don't** show up in the list. Remove them from their current Project first.
* If the app is on a **different cluster** from the Project, Discloud starts a **migration**. It can take a few minutes and the app is offline while it migrates. Follow it in **Builds**.
* **Leave project** only unlinks the app. It is **not** deleted.
* When uploading a new app (ZIP or GitHub), you can pick the Project right away if you have upload permission in it.

{% hint style="warning" %}
Apps hosted with a **Dockerfile** don't migrate between clusters automatically. To move one into the Project, remove the app and host it again, choosing the Project during the upload.
{% endhint %}

***

## 🗄️ Link databases

A [database](../../api-and-integrations/databases.md) created with a Project selected is linked to it from the start. In the Project view, the **Database** section lists only the databases in that group.

Creating a database also requires the **Diamond plan or higher**, the same as Projects and Teams.

***

## 👥 Access manager (Team)

Dashboard → Project → **Access manager**.

* **Link:** choose a Team you own. Its members can then see the Project and its apps and databases, according to each person's role.
* **Unlink:** the Team loses access immediately. The Project stays yours and the apps are not deleted.

{% hint style="info" %}
A Project can be linked to at most one Team at a time.
{% endhint %}

***

## ⚙️ Settings and deletion

| Action                    | Who can                    | Effect                                                                      |
| ------------------------- | -------------------------- | --------------------------------------------------------------------------- |
| Edit name and description | Owner, or a Team **admin** | Only changes the metadata.                                                  |
| Delete the Project        | Owner                      | Removes the Project. Apps and databases **stay** in the account, ungrouped. |
| Transfer the Project      | Nobody                     | Not available in the dashboard yet.                                         |

***

## 🔀 Project, Team and App

| Concept            | Role                                                        |
| ------------------ | ----------------------------------------------------------- |
| **App / Database** | The resource that runs and uses RAM.                        |
| **Project**        | Groups resources and sets the cluster and shared variables. |
| **Team**           | People with roles. Gets access when linked to a Project.    |

The usual flow is to create the Project, link (or create) the apps and databases in it and, if your team will work together, create a Team, add the members and link the Team to the Project.

To automate it, see the [Project API](../../api-and-integrations/api-overview/project.md).
