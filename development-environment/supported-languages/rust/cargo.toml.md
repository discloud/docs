---
description: >-
  Comprehensive guide to the Cargo.toml manifest for Rust bots and web
  (site/API) apps on Discloud.
---

# Cargo.toml

## 🗂️ What is `Cargo.toml`?

`Cargo.toml` is the manifest that defines your Rust package (crate) metadata: name, version, authors, edition, dependencies, features, build scripts and more. Discloud relies on it to resolve and compile your project before starting it.

***

## 🛠️ Creating a New Project

{% stepper %}
{% step %}
Initialize in existing directory:

```bash
cargo init
```
{% endstep %}

{% step %}
Create a new directory automatically:

```bash
cargo new my_bot
```

{% hint style="info" %}
Use [**snake\_case**](https://en.wikipedia.org/wiki/Letter_case#Snake_case) or [**kebab-case**](https://en.wikipedia.org/wiki/Letter_case#Kebab_case) names.
{% endhint %}
{% endstep %}

{% step %}
Add a dependency quickly (Cargo 1.62+):

```bash
cargo add serenity
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Need Rust? See the [installation page](../../local-environment/rust.md).
{% endhint %}

***

## 📦 Examples

{% tabs %}
{% tab title="Discord Bot (serenity)" %}
{% code title="Cargo.toml" %}
```toml
[package]
name = "discord_bot"
version = "0.1.0"
edition = "2021"

[dependencies]
serenity = { version = "0.11", default-features = false, features = [
	"client", "gateway", "rustls_backend", "model" ] }
tokio = { version = "1", features = ["macros", "rt-multi-thread"] }
tracing = "0.1"
dotenvy = "0.15"
```
{% endcode %}

Serenity is a Discord API library: [https://crates.io/crates/serenity](https://crates.io/crates/serenity)
{% endtab %}

{% tab title="Axum API" %}
{% code title="Cargo.toml" %}
```toml
[package]
name = "axum_api"
version = "0.1.0"
edition = "2021"

[dependencies]
axum = "0.7"
tokio = { version = "1", features = ["macros", "rt-multi-thread"] }
serde = { version = "1", features = ["derive"] }
serde_json = "1"
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["fmt", "env-filter"] }
dotenvy = "0.15"
```
{% endcode %}

Must listen on `0.0.0.0:8080`.
{% endtab %}

{% tab title="Rocket (Nightly)" %}
{% code title="Cargo.toml" %}
```toml
[package]
name = "rocket_site"
version = "0.1.0"
edition = "2021"

[dependencies]
rocket = { version = "0.5.0", features = ["json"] }
serde = { version = "1", features = ["derive"] }
serde_json = "1"
```
{% endcode %}

Requires nightly toolchain + bind to port 8080.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Need OS-level dependencies (e.g. `openssl`, `ffmpeg`)? Add them under `APT=` in [`discloud.config`](../../../configurations/discloud.config/). See [the APT packages list](../../../configurations/discloud.config/apt.md) for syntax and examples.
{% endhint %}

***

## 🧰 Common Commands Reference

```bash
# Build debug
cargo build

# Build release
cargo build --release

# Run
cargo run

# Add dependency
cargo add <crate>

# Remove dependency
cargo rm <crate>

# Audit (optional; needs cargo-audit)
cargo audit
```

Optional tools:

```bash
cargo install cargo-edit cargo-outdated cargo-audit
```
