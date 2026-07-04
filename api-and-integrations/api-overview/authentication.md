---
description: >-
  Authentication guide for using the Discloud API (how to obtain and safely use
  your API Token).
icon: key-skeleton
---

# Authentication

{% hint style="info" %}
All requests to the Discloud API must include an **API Token** in the `api-token` header.

If you don't have a token yet, generate or retrieve it in your Discloud dashboard. (Replace this note with the exact dashboard link or a screenshot.)
{% endhint %}

***

## ⚙️ How It Works

{% stepper %}
{% step %}
You generate a unique [token](../../faq/general-questions/how-can-i-get-my-discloud-api-token.md) linked to your account.
{% endstep %}

{% step %}
For every HTTP request include the header: `api-token: YOUR_TOKEN_HERE`.
{% endstep %}

{% step %}
The token authenticates and authorizes actions on behalf of your account (never share it).
{% endstep %}

{% step %}
Use the `/user` endpoint to quickly validate the token.
{% endstep %}
{% endstepper %}

***

## 📤 Sending the Token

{% tabs %}
{% tab title="cURL" %}
```bash
curl -X GET \
  -H "api-token: $DISCLOUD_TOKEN" \
  https://api.discloud.app/v2/user
```
{% endtab %}

{% tab title="Node.js (fetch)" %}
```javascript
import fetch from "node-fetch";

async function getCurrentUser() {
  const res = await fetch("https://api.discloud.app/v2/user", {
    headers: { "api-token": process.env.DISCLOUD_TOKEN },
  });

  if (!res.ok) {
    console.error("Request failed:", res.status, await res.text());
    return;
  }
  const data = await res.json();
  console.log(data);
}
```
{% endtab %}

{% tab title="Node.js (discloud.app SDK)" %}
```javascript
// Install first: npm i discloud.app
const { discloud } = require("discloud.app");

async function validateToken() {
  try {
    const user = await discloud.login("DISCLOUD_API_TOKEN");
    console.log("Authenticated user:", user);
  } catch (e) {
    console.error("Invalid token or network error:", e.message);
  }
}
```
{% endtab %}
{% endtabs %}

***

## 🛡 Securing the Token

{% hint style="danger" %}
Never commit your token (e.g. to Git). Store it in environment variables ([`.env`](../../faq/general-questions/.env-file.md), CI/CD secrets, etc.).
{% endhint %}

📌 Best practices:

* Use environment variables instead of hard‑coding.
* Rotate the token periodically (e.g. every 90 days).
* Revoke and regenerate immediately if you suspect exposure.
* Restrict who can access infrastructure where the variable is stored.

***

## ⚡ Quick Token Verification

Call `/user` right after setting the environment variable. If you get HTTP 200 with user data, authentication is working.

{% hint style="info" %}
You can also update the user locale (e.g. `en-US`) through `/locale/{locale}` to validate another authenticated route.
{% endhint %}

***

## 📚 Related Endpoints References

The operations below require the `api-token` header:

{% openapi-operation spec="api-endpoints-en-v2" path="/user" method="get" %}
[OpenAPI api-endpoints-en-v2](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/5e908ec500787544c22c34eb222c247943b9e5fdca814a16353e8c9366fa470b.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260704%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260704T223737Z&X-Amz-Expires=172800&X-Amz-Signature=c06a29c51b23e0e6bdf75a5ec5e76c2a9acc2ee1678b555fea1f9e2538d7c5bc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
