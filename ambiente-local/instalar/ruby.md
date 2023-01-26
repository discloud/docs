# 💎 Ruby

### Instale o Ruby no seu computador

> **Rubygems** - É um gerenciador de pacotes para módulos Ruby (chamados de gems)
>
> **Bundler** - Permite especificar de quais gems seu projeto depende

> Selecione o seu Sistema Operacional

{% tabs %}
{% tab title="🪟 Windows" %}
### Instalação do `Ruby`

### [Baixe o Ruby Aqui](https://rubyinstaller.org/downloads/)

![](../../.gitbook/assets/win-ruby.png)

### Verifique a Instalação do `Ruby`

Abra o **cmd** ou **PowerShell** e digite**:**

```
ruby -v
```

### Verifique a Instalação do `Rubygems`

Abra o **cmd** ou **PowerShell** e digite:

```
gem -v
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}

### Instalação do `bundler`

Abra o **cmd** ou **PowerShell** e digite:

```
gem install bundler
```
{% endtab %}

{% tab title="🐧 Linux" %}
### Instalação do `Ruby`

### <img src="../../.gitbook/assets/ubuntu.png" alt="" data-size="line"> Ubuntu

Se você usa **Ubuntu** ou alguma distro baseada, digite o seguinte comando no Terminal:

```
sudo apt install ruby-dev
```

Informações dos pacotes dos Repositórios: [ruby](https://packages.ubuntu.com/search?suite=all\&section=all\&arch=any\&keywords=ruby-dev\&searchon=names)

### <img src="../../.gitbook/assets/fedora.png" alt="" data-size="line"> Fedora

Se você utiliza **Fedora** digite o seguinte comando no Terminal

```
sudo dnf install ruby-devel
```

Informações dos pacotes dos Repositórios: [ruby](https://packages.fedoraproject.org/pkgs/ruby/ruby-devel/)

### <img src="../../.gitbook/assets/arch.png" alt="" data-size="line"> Arch Linux

Se você utiliza **Arch Linux** ou alguma distro baseada, digite o seguinte comando no Terminal:

```
sudo pacman -S ruby rubygems
```

Informações dos pacotes dos Repositórios: [ruby](https://archlinux.org/packages/community/x86\_64/ruby/), [rubygems](https://archlinux.org/packages/community/any/rubygems/)

### Verifique a Instalação do `Ruby`

Digite no Terminal o seguinte comando.

```
ruby -v
```

### Verifique a Instalação do `Rubygems`

Digite no Terminal o seguinte comando.

```
gem -v
```

{% hint style="success" %}
Se retornar a versão de ambos então está instalado corretamente!
{% endhint %}

### Instalação do `bundler`

Digite no Terminal o seguinte comando.

```
sudo gem install bundler
```
{% endtab %}
{% endtabs %}

### Colocando dependências no seu `Gemfile`

![Exemplo](../../.gitbook/assets/ruby-example.png)

### [discordrb](https://rubygems.org/gems/discordrb) (rubygems)

Adicione a seguinte linha no seu `Gemfile`

{% code title="Gemfile" %}
```ruby
source "https://rubygems.org"
gem "discordrb"
```
{% endcode %}

### [discordrb](https://github.com/shardlab/discordrb) (github)

{% hint style="warning" %}
Se você quiser executar a versão mais recente do **`discordrb`**, fornece funcionalidades mais recentes, mas pode apresentar instabilidades.
{% endhint %}

{% code title="Gemfile" %}
```ruby
source "https://rubygems.org"
gem 'discordrb', github: 'shardlab/discordrb', branch: 'main'
```
{% endcode %}
