---
description: >-
  Install and manage Go locally (Windows, macOS, Linux) using official archives
  or package managers; manage modules with go mod.
icon: golang
---

# Go

## 🧾 Overview

Go (Golang) is a compiled language suited for APIs, workers, CLIs and concurrent services. Local installation lets you build and test binaries before deploying.

{% embed url="https://go.dev" %}

***

## 📥 Installation (choose one)

{% tabs %}
{% tab title="Windows" %}
{% tabs %}
{% tab title="Installer" %}
{% stepper %}
{% step %}
Download the Windows .msi from [https://go.dev/dl/](https://go.dev/dl/)
{% endstep %}

{% step %}
Run it (adds Go to PATH).
{% endstep %}

{% step %}
Reopen terminal (PowerShell / CMD).
{% endstep %}

{% step %}
Verify:

```bash
go version
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Scoop" %}
```bash
scoop install go
go version
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="Linux" %}
{% tabs %}
{% tab title="Tarball" %}
```bash
# Replace version as needed
curl -LO https://go.dev/dl/go1.22.6.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.6.linux-amd64.tar.gz
export PATH="/usr/local/go/bin:$PATH"
go version
```

{% hint style="info" %}
Add PATH line to \~/.bashrc or \~/.zshrc to persist.
{% endhint %}
{% endtab %}

{% tab title="Debian/Ubuntu" %}
```bash
sudo apt update
sudo apt install -y golang-go
go version
```

{% hint style="info" %}
Note: Repo version may lag behind latest.
{% endhint %}
{% endtab %}

{% tab title="Fedora" %}
```bash
sudo dnf install -y golang
go version
```
{% endtab %}

{% tab title="Arch" %}
```bash
sudo pacman -S --needed go
go version
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="macOS" %}
{% tabs %}
{% tab title="Installer" %}
Download the .pkg from [https://go.dev/dl/](https://go.dev/dl/) then:

```bash
go version
```
{% endtab %}

{% tab title="Homebrew" %}
```bash
brew update
brew install go
go version
```
{% endtab %}

{% tab title="Tarball" %}
```bash
curl -LO https://go.dev/dl/go1.22.6.darwin-arm64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.6.darwin-arm64.tar.gz
export PATH="/usr/local/go/bin:$PATH"
go version
```

{% hint style="info" %}
Add PATH export to shell profile to persist.
{% endhint %}
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## 🗂 Modules & Project Init

{% stepper %}
{% step %}
Initialize a module (creates go.mod)

```bash
mkdir myapp && cd myapp
go mod init example.com/myapp
```
{% endstep %}

{% step %}
Add a file `main.go`

```go
package main
import "fmt"
func main() { fmt.Println("hello") }
```
{% endstep %}

{% step %}
Run

```bash
go run .
```
{% endstep %}

{% step %}
Build

```bash
go build -o app
```
{% endstep %}
{% endstepper %}

***

## 🔄 Updating

| Task                      | Command                 |
| ------------------------- | ----------------------- |
| Tidy modules              | `go mod tidy`           |
| Update deps (minor/patch) | `go get -u ./...`       |
| Update single module      | `go get -u module/name` |
| Verify modules            | `go mod verify`         |

***

## 🗃 Common Commands

```bash
go mod init example.com/project
go mod tidy
go run .
go build -o bin/app
go test ./...
go list -m all
```
