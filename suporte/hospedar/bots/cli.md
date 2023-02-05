---
description: Hébergez et gérez votre application sans quitter votre VSCode !
---

# ⌨ DisCloud CLI

Une **CLI (Command-line Interface)** est un programme basé sur des commandes textuelles.

## :pencil: Exigences

#### 1. Vous devez utiliser la commande [**api**](../../comandos/api.md)**, pour obtenir votre token de l'API de DisCloud**.

<figure><img src="../../../.gitbook/assets/api_cmd.png" alt=""><figcaption><p>Utilisation de la commande .api</p></figcaption></figure>

## :keyboard: DisCloud CLI

DisCloud gère officiellement **2 projets CLI** dans **2 languages différentes**, utilisez celle qui vous convient le mieux.

{% tabs %}
{% tab title="🟨JavaScript" %}
## 1. Download

> Besoin de [NodeJS](../../../ambiente-local/instalar/nodejs.md) installé

### Windows / Linux

```shell
npm i -g discloud-cli
```

## 2. Rouvrez le terminal

## 3. Vérifiez l'installation

```shell
discloud --version
```

{% hint style="success" %}
Si la version apparaît, cela signifie qu'elle a été installée correctement.
{% endhint %}

## 4. Connexion

```
discloud login
```

[Lien du répertoire du projet](https://github.com/discloud/cli)
{% endtab %}

{% tab title="🦀Rust (NEW)" %}
## 1. Téléchargement du programme d'installation

### Windows

```powershell
. {iwr -useb "https://discloud.github.io/cli-rust/installer/windows.ps1"} | iex;
```

### Linux

```shell
curl -L https://discloud.github.io/cli-rust/installer/linux | bash
```

## 2. Rouvrez le terminal

## 3. Vérifiez l'installation

```
discloud --version
```

{% hint style="success" %}
Si la version apparaît, cela signifie qu'elle a été installée correctement.
{% endhint %}

## 4. Connexion

```shell
discloud login TOKEN_ICI
```

[Lien du répertoire du projet](https://github.com/discloud/cli-rust)
{% endtab %}
{% endtabs %}

## :thumbsup: Astuces

### Init

Utilisez la commande `discloud init` pour créer votre **discloud.config** de manière simple, intuitive et rapide!