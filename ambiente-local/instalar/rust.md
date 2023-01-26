---
description: Aprenda a hospedar seu bot em JavaScript na DisCloud
---

# 🦀 Rust

### Instale o Rust e Cargo no seu computador

> **cargo** - Gerenciador de pacotes oficial do **Rust**

> Selecione o seu Sistema Operacional

{% tabs %}
{% tab title="🪟 Windows" %}
### Instalação do Rust e Cargo

### [Baixe o Rust Aqui](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe)

> [Outros metodos de instalação](https://forge.rust-lang.org/infra/other-installation-methods.html)

![](../../.gitbook/assets/rust-win.png)

### Verifique a Instalação do Rust

Abra o **cmd** ou **PowerShell** e digite**:**

```
rustc --version
```

### Verifique a Instalação do Cargo

Abra o **cmd** ou **PowerShell** e digite:

```
cargo --version
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}
{% endtab %}

{% tab title="🐧 Linux" %}
### Instalação do Rust e Cargo

### <img src="../../.gitbook/assets/ubuntu.png" alt="" data-size="line"> <img src="../../.gitbook/assets/fedora.png" alt="" data-size="line"> <img src="../../.gitbook/assets/arch.png" alt="" data-size="line">&#x20;

Se estiver qualquer distro **Linux**, **Mac OS**, ou outro **Unix-like**, execute o seguinte comando no seu Terminal

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Verifique a Instalação do Rust

Digite no Terminal o seguinte comando.

```shell
rustc --version
```

### Verifique a Instalação do Cargo

Digite no Terminal o seguinte comando.

```shell
cargo --version
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}
{% endtab %}
{% endtabs %}

### Colocando dependências no seu `Cargo.toml`

#### instalando o [serenity](https://github.com/serenity-rs/serenity)

> **Serenity** - é uma biblioteca Rust para usar a API do Discord

Adicione a seguinte linha no seu arquivo`Cargo.toml` ou execute `cargo add serenity`

{% code title="Cargo.toml" %}
```toml
[dependencies]
serenity = "0.11"
```
{% endcode %}
