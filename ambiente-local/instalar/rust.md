---
description: Apprenez à héberger votre bot fait Rust avec DisCloud
---

# 🦀 Rust

### Installez Rust et Cargo sur votre ordinateur

> **cargo** - Gestionnaire de paquets **Rust** officiel

> Sélectionnez votre système d'exploitation

{% tabs %}
{% tab title="🪟 Windows" %}
### Installation de Rust et Cargo

### [Téléchargez Rust ici](https://static.rust-lang.org/rustup/dist/i686-pc-windows-gnu/rustup-init.exe)

> [Autres méthodes d'installation](https://forge.rust-lang.org/infra/other-installation-methods.html)

![](../../.gitbook/assets/rust-win.png)

### Vérifiez l'installation de la rouille

Ouvrez votre **cmd** ou **PowerShell** et tapez:

```
rustc --version
```

### Vérifier l'installation de la cargaison

Ouvrez votre **cmd** ou **PowerShell** et tapez:

```
cargo --version
```

{% hint style="success" %}
Si la réponse est la version dans les deux cas, cela voudra dire que c'est installé correctement!
{% endhint %}
{% endtab %}

{% tab title="🐧 Linux" %}
### Installation de Rust et Cargo

### <img src="../../.gitbook/assets/ubuntu.png" alt="" data-size="line"> <img src="../../.gitbook/assets/fedora.png" alt="" data-size="line"> <img src="../../.gitbook/assets/arch.png" alt="" data-size="line">&#x20;

Si vous utilisez une distribution **Linux**, **Mac OS** ou une autre distribution **Unix-like**, exécutez la commande suivante dans votre terminal :

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Vérifier l'installation de Rust

Tapez la commande suivante dans votre Terminal.

```shell
rustc --version
```

### Vérifier l'installation de Cargo

Tapez la commande suivante dans votre Terminal.

```shell
cargo --version
```

{% hint style="success" %}
Si la réponse est la version dans les deux cas, cela voudra dire que c'est installé correctement!
{% endhint %}
{% endtab %}
{% endtabs %}

### Mettre des dépendances dans votre `Cargo.toml`

#### Installer le [serenity](https://github.com/serenity-rs/serenity)

> **Serenity** - Est une bibliothèque Rust pour utiliser l'API Discord

Ajoutez la ligne ci-dessous à votre fichier `Cargo.toml` ou exécutez `cargo add serenity`:

{% code title="Cargo.toml" %}
```toml
[dependencies]
serenity = "0.11"
```
{% endcode %}
