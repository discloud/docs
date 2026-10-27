---
description: >-
  Instale e gerencie Ruby localmente (Windows, macOS, Linux) usando instaladores
  ou gerenciadores de versão; use Bundler para dependências.
icon: gem
---

# Ruby

## 🧾 Visão Geral

Ruby é usado para bots, APIs (Sinatra) e frameworks completos (Rails). A instalação local permite gerenciar gems e testar antes de fazer o upload.

{% embed url="https://www.ruby-lang.org" %}

{% embed url="https://bundler.io/" %}

***

## 📥 Instalação (escolha uma)

{% tabs %}
{% tab title="🪟 Windows" %}
{% stepper %}
{% step %}
Baixe o Ruby+Devkit mais recente (x64) de [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/)
{% endstep %}

{% step %}
Execute o instalador (habilite MSYS2 quando solicitado).
{% endstep %}

{% step %}
Deixe o script pós-instalação terminar (configuração da toolchain).
{% endstep %}

{% step %}
Verifique e instale bundler

```bash
ruby -v
gem -v
gem install bundler
bundler -v
```
{% endstep %}

{% step %}
Inicialize projeto (opcional)

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
Dependências (exemplo Debian):

```bash
sudo apt update
sudo apt install -y build-essential libssl-dev libreadline-dev zlib1g-dev \
libyaml-dev libffi-dev libgdbm-dev libncurses5-dev libsqlite3-dev
```

Instalar rbenv + ruby-build:

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

Em Macs com processador Intel, o caminho é `/usr/local/opt/ruby/bin`.
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

## ✅ Verificação

```bash
ruby -v
gem -v
bundler -v
```

Todos os comandos devem mostrar versões.

***

## 💎 Gerenciando Gems

{% stepper %}
{% step %}
Inicializar

```bash
bundle init
```
{% endstep %}

{% step %}
Adicionar ao `Gemfile`

```ruby
gem "httparty"
```
{% endstep %}

{% step %}
Instalar / atualizar

```bash
bundle install
bundle update httparty
```
{% endstep %}

{% step %}
Executar script com ambiente bloqueado

```bash
bundle exec ruby app.rb
```
{% endstep %}
{% endstepper %}

***

## 🔄 Atualização

| Alvo          | Comando                                             |
| ------------- | --------------------------------------------------- |
| Ruby (rbenv)  | `rbenv install <version> && rbenv global <version>` |
| Todas as gems | `bundle update`                                     |
| Uma gem       | `bundle update <name>`                              |
| Bundler       | `gem install bundler`                               |

***

## 🗃 Comandos Comuns

```bash
gem list
gem install <name>
gem uninstall <name>
bundle init
bundle install
bundle update
bundle exec ruby main.rb
```
