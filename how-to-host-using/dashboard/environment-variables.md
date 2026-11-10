---
description: >-
  Set environment variables in the dashboard at three levels (account, project
  and app) and learn when to use the BUILD_ prefix.
icon: sliders
---

# Environment Variables

## 🔑 What are they?

Environment variables are `NAME=value` pairs that your application reads while it runs. If you use the `BUILD_` prefix, they are also available during the build.

In the Discloud dashboard they exist at **three levels**. The more specific the level, the higher its priority.

<figure><img src="../../.gitbook/assets/env-vars-precedence.png" alt="Diagram of variable priority between account, project and app"><figcaption></figcaption></figure>

If the same name exists at all three levels, the application gets the **app** value. If it's not set on the app, it uses the **project** value. If it's not set on the project, it uses the **account** value.

***

## 📍 Where each level lives

| Level       | Path in the dashboard            | Applies to               |
| ----------- | -------------------------------- | ------------------------ |
| **Account** | Dashboard → **Global variables** | All your applications    |
| **Project** | Project → **Variables**          | The apps in that Project |
| **App**     | Application → **Variables**      | Only that application    |

{% hint style="warning" %}
Don't put secrets in Git. The repository's [`.env`](../../faq/general-questions/.env-file.md) file doesn't replace the dashboard. In production, use Discloud's variables.
{% endhint %}

***

## 👤 Who can edit

| Level       | Who edits                                                                                                |
| ----------- | -------------------------------------------------------------------------------------------------------- |
| **Account** | The account owner.                                                                                       |
| **Project** | The Project owner, or a Team member with the **Admin** or **Developer** role. Viewers can't see or edit. |
| **App**     | The app owner, or a Team member with permission to configure the app.                                    |

***

## ✏️ How to edit

All three levels use the same editor:

| Action             | What it does                                                                                                                      |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------- |
| **Add**            | Creates a variable with a name and value.                                                                                         |
| **Show / hide**    | Shows or hides the value on screen.                                                                                               |
| **Copy**           | Copies one value or all variables.                                                                                                |
| **Paste .env**     | Imports `NAME=value` lines. Accepts `#` comments, `export` and quotes. You can merge with the current ones or replace everything. |
| **Remove**         | Removes one variable or clears the whole level.                                                                                   |
| **Save / Discard** | Saves or undoes pending changes.                                                                                                  |

There is a limit of variables per level. If an import goes over the limit, the dashboard warns you before applying it.

{% hint style="info" %}
After pasting a `.env`, review the list and click **Save**. Importing alone doesn't save anything.
{% endhint %}

***

## 🔄 Apply the changes

Saving in the dashboard **stores** the variables, but the running application keeps the old values until a **rebuild** or a new **deploy**.

{% stepper %}
{% step %}
**Save at the right level**

Edit and save on the app, the project or the account.
{% endstep %}

{% step %}
**Rebuild or deploy**

On the app, click **Rebuild** or make a new [commit](../../faq/general-questions/how-to-commit.md).
{% endstep %}

{% step %}
**Check the logs**

Check the [logs](../../faq/general-questions/how-to-access-the-application-logs.md) to see if the app started with the expected behavior.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Account or project variables affect **every** app at that level. After changing them, rebuild or deploy each app that needs the new value.
{% endhint %}

***

## 🏗️ `BUILD_` prefix

By default, variables are only available once the app is running.

Frameworks like Vite, Next.js, Nuxt, Astro, React, Vue, Svelte and Angular often need values **during the build**. In those cases, add the variable with the `BUILD_` prefix.

| In the dashboard         | During the build and at runtime |
| ------------------------ | ------------------------------- |
| `BUILD_VITE_API_URL`     | `VITE_API_URL`                  |
| `BUILD_NEXT_PUBLIC_SITE` | `NEXT_PUBLIC_SITE`              |

<figure><img src="../../.gitbook/assets/env-vars-build-prefix.png" alt="Diagram of the BUILD_ prefix being removed during the build"><figcaption></figcaption></figure>

The `BUILD_` prefix is just a Discloud marker. It is **removed automatically** during the build, and the application **never** sees the name with `BUILD_`.

Only use `BUILD_` when the value must exist during the build. Secrets that your API only uses at runtime can go without the prefix.

***

## 💡 Best practices

* Use names in `UPPERCASE_WITH_UNDERSCORES`.
* Only put truly global values on the **account**, like a token used by all your bots.
* Put on the **project** what the group of apps shares, like the internal database URL or the product's API key.
* Put on the **app** what is specific to it, like that bot's webhook or a feature flag.
* Avoid reusing the same name at different levels by accident. The app value hides the project value without any warning.
* Don't keep secrets in [`discloud.config`](../../configurations/discloud.config/). Use the dashboard.

To automate it, see the [Environment variable API](../../api-and-integrations/api-overview/environment-variable.md).
