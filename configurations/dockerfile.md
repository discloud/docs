---
description: How to create a Dockerfile compatible with Discloud
icon: docker
---

# Dockerfile

## 🐳 What it is

With a `Dockerfile`, you can host almost anything on Discloud. You define the application environment: runtime, dependencies, start command, and whatever the image needs to run.

That gives you freedom to mix stacks, tools, and setups that the default language flow does not cover. At the same time, you still use what Discloud already provides: dashboard, variables, volume, domain, and the rest of the platform.

The app main file becomes the `Dockerfile` (`MAIN=Dockerfile`).

{% hint style="info" %}
**Golden rule:** `MAIN=Dockerfile` · code in the image (e.g. `/app`) owned by **1000** · data in the `/home/discloud` volume · sites on public port **8080**.
{% endhint %}

***

## 📋 Requirements

For the app to use the Dockerfile flow, you must meet these criteria:

{% hint style="success" %}
`Dockerfile` file – In the project root (or the path you point to), with a capital D.
{% endhint %}

{% hint style="success" %}
`MAIN=Dockerfile` – In `discloud.config`, or select `Dockerfile` as the main file in the dashboard.
{% endhint %}

{% hint style="success" %}
UID 1000 – The process and the code and volume folders must belong to user **1000**.
{% endhint %}

{% hint style="success" %}
`CMD` or `ENTRYPOINT` – The image must define how the app starts.
{% endhint %}

{% hint style="warning" %}
Sites on port 8080 – If the app is hosted as a **site**, the public port is **8080**. Another port will not open on the subdomain or custom domain.
{% endhint %}

***

## 📄 discloud.config

In `discloud.config`, the main file must be the Dockerfile:

{% code title="discloud.config" %}
```properties
NAME=My App
TYPE=site
MAIN=Dockerfile
RAM=512
ID=my-app
```
{% endcode %}

| Key    | Required    | Purpose                                 |
| ------ | ----------- | --------------------------------------- |
| `MAIN` | Required    | Must be `Dockerfile` to enter this flow |
| `TYPE` | Recommended | `site` or `bot` (default: `bot`)        |
| `ID`   | Sites       | Site subdomain                          |
| `RAM`  | Recommended | For sites, practical minimum 512 MB     |

{% hint style="info" %}
Without `MAIN=Dockerfile`, Discloud does not use the Dockerfile flow. In the dashboard, the equivalent is selecting **Dockerfile** as the main file. General file details are in [discloud.config](discloud.config/).
{% endhint %}

For a bot / worker:

{% code title="discloud.config" %}
```properties
NAME=My Bot
TYPE=bot
MAIN=Dockerfile
RAM=100
```
{% endcode %}

***

## 👤 User 1000 and folder permissions

Discloud starts the container as `1000:1000`. That requires three things at once:

1. The process runs as UID **1000** (`USER 1000`)
2. The folder where the code is **copied and executed** (e.g. `/app`) belongs to **1000**
3. The `/home/discloud` volume also belongs to **1000**, so the app can write data

`/app` is only an example path. It can be another directory, **as long as it is not** `/home/discloud` and has **1000** permission.

```dockerfile
RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 . .

USER 1000
```

{% hint style="info" %}
`USER 1000` alone is not enough. The code folder (where `WORKDIR` points and from where `CMD` runs) must belong to UID 1000. Without that, the app fails with a permission error.
{% endhint %}

{% hint style="warning" %}
Use `chown -R 1000:1000` on the folders and `COPY --chown=1000:1000` on the files. `Permission denied` is the most common error when this is missing.
{% endhint %}

{% hint style="info" %}
On images that already have UID 1000 (e.g. `node:*`), `getent` avoids a `UID is not unique` error. What matters is that the code folder and the volume are owned by **1000**.
{% endhint %}

***

## 🌐 Port 8080 (sites)

If you host the app as a **site**, the port you must use is **8080**.

Discloud connects port **8080** to the subdomain or custom domain. That is the **only port exposed on the public network**.

| Access                             | Port                            | When it works                      |
| ---------------------------------- | ------------------------------- | ---------------------------------- |
| Public (subdomain / custom domain) | **8080**                        | Always, for sites                  |
| Another port (e.g. 3000, 5000)     | Any other                       | **Does not** open on the internet  |
| Internal (VLAN / private network)  | The port the process listens on | Only if VLAN is enabled on the app |

In your code, make the site listen on `0.0.0.0:8080` (or `process.env.PORT` pointing to `8080`).

```dockerfile
ENV PORT=8080
```

{% hint style="danger" %}
If the site listens on another port, the public domain **does not work**. That other port would only be reachable internally through the [private network (VLAN)](../platform-features/vlan.md), and only if the app has VLAN enabled.
{% endhint %}

For **bots** (no public HTTP site), port 8080 is not required. The other rules still apply.

***

## ▶️ CMD or ENTRYPOINT

Discloud starts the process defined in the image. Without a valid `CMD` or `ENTRYPOINT`, the app does not start.

```dockerfile
CMD ["node", "server.js"]
```

The command must point to the code in the image folder (e.g. `/app`), not to the volume.

***

## 📦 Volume (`/home/discloud`)

Think of these as two different places:

| Place                         | What for                           | Persists?                             |
| ----------------------------- | ---------------------------------- | ------------------------------------- |
| **Image** (e.g. `/app`)       | Code and dependencies that **run** | Recreated on image rebuild            |
| **Volume** (`/home/discloud`) | Data the app **saves** at runtime  | **Yes**: survives restart and rebuild |
| **Any other path**            | Temporary                          | **No**: gone on rebuild               |

The volume is **not** where the code that will run should live. It is where the application, **once running**, writes what must keep existing (uploads, generated files, embedded databases, etc.).

| Moment                                          | What happens in `/home/discloud`                      |
| ----------------------------------------------- | ----------------------------------------------------- |
| **At build** (`COPY` / `RUN` in the Dockerfile) | What you put there **does not stick**.                |
| **With the app running**                        | What the app **creates or saves** there **persists**. |

{% hint style="danger" %}
`COPY index.js /home/discloud/` in the Dockerfile **does not** make `index.js` exist at startup. Code in the image (e.g. `/app`); volume only for data.
{% endhint %}

Separation example:

```dockerfile
RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 . .

USER 1000
CMD ["node", "index.js"]
```

In your application code, write what needs to persist under `/home/discloud`, for example `/home/discloud/uploads`.

***

## 🔐 Environment variables

Set tokens, URLs, and secrets in the **Discloud dashboard**. The app reads those variables at runtime.

{% hint style="info" %}
For apps with a **custom Dockerfile**, use dashboard variables for runtime. The dashboard `BUILD_` prefix is **not** injected into your Dockerfile build. Anything the image needs at build time must be in the Dockerfile itself.
{% endhint %}

See also [Environment Variables](../platform-features/environment-variables.md).

***

## 🧪 Examples

{% tabs %}
{% tab title="Node.js (site)" %}
```dockerfile
FROM node:20-slim

RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 package*.json ./
RUN npm ci --omit=dev
COPY --chown=1000:1000 . .

USER 1000
ENV PORT=8080

CMD ["node", "server.js"]
```
{% endtab %}

{% tab title="Python / FastAPI (site)" %}
```dockerfile
FROM python:3.12-slim

RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY --chown=1000:1000 . .

USER 1000
ENV PORT=8080

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
```
{% endtab %}

{% tab title="Bot / worker" %}
```dockerfile
FROM python:3.12-slim

RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY --chown=1000:1000 . .

USER 1000

CMD ["python", "bot.py"]
```
{% endtab %}
{% endtabs %}

***

## 🛠️ Common issues

| Problem                               | Likely cause                             | Fix                                                                    |
| ------------------------------------- | ---------------------------------------- | ---------------------------------------------------------------------- |
| App did not enter the Dockerfile flow | Wrong or missing `MAIN`                  | `MAIN=Dockerfile` in `discloud.config` (or select it in the dashboard) |
| Site does not open                    | Not listening on public port 8080        | Listen on `0.0.0.0:8080`; another port does not reach the domain       |
| Permission denied                     | Code folder or volume not owned by 1000  | `chown` + `COPY --chown=1000:1000` + `USER 1000`                       |
| App crashes on start                  | Invalid `CMD`/`ENTRYPOINT` or wrong path | Command pointing to the code in the image                              |
| `COPY` file “vanished”                | It went to `/home/discloud` at build     | Code in the image; volume only for runtime data                        |
| Lost data after rebuild               | Saved outside the volume                 | Write to `/home/discloud` while the app is running                     |

***

## 🚫 What not to do

* Do not use `MAIN=index.js` (or another file) if you want the Dockerfile flow.
* Do not put the executable code in `/home/discloud` in the Dockerfile.
* Do not expect a build-time `COPY` into the volume to appear at startup.
* Do not use a public site port other than **8080**. Only 8080 goes to the subdomain/domain; other ports stay internal only (VLAN, if enabled).
* Do not run as root: the runtime forces UID **1000**.
* Dockerfile apps **do not migrate automatically** between clusters. To change cluster/Project, remove the app and host it again.

***

## ✅ Summary

1. `Dockerfile` file + **`MAIN=Dockerfile`**
2. `CMD` or `ENTRYPOINT` pointing to the code in the image
3. UID **1000** + 1000 permission on the code folder **and** the volume
4. Sites on public port **8080** (the only one exposed to the domain)
5. Code in the image (e.g. `/app`), **never** in the volume
6. Volume `/home/discloud` = where the app **saves** what must live on; what goes there at build time **does not stick**
