---
description: >-
  Share Projects with other people and define what each member can see and
  change in the dashboard.
icon: users-gear
---

# Teams and Permissions

## 👥 What is a Team?

A Team is a group of people who share Projects and, with them, the apps and databases in those Projects. Each member has a **role**, which defines what that person can see and change in the dashboard.

Two different things decide what a member can do:

| What          | What it controls                                                                        | Who sets it                                          |
| ------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| **Plan**      | Which features the **owner's** account has unlocked (Console, domain, Edge and others). | The subscription of the resource owner.              |
| **Team role** | What **you** can do on that shared resource.                                            | The Team Owner, when inviting or editing the member. |

<figure><img src="../../.gitbook/assets/team-plan-and-role.png" alt="Diagram of the owner plan and member role allowing an action"><figcaption></figcaption></figure>

On a shared app, the plan that counts for advanced features is the **app owner's**, not yours. Your role only decides whether you can use that screen.

***

## 📋 Requirements

* Creating a Team requires the [**Diamond plan or higher**](https://discloud.com/plans).
* You can be a **member** of a Team even on a lower plan. The owner invites you using your [Discloud account ID](../../faq/general-questions/how-can-i-get-my-discloud-account-id.md).

***

## 📍 Where to find it

[Discloud Dashboard](https://discloud.com/dashboard) → **Team** (under Settings).

On the Team page you will find:

* the list of **members**, with their role, join date and an option to remove them
* the list of linked **Projects**
* options to edit the name and description, leave the Team or, if you are the owner, delete the Team

You can also link or unlink a Team from the Project's **Access manager**.

***

## 🎭 Roles

| Role          | Summary                                                                                                                        |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Owner**     | Owns the Team. Manages everything: members, Projects and Team deletion.                                                        |
| **Admin**     | Manages the Team and its Projects (name, access and members). Operates apps and variables.                                     |
| **Developer** | Operates Projects and apps (upload, Project variables and app settings, if they have the permission). Doesn't manage the Team. |
| **Viewer**    | Read only. Can't see or edit Project variables, can't upload and can't change settings.                                        |

### In the Project

| Action                                | Project owner | Admin | Developer | Viewer |
| ------------------------------------- | ------------- | ----- | --------- | ------ |
| See the Project                       | Yes           | Yes   | Yes       | Yes    |
| See and edit Project variables        | Yes           | Yes   | Yes       | No     |
| Upload or link an app to the Project  | Yes           | Yes   | Yes       | No     |
| Edit the Project name and description | Yes           | Yes   | No        | No     |
| Delete the Project                    | Yes           | No    | No        | No     |
| Link or unlink the Team               | Yes           | No    | No        | No     |

{% hint style="info" %}
The Project owner is the account that created the Project. It can be the same person as the Team Owner, but they are different roles.
{% endhint %}

### On shared applications and databases

On apps and databases shared through a Team, each action depends on a member permission. The dashboard shows or hides actions based on these permissions.

| Area                                                       | Permission     |
| ---------------------------------------------------------- | -------------- |
| App settings (auto-restart, private network, domain, Edge) | `config_app`   |
| Explorer (files)                                           | `explorer_app` |
| Web console                                                | `terminal_app` |
| Download backups                                           | `backup_app`   |
| Change settings or rebuild a database                      | `commit_app`   |
| Change a database's RAM                                    | `edit_ram`     |

If an action is blocked, there are two possible reasons. Your role doesn't include that permission, or the **owner's** plan doesn't unlock the feature (for example, Edge requires Ruby or higher).

***

## 🚀 Create and manage a Team

{% stepper %}
{% step %}
**Create the Team**

In **Team**, click **New team**. Enter the name (3 to 50 characters) and, if you want, a description.
{% endstep %}

{% step %}
**Add members**

Open the Team and click **Add member**. Enter the person's [**Discloud account ID**](../../faq/general-questions/how-can-i-get-my-discloud-account-id.md) (not their Discord username) and choose the role.
{% endstep %}

{% step %}
**Link a Project**

In **Add project**, choose a Project you own that isn't in another Team yet.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Each Project belongs to **one** Team at a time.
{% endhint %}

### Remove access

| Action             | Effect                                                                                         |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| **Remove member**  | The person immediately loses access to that Team's Projects, apps and databases.               |
| **Unlink Project** | The Project still exists. It just stops being shared with the Team.                            |
| **Leave Team**     | You remove your own access.                                                                    |
| **Delete Team**    | Permanent action by the Owner. The Projects are left without a Team, but they are not deleted. |

{% hint style="warning" %}
When you remove someone or unlink a Project, access is cut immediately. Let your team know first.
{% endhint %}

***

## 💎 Owner's plan and member's plan

A common case is an owner on Diamond or Ruby inviting a member on Free or Gold.

* The member **sees** the shared app.
* Features like Console, Explorer, domain and Edge follow the **owner's** plan, as long as the member's role allows the action.
* Creating a **new** Project, a **new** Team or buying an add-on still requires **your own** account's plan.

To automate it, see the [Team](../../api-and-integrations/api-overview/team.md) and [Team Apps](../../api-and-integrations/api-overview/team-apps.md) API.
