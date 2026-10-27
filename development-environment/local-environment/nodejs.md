---
description: >-
  Instale e gerencie Node.js localmente (Windows, macOS, Linux) usando um
  instalador, gerenciador de pacotes ou gerenciador de versão.
icon: node-js
---

# Node.js

## 🧾 Visão Geral

Node.js executa JavaScript fora do navegador para CLIs, APIs, workers, tarefas agendadas e serviços em tempo real. A instalação local permite:

* Instalar dependências (npm, pnpm ou Yarn)
* Executar e depurar antes de fazer o upload na Discloud
* Preparar builds ou bundles quando necessário

{% embed url="https://nodejs.org/" %}

***

## 📥 Instalação

Escolha seu sistema operacional, então um método. Gerenciadores de versão (NVM) ajudam ao alternar projetos.

{% tabs %}
{% tab title="🪟 Windows" %}
{% tabs %}
{% tab title="Instalador" %}
{% stepper %}
{% step %}
Abra [https://nodejs.org/en/download](https://nodejs.org/en/download) e baixe o .msi LTS
{% endstep %}

{% step %}
Execute o instalador (mantenha os padrões incluindo npm + PATH)
{% endstep %}

{% step %}
Reabra o terminal e verifique

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

{% tab title="NVM para Windows" %}
{% stepper %}
{% step %}
Baixe o último `nvm-setup.exe` dos [lançamentos](https://github.com/coreybutler/nvm-windows/releases)
{% endstep %}

{% step %}
Instale aceitando os padrões
{% endstep %}

{% step %}
Instale e use LTS

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
{% tab title="Instalador" %}
Baixe o .pkg LTS de [nodejs.org](https://nodejs.org/en/download) então:

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

## 🔄 Atualizando Node.js

Se você estiver usando **NVM**, pode atualizar Node.js com:

```bash
nvm install --lts
```

No NVM para Windows, use `nvm install lts`.

Caso contrário, use o gerenciador de pacotes do seu sistema ou baixe novamente o instalador mais recente do site do Node.js.
