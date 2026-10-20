---
description: >-
  Instale e gerencie PHP e Composer localmente (Windows, macOS, Linux) usando
  instaladores ou gerenciadores de pacotes; gerencie dependências com
  composer.json.
icon: php
---

# PHP

## 🧾 Visão Geral

PHP é usado em sites, APIs e bots. A instalação local permite:

* Executar e testar seu projeto antes de fazer o upload na Discloud
* Instalar dependências com o Composer
* Gerar o `composer.lock` para que a Discloud instale as mesmas versões que você testou

{% embed url="https://www.php.net/" %}

{% hint style="info" %}
Veja [PHP](../supported-languages/php/) para os detalhes de hospedagem e [composer.json](../supported-languages/php/composer.json.md) para o gerenciamento de dependências na Discloud.
{% endhint %}

***

## 📥 Instalação

Instale primeiro o **PHP** e depois o **Composer** (o gerenciador de dependências do PHP).

{% tabs %}
{% tab title="🪟 Windows" %}
{% tabs %}
{% tab title="ZIP oficial" %}
{% stepper %}
{% step %}
Baixe o ZIP **Thread Safe** mais recente em [https://windows.php.net/download](https://windows.php.net/download)
{% endstep %}

{% step %}
Extraia (ex.: em `C:\php`), copie `php.ini-development` para `php.ini` e adicione `C:\php` ao PATH
{% endstep %}

{% step %}
Reabra o terminal e verifique

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

**Composer:** baixe e execute o [`Composer-Setup.exe`](https://getcomposer.org/download/) e depois:

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

## 🧪 Fluxo Mínimo

{% stepper %}
{% step %}
Crie um `composer.json` (ou use o do seu projeto)

```bash
composer init
```
{% endstep %}

{% step %}
Instale as dependências

```bash
composer install
```
{% endstep %}

{% step %}
Execute o projeto localmente

```bash
# Script ou bot
php index.php
# Site: servidor de desenvolvimento embutido
php -S 0.0.0.0:8080
```
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Não inclua a pasta `vendor/` no seu `.zip`: envie o `composer.json` (e o `composer.lock`) para que as dependências sejam instaladas na Discloud.
{% endhint %}

***

## 🔄 Atualização

| Tarefa                       | Comando                          |
| ---------------------------- | -------------------------------- |
| Atualizar dependências       | `composer update`                |
| Atualizar um único pacote    | `composer update vendor/package` |
| Atualizar o próprio Composer | `composer self-update`           |
| Atualizar o PHP (Homebrew)   | `brew upgrade php`               |

***

## 🗃 Comandos Comuns

```bash
php -v
php -m
composer init
composer require vendor/package
composer install
composer update
composer dump-autoload
```
