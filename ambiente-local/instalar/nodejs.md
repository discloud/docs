---
description: Aprenda a hospedar seu bot em JavaScript na DisCloud
---

# 🟨 JavaScript (nodejs)

### Instale o Nodejs e npm no seu computador

> **npm** - Gerenciador de pacotes oficial do NodeJS

> Selecione o seu Sistema Operacional

{% tabs %}
{% tab title="🪟 Windows" %}
### Instalação do Nodejs e Npm

### [Baixe o Nodejs Aqui](https://nodejs.org/en/)

![](<../../.gitbook/assets/image (39).png>)

### Verifique a Instalação do NodeJS

Abra o **cmd** ou **PowerShell** e digite**:**

```
node -v
```

### Verifique a Instalação do npm

Abra o **cmd** ou **PowerShell** e digite:

```
npm -v
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}
{% endtab %}

{% tab title="🐧 Linux" %}
### Instalação do Nodejs e Npm

### <img src="../../.gitbook/assets/ubuntu.png" alt="" data-size="line"> Ubuntu

Se você usa **Ubuntu** ou alguma distro baseada nele, saiba que nem sempre a versão do **NodeJS** dos [repositórios](https://packages.ubuntu.com/search?keywords=nodejs\&searchon=names\&suite=all\&section=all) do **Ubuntu** é a mais recente (principalmente as versões LTS), por esse motivo, recomendo seguir as instruções abaixo:

```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
```

{% hint style="info" %}
O pacote **nodejs** já instala o **npm**
{% endhint %}

Outras versões, consulte [aqui](https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions)

Informações dos pacotes dos Repositórios: [nodejs](https://packages.ubuntu.com/search?keywords=nodejs\&searchon=names\&suite=all\&section=all), [npm](https://packages.ubuntu.com/search?suite=all\&section=all\&arch=any\&keywords=npm\&searchon=names)

### <img src="../../.gitbook/assets/fedora.png" alt="" data-size="line"> Fedora

A versão do **NodeJS** dos [repositórios](https://packages.fedoraproject.org/pkgs/nodejs/nodejs/) oficiais costuma ser bem recente, pode instalar com seguinte comando no Terminal:

```
sudo dnf install nodejs npm -y
```

Informações dos pacotes dos Repositórios: [nodejs](https://packages.fedoraproject.org/pkgs/nodejs/nodejs/), [npm](https://packages.fedoraproject.org/pkgs/nodejs/npm/)

### <img src="../../.gitbook/assets/arch.png" alt="" data-size="line"> Arch Linux

Os repositórios dos Arch Linux e derivados dele, têm os mais recentes pacotes, está disponível o **nodejs LTS e** **Node Latest.**&#x20;

Digite o seguinte comando para instalar a **v18.x.** _(mais detalhes consulte_ [_Arch Wiki_](https://wiki.archlinux.org/title/Node.js#Installation)_)_

```
sudo pacman -S nodejs-lts-hydrogen npm
```

Informações dos pacotes dos Repositórios: [nodejs](https://archlinux.org/packages/?sort=\&q=nodejs\&maintainer=\&flagged=), [npm](https://archlinux.org/packages/community/any/npm/)

### Verifique a Instalação do NodeJS

Digite no Terminal o seguinte comando.

```
node -v
```

### Verifique a Instalação do npm

Digite no Terminal o seguinte comando.

```
npm -v
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}
{% endtab %}
{% endtabs %}
