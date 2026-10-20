---
description: Checklist for when your website or API hosted on Discloud doesn't load.
---

# Why can't I access my website?

If your website or API address doesn't load, go through the items below. In most cases, the problem is one of them.

***

## ✅ Checklist

{% stepper %}
{% step %}
**Platinum Plan or higher**

Websites and APIs require the [**Platinum Plan or higher**](https://discloud.com/plans).
{% endstep %}

{% step %}
**`TYPE=site` in `discloud.config`**

Your [`discloud.config`](../../configurations/discloud.config/) must have `TYPE=site`. With `TYPE=bot`, the application doesn't get external access.
{% endstep %}

{% step %}
**`ID` set to your registered subdomain**

The `ID` field must contain the name of a [subdomain registered](../general-questions/how-to-create-a-subdomain.md) on your account, **without** `.discloud.app` or `.discloud.dev`:

```ini
TYPE=site
ID=myapp
```
{% endstep %}

{% step %}
**The right address: `.discloud.app` or `.discloud.dev`**

Discloud subdomains can be on `.discloud.app` or `.discloud.dev`. You don't choose which: the domain is chosen automatically by Discloud when the subdomain is created. Check the domains section of the [**Dashboard**](https://discloud.com/dashboard) to see your subdomain's address, and open that one.
{% endstep %}

{% step %}
**Port 8080 and host 0.0.0.0**

Your application must listen on port **`8080`** and host **`0.0.0.0`**. If it listens on another port or on `localhost`/`127.0.0.1`, traffic can't reach it.
{% endstep %}

{% step %}
**Enough RAM**

Websites need at least **512MB** of RAM.
{% endstep %}

{% step %}
**Application online**

Check that the application started without errors. If it crashed or stopped, the website won't load. See [**How to access the application logs?**](../general-questions/how-to-access-the-application-logs.md).
{% endstep %}
{% endstepper %}

***

## 🌍 Using a custom domain?

If the problem only happens on your own domain (and the Discloud subdomain works), check your DNS setup in [**Custom Domain**](../../api-and-integrations/custom-domain.md).

***

## 📚 See also

* [**Websites & APIs**](../../how-to-host/websites-and-apis.md)
* [**How to create a subdomain?**](../general-questions/how-to-create-a-subdomain.md)
* [**Diagnosing Offline Applications**](diagnosing-offline-applications.md)

***

## ❓ Still need help?

See [**Troubleshooting Solutions**](./) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
