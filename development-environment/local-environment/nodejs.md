---
description: >-
  Install and manage Node.js locally (Windows, macOS, Linux) using an installer,
  package manager, or version manager.
icon: node-js
---

# Node.js

## 🧾 Overview

Node.js runs JavaScript outside the browser for CLIs, APIs, workers, scheduled tasks, and real‑time services. Local installation lets you:

* Install dependencies (npm, pnpm, or Yarn)
* Run and debug before deploying to Discloud
* Prepare builds or bundles where needed

{% embed url="https://nodejs.org/" %}

***

## 📥 Installation

Pick your operating system, then one method. Version managers (NVM) help when switching projects.

{% tabs %}
{% tab title="🪟 Windows" %}
{% tabs %}
{% tab title="Installer" %}
{% stepper %}
{% step %}
Open [https://nodejs.org/en/download](https://nodejs.org/en/download) and download the LTS .msi
{% endstep %}

{% step %}
Run installer (keep defaults incl. npm + PATH)
{% endstep %}

{% step %}
Reopen terminal & verify

```bash
node -v
npm -v
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Chocolatey" %}
```bash
choco install nodejs-lts -y
node -v
npm -v
```
{% endtab %}

{% tab title="NVM for Windows" %}
{% stepper %}
{% step %}
Download latest `nvm-setup.exe` from [releases](https://github.com/coreybutler/nvm-windows/releases)
{% endstep %}

{% step %}
Install accepting defaults
{% endstep %}

{% step %}
Install & use LTS

```bash
nvm install lts 
nvm use lts 
node -v 
npm -v
```
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🐧 Linux" %}
{% tabs %}
{% tab title="Debian/Ubuntu" %}
```bash
sudo apt update
sudo apt install -y nodejs npm
node -v
npm -v
```
{% endtab %}

{% tab title="Fedora" %}
```bash
sudo dnf install -y nodejs npm
node -v
npm -v
```
{% endtab %}

{% tab title="Arch" %}
```bash
sudo pacman -S --needed nodejs-lts-jod npm
node -v
npm -v
```
{% endtab %}

{% tab title="NVM" %}
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
source ~/.bashrc 2>/dev/null || source ~/.zshrc 2>/dev/null
nvm install --lts
nvm use --lts
nvm alias default lts/*
node -v
npm -v
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🍎 macOS" %}
{% tabs %}
{% tab title="Installer" %}
Download LTS .pkg from [nodejs.org](https://nodejs.org/en/download) then:

```bash
node -v
npm -v
```
{% endtab %}

{% tab title="Homebrew" %}
```bash
brew update
brew install node
node -v
npm -v
```
{% endtab %}

{% tab title="NVM" %}
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
source ~/.zshrc 2>/dev/null || source ~/.bashrc 2>/dev/null
nvm install --lts
nvm use --lts
node -v
npm -v
```
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## 🔄 Updating Node.js

If you're using **NVM**, you can update Node.js with:

```bash
nvm install --lts
```

On NVM for Windows, use `nvm install lts`.

Otherwise, use your system's package manager or re-download the latest installer from the Node.js website.
