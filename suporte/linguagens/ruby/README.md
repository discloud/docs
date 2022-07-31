---
description: Aprenda a hospedar seu bot em JavaScript na DisCloud
---

# 💎 Ruby

## :file\_folder: Arquivos

**Não envie todos os arquivos** de uma vez, você precisará colocar apenas os arquivos necessários do seu bot em um arquivo compactado`.zip`.&#x20;

```diff
Arquivos Mínimos Necessários
+ Arquivo Principal (Exemplo: index.rb, bot.rb...)
+ Arquivo Gemfile
+ Outros (Se o seu bot depender de outros arquivos deve incluir)
Não Necessários
- Arquivo Gemfile.lock
- Pasta .git
- Arquivo LICENSE
```

> * Dúvidas para encontrar o seu arquivo principal? [Clique aqui](../../faq/arquivo-principal.md#arquivos-principais-gerais)
> * Dúvidas em criar o seu  arquivo `Gemfile`? [Clique aqui](gemfile.md)

{% content-ref url="gemfile.md" %}
[gemfile.md](gemfile.md)
{% endcontent-ref %}

### :compression: Compactando os Arquivos

Selecione apenas os arquivos necessários, como mencionado em cima e crie o seu **.zip**

![](../../../.gitbook/assets/ruby-zip.png)

Para mais detalhes sobre como **Compactar os seus Arquivos** de acordo com o seu **Sistema Operativo**, pode consultar em baixo:

{% content-ref url="../../faq/zip.md" %}
[zip.md](../../faq/zip.md)
{% endcontent-ref %}

## ✍ Hospedando o seu bot

{% hint style="info" %}
Escolha o método para hospedar seu Bot na Discloud:
{% endhint %}

{% content-ref url="../../hospedar/bots/via-painel-de-controle.md" %}
[via-painel-de-controle.md](../../hospedar/bots/via-painel-de-controle.md)
{% endcontent-ref %}

{% content-ref url="../../hospedar/bots/discord.md" %}
[discord.md](../../hospedar/bots/discord.md)
{% endcontent-ref %}

## :earth\_americas: Hospedando o Seu Site

{% hint style="info" %}
Esta funcionalidade necessita de alguns requisitos básicos para poder ser utilizada, por favor consulte os requisitos [aqui](../../hospedar/sites/#requisitos) antes de continuar
{% endhint %}

### Utilizando o `Ruby On Rails`

**`Rails`** é uma ferramenta de desenvolvimento que dá aos desenvolvedores web uma estrutura, pode ser usada na construção de Sites ou APIs.

### Instalando o `Rails`

Consulte a documentação oficial abaixo.

{% embed url="https://guides.rubyonrails.org/getting_started.html#creating-a-new-rails-project-installing-rails" %}

### Configurando o `Rails`

Você precisa de adicionar o seu **subdomínio** (ou **domínio**) nos hosts permitidos do `Rails`.

> * Edite o arquivo `config/application.rb`
> * Modifique a **linha 21**, com o seu dominio

{% code title="config/application.rb" %}
```ruby
require_relative "boot"

require "rails/all"

# Require the gems listed in Gemfile, including any gems
# you've limited to :test, :development, or :production.
Bundler.require(*Rails.groups)

module RailsOnDiscloud
  class Application < Rails::Application
    # Initialize configuration defaults for originally generated Rails version.
    config.load_defaults 7.0
    # config.time_zone = "Central Time (US & Canada)"
    # config.eager_load_paths << Rails.root.join("extras")
    Rails.application.config.hosts = [
    IPAddr.new("0.0.0.0/0"),        # All IPv4 addresses.
    IPAddr.new("::/0"),             # All IPv6 addresses.
    "localhost",                    # The localhost reserved domain.
    "yourdomain.discloud.app"       # !!!! Discloud Domain !!!!!
]
  end
end

```
{% endcode %}
