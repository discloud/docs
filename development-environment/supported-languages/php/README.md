---
description: Complete guide to host PHP applications on Discloud.
icon: php
---

# Php

## 📁 **Preparing Your Project Files**

If your project uses Composer, ensure a valid [`composer.json`](composer.json.md) is at the **root** of the archive you upload. Discloud will install dependencies automatically when it detects this file.

#### ❌ **Files / Directories to Exclude**

Exclude items that are not required for runtime:

```diff
- vendor/
- node_modules/
- .git/
- tests/
- .cache/
```

📌 Use a [**`.discloudignore`**](../../../configurations/.discloudignore.md) file to exclude directories you do **not** want packed (e.g. `vendor/` if you prefer a clean install).

{% hint style="info" %}
Include `vendor/` ONLY if: you have patched libraries locally or you rely on extensions or binaries compiled during install that must match your dev environment. Otherwise excluding it keeps uploads smaller and lets Discloud perform a fresh, reproducible install.
{% endhint %}

🔗 Need to define your **main file**? See: [**Main File FAQ**](../../../faq/general-questions/what-is-the-main-file.md)

***

## 📦 **composer.json Essentials**

Minimal example:

```json
{
  "name": "example/app",
  "type": "project",
  "require": {
    "guzzlehttp/guzzle": "^7.9"
  },
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  },
  "scripts": {
    "start": "php -S 0.0.0.0:8080 -t public"
  }
}
```

After editing dependencies locally:

```bash
composer install
composer dump-autoload --optimize
```

More details: [`composer.json`](composer.json.md)

***

## 🌐 **Hosting Websites & APIs**

Before deploying your website or API on Discloud, ensure that you meet the following **requirements**:

{% hint style="success" %}
[Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](../../../faq/general-questions/how-to-create-a-subdomain.md) before deployment.
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – Applications must listen on this port.
{% endhint %}

{% tabs %}
{% tab title="Built-in Server" %}
Run locally / simple deploy:

```bash
php -S 0.0.0.0:8080 -t public
```

`public/index.php` minimal:

```php
<?php
declare(strict_types=1);
echo "Hello, Discloud!";
```
{% endtab %}

{% tab title="Basic Router" %}
`public/index.php`:

```php
<?php
declare(strict_types=1);
$path = parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH);
header('Content-Type: application/json');
if ($path === '/status') {
    echo json_encode(['ok' => true]);
    return;
}
echo json_encode(['message' => 'Hello, Discloud!']);
```
{% endtab %}

{% tab title="Composer Script" %}
Add to `composer.json`:

```json
{
  "scripts": { "start": "php -S 0.0.0.0:8080 -t public" }
}
```

Run:

```bash
composer run-script start
```
{% endtab %}
{% endtabs %}

***

## ✍️ **Deploying Your Application**

Once your project is **configured and compressed**, you can choose one of the following **deployment methods** on Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Upload and manage your application via the web interface.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Deploy directly through Discloud’s Discord bot commands.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integrate with VS Code for seamless project management.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use the command-line interface for quick and efficient deployment.</td><td></td><td></td><td></td></tr></tbody></table>
