---
description: >-
  Install Rust using rustup, manage toolchains, and verify cargo for local
  development before deploying to Discloud.
icon: rust
---

# Rust

## 🧾 Overview

Rust provides performance, memory safety, and predictable resource usage for APIs, workers, and bots. Install with `rustup` to manage toolchains locally before deploying.

***

## 📥 Installation (choose your OS)

{% tabs %}
{% tab title="🪟 Windows" %}
{% tabs %}
{% tab title="rustup-init (Official)" %}
{% stepper %}
{% step %}
Download the installer: https://win.rustup.rs/ (or use the PowerShell tab)
{% endstep %}

{% step %}
Run and accept defaults (installs to user profile).
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="PowerShell" %}
```powershell
Invoke-WebRequest https://win.rustup.rs/x86_64 -OutFile rustup-init.exe
.\rustup-init.exe
```
{% endtab %}
{% endtabs %}

#### Verify

```bash
rustc --version
cargo --version
```

#### Update Toolchain

```bash
rustup update
```
{% endtab %}

{% tab title="🐧 Linux" %}
Install via rustup script:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustc --version
cargo --version
```

#### Add Build Essentials (Debian/Ubuntu)

```bash
sudo apt update
sudo apt install -y build-essential pkg-config libssl-dev
```

#### Update

```bash
rustup update
```

#### Uninstall Rust (rustup and all toolchains)

```bash
rustup self uninstall
```
{% endtab %}

{% tab title="🍎 macOS" %}
Install with rustup:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustc --version
cargo --version
```

Add build tools (if not present):

```bash
xcode-select --install  # prompts for developer tools
```

Update:

```bash
rustup update
```
{% endtab %}
{% endtabs %}

***

## 🧰 Toolchains & Components

{% stepper %}
{% step %}
List installed

```bash
rustup toolchain list
```
{% endstep %}

{% step %}
Add nightly (optional)

```bash
rustup toolchain install nightly
```
{% endstep %}

{% step %}
Set default

```bash
rustup default stable
```
{% endstep %}

{% step %}
Add components (example)

```bash
rustup component add clippy rustfmt
```
{% endstep %}
{% endstepper %}

***

## 🗂 Project Init

Create new project:

```bash
cargo new myapp
cd myapp
cargo build
```

Run:

```bash
cargo run
```

Format & lint:

```bash
cargo fmt -- --check
cargo clippy -- -D warnings
```

***

## 🗃 Common Cargo Commands

```bash
cargo new api-service          # create binary project
cargo build --release          # optimized build
cargo run                      # build + run
cargo test                     # run tests
cargo update                   # update dependency lock
cargo tree                     # dependency graph
cargo doc --open               # build docs locally
```

***

## 📦 Dependency Management

Dependencies declared in [`Cargo.toml`](../supported-languages/rust/cargo.toml.md) under `[dependencies]`:

```toml
[dependencies]
reqwest = { version = "0.12", features = ["json"] }
serde = { version = "1", features = ["derive"] }
tokio = { version = "1", features = ["rt-multi-thread", "macros"] }
```

Update lockfile:

```bash
cargo update
```

***

## 🔄 Updating

```bash
rustup update            # update all toolchains
rustup self update       # update rustup itself
```
