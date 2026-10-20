---
description: >-
  Install and manage PHP and Composer locally (Windows, macOS, Linux) using
  installers or package managers; manage dependencies with composer.json.
icon: php
---

# PHP

## 🧾 Overview

PHP powers websites, APIs, and bots. A local installation lets you:

* Run and test your project before uploading it to Discloud
* Install dependencies with Composer
* Generate `composer.lock` so Discloud installs the same versions you tested

{% embed url="https://www.php.net/" %}

{% hint style="info" %}
See [PHP](../supported-languages/php/) for hosting details and [composer.json](../supported-languages/php/composer.json.md) for dependency management on Discloud.
{% endhint %}

***

## 📥 Installation

Install **PHP** first, then **Composer** (PHP's dependency manager).

{% tabs %}
{% tab title="🪟 Windows" %}
{% tabs %}
{% tab title="Official ZIP" %}
{% stepper %}
{% step %}
Download the latest **Thread Safe** ZIP from [https://windows.php.net/download](https://windows.php.net/download)
{% endstep %}

{% step %}
Extract it (e.g. to `C:\php`), copy `php.ini-development` to `php.ini`, and add `C:\php` to your PATH
{% endstep %}

{% step %}
Reopen the terminal and verify

```bash
php -v
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="winget" %}
```bash
winget install PHP.PHP.8.3
php -v
```
{% endtab %}

{% tab title="Chocolatey" %}
```bash
choco install php -y
php -v
```
{% endtab %}
{% endtabs %}

**Composer:** download and run [`Composer-Setup.exe`](https://getcomposer.org/download/), then:

```bash
composer --version
```
{% endtab %}

{% tab title="🐧 Linux" %}
{% tabs %}
{% tab title="Debian/Ubuntu" %}
```bash
sudo apt update
sudo apt install -y php-cli php-mbstring php-xml php-curl php-zip unzip composer
php -v
composer --version
```
{% endtab %}

{% tab title="Fedora" %}
```bash
sudo dnf install -y php-cli php-mbstring php-xml composer
php -v
composer --version
```
{% endtab %}

{% tab title="Arch" %}
```bash
sudo pacman -S --needed php composer
php -v
composer --version
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🍎 macOS" %}
{% tabs %}
{% tab title="Homebrew" %}
```bash
brew update
brew install php composer
php -v
composer --version
```
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## 🧪 Minimal Workflow

{% stepper %}
{% step %}
Create a `composer.json` (or use the one from your project)

```bash
composer init
```
{% endstep %}

{% step %}
Install the dependencies

```bash
composer install
```
{% endstep %}

{% step %}
Run the project locally

```bash
# Script or bot
php index.php
# Website: built-in development server
php -S 0.0.0.0:8080
```
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Don't include the `vendor/` folder in your `.zip`: send `composer.json` (and `composer.lock`) so the dependencies are installed on Discloud.
{% endhint %}

***

## 🔄 Updating

| Task                    | Command                          |
| ----------------------- | -------------------------------- |
| Update dependencies     | `composer update`                |
| Update a single package | `composer update vendor/package` |
| Update Composer itself  | `composer self-update`           |
| Update PHP (Homebrew)   | `brew upgrade php`               |

***

## 🗃 Common Commands

```bash
php -v
php -m
composer init
composer require vendor/package
composer install
composer update
composer dump-autoload
```
