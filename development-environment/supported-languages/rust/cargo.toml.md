---
description: >-
  Guia completo do manifesto Cargo.toml para bots Rust e aplicações web
  (site/API) na Discloud.
---

# Cargo.toml

## 🗂️ O que é `Cargo.toml`?

`Cargo.toml` é o manifesto que define os metadados do seu pacote Rust (crate): nome, versão, autores, edição, dependências, recursos, scripts de build e mais. A Discloud depende dele para resolver e compilar seu projeto antes de iniciá-lo.

***

## 🛠️ Criando um Novo Projeto

{% stepper %}
{% step %}
Inicialize em diretório existente:

```bash
cargo init
```
{% endstep %}

{% step %}
Crie um novo diretório automaticamente:

```bash
cargo new my_bot
```

{% hint style="info" %}
Use nomes em [**snake\_case**](https://en.wikipedia.org/wiki/Letter_case#Snake_case) ou [**kebab-case**](https://en.wikipedia.org/wiki/Letter_case#Kebab_case).
{% endhint %}
{% endstep %}

{% step %}
Adicione uma dependência rapidamente (Cargo 1.62+):

```bash
cargo add serenity
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Precisa do Rust? Veja a [página de instalação](../../local-environment/rust.md).
{% endhint %}

***

## 📦 Exemplos

{% tabs %}
{% tab title="Bot Discord (serenity)" %}
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

Serenity é uma biblioteca da API do Discord: [https://crates.io/crates/serenity](https://crates.io/crates/serenity)
{% endtab %}

{% tab title="API Axum" %}
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

Deve escutar em `0.0.0.0:8080`.
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

Requer toolchain nightly + bind na porta 8080.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Precisa de dependências no nível do SO (ex.: `openssl`, `ffmpeg`)? Adicione-as sob `APT=` no [`discloud.config`](../../../configurations/discloud.config/). Veja [a lista de pacotes APT](../../../configurations/discloud.config/apt.md) para sintaxe e exemplos.
{% endhint %}

***

## 🧰 Referência de Comandos Comuns

```bash
# Build debug
cargo build

# Build release
cargo build --release

# Executar
cargo run

# Adicionar dependência
cargo add <crate>

# Remover dependência
cargo rm <crate>

# Auditar (opcional; precisa cargo-audit)
cargo audit
```

Ferramentas opcionais:

```bash
cargo install cargo-edit cargo-outdated cargo-audit
```
