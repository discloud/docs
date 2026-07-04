---
description: >-
  Complete reference for the Discloud REST API: authentication, endpoints, and
  resource groups.
icon: webhook
---

# API Overview

### 🌐 Base URL

All requests point to:

```
https://api.discloud.app/v2
```

***

### 🔑 Authentication

Every request requires the `api-token` header with your personal token:

```bash
api-token: YOUR_TOKEN_HERE
```

See [Authentication](./#authentication) to learn how to obtain and protect your token.

***

### ⚡ Quick Start

{% stepper %}
{% step %}
Get your API token from the Dashboard.
{% endstep %}

{% step %}
Make your first request to confirm the token works:

```bash
curl -X GET \
  -H "api-token: YOUR_TOKEN_HERE" \
  https://api.discloud.app/v2/user
```

A `200 OK` response with your user data confirms authentication is working.
{% endstep %}
{% endstepper %}

{% hint style="danger" %}
Never expose your token in public code or Git repositories. Store it in environment variables. See [Authentication](./#authentication) for security best practices.
{% endhint %}
