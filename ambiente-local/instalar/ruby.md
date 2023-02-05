---
description: Apprenez à héberger votre bot fait Ruby avec DisCloud
---

# 💎 Ruby

### Installez Ruby sur votre ordinateur

> **Rubygems** - C'est un gestionnaire de paquets pour les modules Ruby (appelés gems)
>
> **Bundler** - Vous permet de spécifier de quelles gemmes dépend votre projet

> Sélectionnez votre système d'exploitation

{% tabs %}
{% tab title="🪟 Windows" %}
#### Installation de `Ruby`

#### [Télécharger Ruby ici](https://rubyinstaller.org/downloads/)

![](../../.gitbook/assets/ruby\_download.png)

#### Vérifier l'installation de `Ruby`

Ouvrez votre **cmd** ou **PowerShell** et tapez:

```
ruby -v
```

#### Vérifier l'installation de `Rubygems`

Ouvrez votre **cmd** ou **PowerShell** et tapez:

```
gem -v
```

{% hint style="success" %}
Si la réponse est la version dans les deux cas, cela voudra dire que c'est installé correctement!
{% endhint %}

#### Installation du `bundler`

Ouvrez votre **cmd** ou **PowerShell** et tapez:

```
gem install bundler
```
{% endtab %}

{% tab title="🐧 Linux" %}
#### Installation de `Ruby`

#### <img src="../../.gitbook/assets/ubuntu_logo.png" alt="" data-size="line"> Ubuntu

Si vous utilisez **Ubuntu** ou une distribution basée sur, tapez la commande suivante dans votre Terminal:

```
sudo apt install ruby-dev
```

Informations sur le package des répositoires: [ruby](https://packages.ubuntu.com/search?suite=all\&section=all\&arch=any\&keywords=ruby-dev\&searchon=names)

#### <img src="../../.gitbook/assets/fedora_logo.png" alt="" data-size="line"> Fedora

Si vous utilisez **Fedora** tapez la commande suivante dans votre Terminal:

```
sudo dnf install ruby-devel
```

Informations sur le package des répositoires: [ruby](https://packages.fedoraproject.org/pkgs/ruby/ruby-devel/)

#### <img src="../../.gitbook/assets/arch-linux_logo.png" alt="" data-size="line"> Arch Linux

Si vous utilisez **Arch Linux** ou toute autre distribution basée, tapez la commande suivante dans votre Terminal:

```
sudo pacman -S ruby rubygems
```

Informations sur le package des répositoires: [ruby](https://archlinux.org/packages/community/x86\_64/ruby/), [rubygems](https://archlinux.org/packages/community/any/rubygems/)

#### Verifique a Instalação do `Ruby`

Tapez la commande suivante dans votre Terminal.

```
ruby -v
```

#### Verifique a Instalação do `Rubygems`

Tapez la commande suivante dans votre Terminal.

```
gem -v
```

{% hint style="success" %}
Si la réponse est la version dans les deux cas, cela voudra dire que c'est installé correctement!
{% endhint %}

#### Instalação do `bundler`

Tapez la commande suivante dans votre Terminal.

```
sudo gem install bundler
```
{% endtab %}
{% endtabs %}

### Mettre des dépendances dans votre `Gemfile`

![Exemplo](../../.gitbook/assets/gem-file\_example.png)

### [discordrb](https://rubygems.org/gems/discordrb) (rubygems)

Ajoutez la ligne suivante à votre `Gemfile`

{% code title="Gemfile" %}
```ruby
source "https://rubygems.org"
gem "discordrb"
```
{% endcode %}

### [discordrb](https://github.com/shardlab/discordrb) (github)

{% hint style="warning" %}
Si vous souhaitez exécuter la dernière version de **`discordrb`**, elle fournit des fonctionnalités plus récentes mais peut être instable.
{% endhint %}

{% code title="Gemfile" %}
```ruby
source "https://rubygems.org"
gem 'discordrb', github: 'shardlab/discordrb', branch: 'main'
```
{% endcode %}
