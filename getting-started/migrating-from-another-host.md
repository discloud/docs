---
description: >-
  How to bring a bot, website or API from another host to Discloud, with the
  equivalent of each setting.
icon: truck-arrow-right
---

# Migrating from Another Host

If your application already runs on another host, migrating is usually quick. Most of the work is translating the configuration into [`discloud.config`](../configurations/discloud.config/).

***

## 🔁 Equivalents

| On the other host                       | On Discloud                                                                                                          |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `Procfile` with `worker: node index.js` | `TYPE=bot` and `MAIN=index.js` in `discloud.config`                                                                  |
| `Procfile` with `web: ...`              | `TYPE=site` and a [subdomain](../faq/general-questions/how-to-create-a-subdomain.md), with the server on port `8080` |
| Build command                           | `BUILD` option in `discloud.config`                                                                                  |
| Start command                           | `START` option in `discloud.config`                                                                                  |
| Dashboard environment variables         | Discloud [environment variables](../platform-features/environment-variables.md)                                      |
| Runtime version                         | `VERSION` option in `discloud.config`                                                                                |
| System packages                         | [`APT`](../configurations/discloud.config/apt.md) option in `discloud.config`                                        |
| Your own domain                         | [Custom domain](../platform-features/custom-domain.md)                                                               |

***

## 🚀 Step by step

{% stepper %}
{% step %}
**Create the `discloud.config`**

In the [project root](../faq/general-questions/what-is-the-root-of-the-project.md), create `discloud.config` with the type, main file and RAM. Use the equivalents above.
{% endstep %}

{% step %}
**Bring the variables**

Copy the environment variables from the old host. In the Discloud dashboard, the **Paste .env** option imports several at once.
{% endstep %}

{% step %}
**Adjust the port (websites and APIs)**

The server must listen on port `8080`.
{% endstep %}

{% step %}
**Upload**

Compress the project without folders like `node_modules` and upload it with the method you prefer. See [Bots](bots.md) and [Websites & APIs](websites-and-apis.md) for the step by step.
{% endstep %}

{% step %}
**Turn off the old host**

Once the application runs on Discloud, turn off the old one. A Discord bot running in two places with the same token responds twice.
{% endstep %}
{% endstepper %}
