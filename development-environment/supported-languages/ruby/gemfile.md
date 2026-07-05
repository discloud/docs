---
description: >-
  Guia completo do Gemfile para bots Ruby e aplicações web (site/API) na
  Discloud.
---

# Gemfile

## 🗂️ O que é `Gemfile`?

`Gemfile` lista as gems (bibliotecas) que sua aplicação Ruby precisa. A Discloud usa o **Bundler** durante o deploy para instalá-las antes de iniciar sua aplicação.

***

## 🛠️ Criando um `Gemfile` (Início Rápido)

{% stepper %}
{% step %}
Inicialize o Bundler em uma pasta vazia:

```bash
bundle init
```

Isso cria um `Gemfile` inicial.
{% endstep %}

{% step %}
Adicione dependências diretamente via Bundler:

```bash
bundle add sinatra
bundle add puma
```
{% endstep %}

{% step %}
Instale (respeitando o Gemfile):

```bash
bundle install
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Instale o Bundler se estiver faltando: `gem install bundler`.
{% endhint %}

***

## 🧪 Grupos de Ambiente

```ruby
group :development, :test do
	gem 'pry'
	gem 'rspec'
end

group :production do
	# gems apenas para produção (APM, backends de logging, etc.)
end
```

Pule a instalação de grupos dev/test no momento do deploy se desejado:

```bash
bundle install --without development test
```

***

## 🧩 Exemplos de Gemfiles

{% tabs %}
{% tab title="Rails (Site/API)" %}
{% code title="Gemfile" %}
```ruby
source 'https://rubygems.org'

ruby '3.2.2'

gem 'rails', '~> 7.0.0'
gem 'puma',  '~> 5.0'
gem 'pg',    '~> 1.1'   # ou 'sqlite3' para uso simples/local
gem 'bootsnap', '>= 1.4.4', require: false

group :development, :test do
	gem 'pry'
	gem 'rspec-rails'
end

group :production do
	# monitoramento / cache / etc.
end

gem 'bundler', '~> 2.4'
```
{% endcode %}
{% endtab %}

{% tab title="Sinatra (Site/API)" %}
{% code title="Gemfile" %}
```ruby
source 'https://rubygems.org'
ruby '3.2.2'

gem 'sinatra', '~> 3.0'
gem 'puma',    '~> 5.0'
gem 'dotenv',  '~> 2.8', require: false

group :development do
	gem 'rerun'
end
```
{% endcode %}
{% endtab %}

{% tab title="discordrb (Bot)" %}
{% code title="Gemfile" %}
```ruby
source 'https://rubygems.org'
ruby '3.2.2'

gem 'discordrb', '~> 3.4'
gem 'dotenv',    '~> 2.8', require: false

group :development do
	gem 'pry'
end
```
{% endcode %}
{% endtab %}

{% tab title="Bot Mínimo" %}
{% code title="Gemfile" %}
```ruby
source 'https://rubygems.org'
ruby '3.2.2'

# Adicione apenas o que você realmente precisa
gem 'httparty', '~> 0.21'
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

## 🧾 Exemplo de `config.ru` (Site Sinatra / Rack)

{% code title="config.ru" %}
```ruby
require 'bundler/setup'
require 'sinatra'
require 'dotenv/load' if ENV['RACK_ENV'] != 'production'

set :bind, '0.0.0.0'
set :port, (ENV['PORT'] || 8080)

get '/' do
	'Olá do app Sinatra na Discloud!'
end

run Sinatra::Application
```
{% endcode %}

Para bots, você normalmente NÃO precisa de `config.ru`; em vez disso, apenas aponte `MAIN` no [`discloud.config`](https://github.com/discloud/docs/blob/portuguese/configurations/discloud.config) para sua entrada Ruby (ex.: `bot.rb`).

***

## 🧪 Atualizando Dependências

```bash
# Atualize uma única gem
bundle update puma

# Atualize todas (cuidado – pode introduzir mudanças incompatíveis)
bundle update

# Veja gems desatualizadas
bundle outdated
```

Patches de segurança: monitore avisos (ex.: RubySec / Dependabot) e agende `bundle update --patch` periodicamente.

***

## 🧰 Referência de Comandos Comuns

```bash
# Inicializar Gemfile
bundle init

# Adicionar gem (escreve no Gemfile & instala)
bundle add <gem>

# Instalar apenas com grupos de produção
bundle install --without development test

# Verificar problemas no gráfico de dependências
bundle check

# Limpar gems não utilizadas (após prune)
bundle clean --force
```
