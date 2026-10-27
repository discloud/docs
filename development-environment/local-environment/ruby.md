---
description: >-
  Install and manage Ruby locally (Windows, macOS, Linux) using installers or
  version managers; use Bundler for dependencies.
icon: gem
---

# Ruby

## 🧾 Overview

Ruby is used for bots, APIs (Sinatra), and full frameworks (Rails). Local installation lets you manage gems and test before deploying.

{% embed url="https://www.ruby-lang.org" %}

{% embed url="https://bundler.io/" %}

***

## 📥 Installation (choose one)

{% tabs %}
{% tab title="🪟 Windows" %}
{% stepper %}
{% step %}
Download the latest Ruby+Devkit (x64) from [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)
{% endstep %}

{% step %}
Run installer (enable MSYS2 when prompted).
{% endstep %}

{% step %}
Let post-install script finish (toolchain setup).
{% endstep %}

{% step %}
Verify & install bundler

```bash
ruby -v
gem -v
gem install bundler
bundler -v
```
{% endstep %}

{% step %}
Initialize project (optional)

```bash
bundle init
bundle install
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🐧 Linux" %}
{% tabs %}
{% tab title="Debian/Ubuntu" %}
```bash
sudo apt update
sudo apt install -y ruby-full build-essential
ruby -v
gem -v
gem install bundler
```
{% endtab %}

{% tab title="Fedora" %}
```bash
sudo dnf install -y ruby ruby-devel @development-tools
ruby -v
gem -v
gem install bundler
```
{% endtab %}

{% tab title="Arch" %}
```bash
sudo pacman -S --needed ruby base-devel
ruby -v
gem -v
gem install bundler
```
{% endtab %}

{% tab title="rbenv" %}
Dependencies (Debian example):

```bash
sudo apt update
sudo apt install -y build-essential libssl-dev libreadline-dev zlib1g-dev \
libyaml-dev libffi-dev libgdbm-dev libncurses5-dev libsqlite3-dev
```

Install rbenv + ruby-build:

```bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
rbenv install 3.3.0
rbenv global 3.3.0
ruby -v
gem install bundler
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🍎 macOS" %}
{% tabs %}
{% tab title="Homebrew" %}
```bash
brew update
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
ruby -v
gem -v
gem install bundler
```

On Intel Macs, the path is `/usr/local/opt/ruby/bin`.
{% endtab %}

{% tab title="rbenv" %}
```bash
brew install rbenv
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
source ~/.zshrc
rbenv install 3.3.0
rbenv global 3.3.0
ruby -v
gem install bundler
```
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## ✅ Verification

```bash
ruby -v
gem -v
bundler -v
```

All commands should output versions.

***

## 💎 Managing Gems

{% stepper %}
{% step %}
Initialize

```bash
bundle init
```
{% endstep %}

{% step %}
Add to `Gemfile`

```ruby
gem "httparty"
```
{% endstep %}

{% step %}
Install / update

```bash
bundle install
bundle update httparty
```
{% endstep %}

{% step %}
Run script with locked environment

```bash
bundle exec ruby app.rb
```
{% endstep %}
{% endstepper %}

***

## 🔄 Updating

| Target       | Command                                             |
| ------------ | --------------------------------------------------- |
| Ruby (rbenv) | `rbenv install <version> && rbenv global <version>` |
| All gems     | `bundle update`                                     |
| One gem      | `bundle update <name>`                              |
| Bundler      | `gem install bundler`                               |

***

## 🗃 Common Commands

```bash
gem list
gem install <name>
gem uninstall <name>
bundle init
bundle install
bundle update
bundle exec ruby main.rb
```
