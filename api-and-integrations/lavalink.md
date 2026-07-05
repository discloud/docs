---
description: Step-by-step guide to host a Lavalink audio server on Discloud.
icon: music
tags:
  - new
---

# Lavalink

### 🎵 What is Lavalink?

**Lavalink** is a standalone audio streaming server used by Discord music bots to play audio from sources like YouTube, SoundCloud, Bandcamp, Twitch, and more. Instead of handling audio directly inside the bot, Lavalink offloads all the heavy audio processing to a dedicated server.

Lavalink runs as a **Java application** and exposes a WebSocket API that your bot connects to.

***

### ✅ Requirements

{% hint style="success" %}
[**Platinum Plan or Higher**](https://discloud.com/plans) – Required for all `TYPE=site` applications.
{% endhint %}

{% hint style="success" %}
[**Subdomain**](../faq/general-questions/how-to-create-a-subdomain.md) – You must register a unique subdomain on Discloud.
{% endhint %}

{% hint style="danger" %}
**Port 8080 & Host 0.0.0.0** – Your application **must** listen on port `8080` and host `0.0.0.0` to be accessible externally.
{% endhint %}

{% hint style="info" %}
**RAM** – A minimum of **512MB** is recommended for web applications.
{% endhint %}

***

### 🚀 Step-by-Step Setup

{% stepper %}
{% step %}
**⬇️ Download `Lavalink.jar`**

Download the latest stable release of Lavalink from the official GitHub repository:

👉 [https://github.com/lavalink-devs/Lavalink/releases](https://github.com/lavalink-devs/Lavalink/releases)

Download the file named `Lavalink.jar` from the Assets section of the latest release.
{% endstep %}

{% step %}
**📝 Create `application.yml`**

Create a file named `application.yml` in the same folder as `Lavalink.jar`. This is the main configuration file for Lavalink.

{% code title="application.yml" expandable="true" %}
```yaml
server:
  port: 8080
  address: 0.0.0.0

lavalink:
  server:
    password: "youshallnotpass"
    sources:
      youtube: false
      bandcamp: true
      soundcloud: true
      twitch: true
      vimeo: true
      http: true
      local: false

  plugins:
    # Replace VERSION with the current version as shown by the Releases tab or a long commit hash for snapshots.
    - dependency: "dev.lavalink.youtube:youtube-plugin:VERSION"
      snapshot: false

plugins:
  youtube:
    enabled: true
    allowSearch: true
    allowDirectVideoIds: true
    allowDirectPlaylistIds: true
    oauth:
      enabled: true

logging:
  level:
    root: INFO
    lavalink: INFO
```
{% endcode %}

{% hint style="danger" %}
**Set `server.port` to `8080`** - This is required for Discloud to route external traffic correctly.

**Set `server.address` to `0.0.0.0`** - This allows external connections to reach Lavalink.
{% endhint %}

{% hint style="warning" %}
**Change the password** - Replace `"youshallnotpass"` with a strong, unique password. Anyone who knows your password can use your Lavalink server.
{% endhint %}

{% hint style="info" %}
**YouTube plugin** - The `youtube: false` setting under `sources` disables the built-in (deprecated) YouTube source. The `youtube-plugin` listed under `plugins` replaces it with a more up-to-date implementation. Check the [plugin releases page](https://github.com/lavalink-devs/youtube-source/releases) for the latest version number.
{% endhint %}
{% endstep %}

{% step %}
**⚙️ Create `discloud.config`**

Create a [`discloud.config`](https://github.com/discloud/docs/blob/english/configurations/discloud.config) file in the same folder:

```ini
NAME=MyLavalink
TYPE=site
MAIN=Lavalink.jar
RAM=512
VERSION=17.x.x
ID=my-lavalink-subdomain
```

* **`TYPE=site`** - Required because Lavalink listens on a network port.
* **`MAIN=Lavalink.jar`** - Must match the exact filename of the JAR.
* **`VERSION=17.x.x`** - Lavalink 4.x requires Java 17. Use `17.x.x` or `latest`.
* **`ID`** - Your registered subdomain (without `.discloud.app`).
{% endstep %}

{% step %}
**📦 Create the ZIP file**

Your folder should contain exactly these three files:

```
lavalink-upload/
├─ Lavalink.jar
├─ application.yml
└─ discloud.config
```

Compress these files into a `.zip` archive. Make sure the files are [**at the root**](../faq/general-questions/what-is-the-root-of-the-project.md) of the ZIP, do not compress a folder.
{% endstep %}

{% step %}
**🚀 Upload to Discloud**

{% content-ref url="https://app.gitbook.com/s/ETNoAt35DpCBhinHpaRx/how-to-host" %}
[How To Host](https://app.gitbook.com/s/ETNoAt35DpCBhinHpaRx/how-to-host)
{% endcontent-ref %}
{% endstep %}

{% step %}
**🤖 Configure your bot**

Connect your Discord bot to Lavalink using your subdomain. Since Discloud uses HTTPS/WSS with a reverse proxy, you must connect on **port 443 with `secure: true`**.

```json
{
  "host": "my-lavalink-subdomain.discloud.app",
  "port": 443,
  "secure": true,
  "password": "youshallnotpass"
}
```

Replace `my-lavalink-subdomain` with your actual subdomain and `youshallnotpass` with the password you set in `application.yml`.

{% hint style="warning" %}
Do **not** connect on port `8080` from your bot. Port `8080` is only for internal use by Discloud. Your bot must always connect on port `443` with `secure: true`.
{% endhint %}
{% endstep %}
{% endstepper %}

***

### 🔗 Connecting a YouTube Account (OAuth2)

By default, Lavalink may display a login prompt in the logs asking you to authorize a YouTube account. This is required to avoid YouTube throttling and playback errors.

{% hint style="info" %}
If you enabled `oauth.enabled: true` in your `application.yml`, Lavalink will automatically generate a device authorization URL on the first startup.
{% endhint %}

{% stepper %}
{% step %}
**📋 Start Lavalink and check the logs**

After uploading and starting your Lavalink instance, check the application logs. Look for a message similar to:

```
Please navigate to https://www.youtube.com/device?user_code=XXXX-XXXX and grant access.
```
{% endstep %}

{% step %}
**🔑 Authorize the YouTube account**

Open the URL from the logs in your browser (e.g., `https://www.youtube.com/device?user_code=XXXX-XXXX`).

Sign in with the Google / YouTube account you want Lavalink to use. A personal account works fine, a dedicated account is recommended.

{% hint style="warning" %}
You must complete this step **before the code expires** (usually within a few minutes). If it expires, restart Lavalink to generate a new code.
{% endhint %}
{% endstep %}

{% step %}
**✅ Confirm authorization**

After granting access, return to your Lavalink logs. You should see a message confirming the authorization was successful:

```
YouTube token refreshed successfully.
```

Lavalink will save the token and reuse it automatically on future restarts. You do not need to repeat this process unless you revoke the access or change the account.
{% endstep %}
{% endstepper %}
