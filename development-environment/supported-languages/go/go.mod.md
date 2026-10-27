---
description: >-
  Learn how to generate and configure the go.mod file to manage modules and
  dependencies for Go apps on Discloud.
---

# go.mod

## 🗂️ What is `go.mod`?

`go.mod` defines your module path, the Go toolchain version (in `major.minor` form), and the direct dependencies required by your project. Discloud uses it (and the accompanying `go.sum`) to download and verify modules before building your application.

***

## 🛠️ Creating a New Module

{% stepper %}
{% step %}
Initialize a module in the current directory:

```bash
go mod init github.com/you/yourapp
```
{% endstep %}

{% step %}
Add (or update) dependencies automatically by referencing them in code and tidying:

```bash
go mod tidy
```

This creates `go.sum` (must not be empty) with checksum lines.
{% endstep %}

{% step %}
Add a specific dependency explicitly:

```bash
go get github.com/go-chi/chi/v5
```

Then tidy again if needed:

```bash
go mod tidy
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Need Go locally? See the [local environment guide](../../local-environment/golang.md).
{% endhint %}

***

## 🧩 Minimal Example

{% code title="go.mod" %}
```go
module github.com/you/yourapp

go 1.22
```
{% endcode %}

{% hint style="warning" %}
The Go version **MUST** be in `major.minor` form (e.g. `1.22`). Do **NOT** use patch: `1.22.3`.
{% endhint %}

***

## 📦 Adding Dependencies

To add a new dependency, either:

{% stepper %}
{% step %}
Import it in your source file then run `go mod tidy`, or
{% endstep %}

{% step %}
Run `go get module/path@version` directly.

**Example: add Chi router**

```bash
go get github.com/go-chi/chi/v5
```

Resulting `go.mod` snippet:

```go
require (
	github.com/go-chi/chi/v5 v5.0.12 // example version
)
```

> Versions are resolved semantically by the proxy/module system.
{% endstep %}
{% endstepper %}

***

## 🔒 `go.sum` Integrity

`go.sum` contains cryptographic hashes of every required module version (direct & indirect) to guarantee reproducible builds. It **must be committed** together with `go.mod`.

Regenerate / update it anytime:

```bash
go mod tidy
```

***

## 🧪 Application Type Examples

Tabbed examples for common scenarios:

{% tabs %}
{% tab title="🤖 Discord Bot" %}
{% code title="go.mod" %}
```go
module github.com/you/discordbot

go 1.22

require (
    github.com/bwmarrin/discordgo v0.27.1 // example
)
```
{% endcode %}
{% endtab %}

{% tab title="🌐 Website / API" %}
{% code title="go.mod" %}
```go
module github.com/you/webapp

go 1.22

require (
    github.com/go-chi/chi/v5 v5.0.12
)
```
{% endcode %}

Requirements:

* Your HTTP server must listen on `8080`.
{% endtab %}

{% tab title="📦 Minimal Stdlib" %}
{% code title="go.mod" %}
```go
module github.com/you/stdlibonly

go 1.22
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

## 🧰 Common Commands Reference

```bash
# Run your app directly
go run .

# Build a binary
go build -o app

# List all modules (direct+indirect)
go list -m all

# Show dependency graph
go mod graph
```
