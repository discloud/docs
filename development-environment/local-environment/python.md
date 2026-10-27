---
description: >-
  Install and manage Python locally (Windows, macOS, Linux) using official
  installers, system packages, or pyenv; create virtual environments.
icon: python
---

# Python

## 🧾 Overview

Python is used for bots, APIs, automation, scripting, and data tasks. Local installation allows you to install dependencies and test before deploying to Discloud.

{% embed url="https://www.python.org" %}

***

## 📥 Installation

{% tabs %}
{% tab title="🪟 Windows" %}
{% stepper %}
{% step %}
Download the latest Python 3 installer from [https://www.python.org/downloads/](https://www.python.org/downloads/)
{% endstep %}

{% step %}
Check "Add Python to PATH" and complete installation.
{% endstep %}

{% step %}
Reopen terminal and verify

```bash
python --version
pip -V
```
{% endstep %}

{% step %}
Create optional virtual environment

```bash
python -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🐧 Linux" %}
{% tabs %}
{% tab title="Debian/Ubuntu" %}
```bash
sudo apt update
sudo apt install -y python3 python3-pip python3-venv
python3 --version
pip3 -V
python3 -m venv .venv
source .venv/bin/activate
```
{% endtab %}

{% tab title="Fedora" %}
```bash
sudo dnf install -y python3 python3-pip
python3 --version
pip3 -V
python3 -m venv .venv
source .venv/bin/activate
```
{% endtab %}

{% tab title="Arch" %}
```bash
sudo pacman -S --needed python python-pip
python --version
pip -V
python -m venv .venv
source .venv/bin/activate
```
{% endtab %}

{% tab title="pyenv" %}
Dependencies (Debian example):

```bash
sudo apt update
sudo apt install -y build-essential libssl-dev zlib1g-dev \
libncurses5-dev libffi-dev libbz2-dev libreadline-dev libsqlite3-dev \
liblzma-dev wget curl
```

Install & configure:

```bash
curl https://pyenv.run | bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.bashrc
pyenv install 3.12.4
pyenv global 3.12.4
python --version
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🍎 macOS" %}
{% tabs %}
{% tab title="Installer" %}
Download from [python.org](https://www.python.org/downloads/) and run, then:

```bash
python3 --version
pip3 -V
```
{% endtab %}

{% tab title="Homebrew" %}
```bash
brew update
brew install python
python3 --version
pip3 -V
```
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## ✅ Verification

```bash
python --version
pip -V
```

If your distribution uses `python3`, invoke that instead of `python`.

***

## 🗂 Virtual Environments

**What it is**: A virtual environment is an isolated directory tree containing its own Python interpreter and installed packages, separate from your global (system) Python.

**Why use it**:

* Keeps project dependencies isolated (one project can use `requests==2.31`, another `requests==2.29`).
* Avoids needing administrator / system-wide installs.
* Prevents accidental conflicts with OS packages or other projects.
* Makes `requirements.txt` reflect only what the project actually needs (reproducibility when deploying or sharing).
* Lets you test upgrades safely (create a new env, install, compare behavior).

Create & activate:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

Install dependencies & capture versions:

```bash
pip install -r requirements.txt
pip freeze > requirements.txt
```

***

## 🔄 Updating

| Task                       | Command                               |
| -------------------------- | ------------------------------------- |
| Upgrade pip                | `python -m pip install --upgrade pip` |
| Upgrade a package          | `pip install <name> --upgrade`        |
| Install new Python (pyenv) | `pyenv install <version>`             |

***

## 🗃 Common Commands

```bash
pip install requests
pip list
pip freeze > requirements.txt
python main.py
python -m venv .venv
```
