---
description: List of all Discloud Bot commands on Discord.
icon: list
---

# Bot Commands

The Discloud Bot uses **slash commands**. Type `/` in the [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) channel on the **Discloud Discord Server** and pick the command from the list Discord shows.

{% hint style="info" %}
To use the commands, your account must be verified on the server. See how on [**Discord Bot**](./).
{% endhint %}

{% hint style="info" %}
In commands that take the `app` option, enter the **application ID**, or `all` to apply it to all your applications. Example: `/reiniciar app:all`.
{% endhint %}

***

## 🚀 Hosting

| Command     | What it does                                                                                           |
| ----------- | ------------------------------------------------------------------------------------------------------ |
| `/upconfig` | Uploads an application using the [`discloud.config`](../../configurations/discloud.config/) file.      |
| `/up`       | Uploads an application with a guided setup.                                                            |
| `/upsite`   | Uploads a website.                                                                                     |
| `/commit`   | Updates your application files. See [**How to commit?**](../../faq/general-questions/how-to-commit.md) |

### 📤 During an upload

| Command     | What it does                                                      |
| ----------- | ----------------------------------------------------------------- |
| `/cancelar` | Cancels the upload in progress. Use it inside the upload channel. |
| `/fechar`   | Closes the upload channel.                                        |

***

## ⚙️ Managing applications

| Command              | What it does                                                                                               |
| -------------------- | ---------------------------------------------------------------------------------------------------------- |
| `/apps`              | Lists the applications you have hosted.                                                                    |
| `/status (ID)`       | Shows the status of an application.                                                                        |
| `/logs`              | Shows the logs of your application.                                                                        |
| `/iniciar app:all`   | Starts your application.                                                                                   |
| `/parar app:all`     | Stops your application.                                                                                    |
| `/reiniciar app:all` | Restarts your application.                                                                                 |
| `/memoria`           | Changes the maximum RAM an application can use.                                                            |
| `/autorestart`       | Enables or disables the application's autorestart.                                                         |
| `/version`           | Changes the [language version](../../configurations/discloud.config/versions.md) used by your application. |
| `/apt`               | Installs [packages](../../configurations/discloud.config/apt.md) on your application's Linux instance.     |
| `/backup`            | Backs up your application's files.                                                                         |
| `/restorepoints`     | Creates restore points for an application.                                                                 |
| `/resetweek`         | Resets the time until your application shuts down.                                                         |
| `/removerapp (ID)`   | Deletes the application, removing all its data and settings.                                               |

{% hint style="danger" %}
**`/removerapp` is permanent.** Run `/backup` first if you want to keep the files.
{% endhint %}

***

## 🌐 Domains and subdomains

| Command       | What it does                                                                                              |
| ------------- | --------------------------------------------------------------------------------------------------------- |
| `/subdominio` | Registers or removes a [subdomain](../../faq/general-questions/how-to-create-a-subdomain.md) on Discloud. |
| `/dominio`    | Manages your [custom domain](../../api-and-integrations/custom-domain.md).                                |

{% hint style="info" %}
We recommend managing domains and subdomains on the [**Discloud website**](https://discloud.com/dashboard), which has better integration than the bot commands.
{% endhint %}

***

## 👥 Team

| Command | What it does                                 |
| ------- | -------------------------------------------- |
| `/mod`  | Manages the moderators of your applications. |

***

## 👤 Account

| Command              | What it does                                                                                                          |
| -------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `/api`               | Generates the [token for using the Discloud API](../../faq/general-questions/how-can-i-get-my-discloud-api-token.md). |
| `/userinfo [userid]` | Shows a client's information.                                                                                         |
| `/planos`            | Shows all available plans and their benefits.                                                                         |
| `/locale`            | Changes the language the Discloud Bot answers you in.                                                                 |
| `/cleardm`           | Deletes all messages the bot sent in your DMs.                                                                        |

***

## 🧰 Other

| Command | What it does                              |
| ------- | ----------------------------------------- |
| `/help` | Shows the help message with the commands. |
| `/ping` | Shows the latency.                        |

***

## ❓ Still need help?

Use `/help` on Discord or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
