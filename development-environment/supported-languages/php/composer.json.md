---
description: >-
  Understand and configure composer.json so Discloud can install your PHP
  dependencies automatically.
---

# composer.json

## 🗂 What is `composer.json`?

`composer.json` declares your project's metadata, required packages, autoload rules, and optional scripts. When present at the root of the archive you upload, Discloud installs the dependencies defined inside using Composer.

***

## 🛠 Creating `composer.json`

{% stepper %}
{% step %}
Generate interactively:

```bash
composer init
```
{% endstep %}

{% step %}
Or create a minimal file manually:

```json
{
  "name": "example/app",
  "type": "project",
  "require": {
    "guzzlehttp/guzzle": "^7.9"
  },
  "autoload": {
    "psr-4": { "App\\": "src/" }
  }
}
```
{% endstep %}

{% step %}
Then install:

```bash
composer install
```
{% endstep %}
{% endstepper %}

***

## 📦 Adding / Updating Dependencies

Install new package:

```bash
composer require ramsey/uuid
```

Update one package:

```bash
composer update ramsey/uuid
```

Update all (may change versions broadly):

```bash
composer update
```

***

## 📄 Lock File (`composer.lock`)

Commit `composer.lock` so deployments reproduce the exact dependency versions. If absent, latest matching versions are resolved during install.

***

## 🧰 Common Commands Reference

```bash
# Init project
composer init

# Install deps
composer install

# Remove package
composer remove vendor/pkg

# Optimize autoload
composer dump-autoload --optimize

# Run script
composer run-script <name>

# Show outdated
composer outdated
```
