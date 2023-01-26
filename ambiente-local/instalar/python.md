# 🐍 Python

## Instale o `Python` no seu computador

> **pip** - Instalador de pacotes oficial para Python.

> Selecione o seu Sistema Operacional

{% tabs %}
{% tab title="🪟 Windows" %}
### Instalando o `Python`

### [Baixe o Python Aqui](https://www.python.org/downloads/)

![](../../.gitbook/assets/py-win-download.png)

### Verifique a instalação do `Python`

Abra o **cmd** ou **PowerShell** e digite**:**

```
python --version
```

### Verifique a instalação do `pip`

Abra o **cmd** ou **PowerShell** e digite**:**

```
pip -V
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}
{% endtab %}

{% tab title="🐧 Linux" %}
### Instalando o `Python`

### <img src="../../.gitbook/assets/ubuntu.png" alt="" data-size="line"> Ubuntu

Se você usa **Ubuntu** ou alguma distro baseada, digite o seguinte comando no Terminal:

```
sudo apt install python3 python3-pip
```

Informações dos pacotes dos Repositórios: [python](https://packages.ubuntu.com/search?suite=all\&section=all\&arch=any\&keywords=python3\&searchon=names), [pip](https://packages.ubuntu.com/search?suite=all\&section=all\&arch=any\&keywords=python3-pip\&searchon=names)

### <img src="../../.gitbook/assets/fedora.png" alt="" data-size="line"> Fedora

Se você utiliza **Fedora** digite o seguinte comando no Terminal

```
sudo dnf install python3 python3-pip
```

Informações dos pacotes dos Repositórios: [python](https://packages.fedoraproject.org/pkgs/python3.10/python3/), [pip](https://packages.fedoraproject.org/pkgs/python-pip/python3-pip/)

### <img src="../../.gitbook/assets/arch.png" alt="" data-size="line"> Arch Linux

Se você utiliza **Arch Linux** ou alguma distro baseada, digite o seguinte comando no Terminal:

```
sudo pacman -S python python-pip
```

Informações dos pacotes dos Repositórios: [python](https://archlinux.org/packages/core/x86\_64/python/), [pip](https://archlinux.org/packages/extra/any/python-pip/)

### Verifique a instalação do `Python`

Abra o **Terminal** e digite:

```
python --version
```

### Verifique a instalação do `Pip`

Abra o **Terminal** e digite:

```
pip -V
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}
{% endtab %}
{% endtabs %}
