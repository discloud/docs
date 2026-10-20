---
description: >-
  Comprehensive Gemfile guide for Ruby bots and web (site/API) applications on
  Discloud.
---

# Gemfile

## 🗂️ What is `Gemfile`?

`Gemfile` lists the gems (libraries) your Ruby application needs. Discloud uses **Bundler** during deployment to install them before starting your app.

***

## 🛠️ Creating a `Gemfile` (Quick Start)

{% stepper %}
{% step %}
Initialize Bundler in an empty folder:

```bash
bundle init
```

This creates a starter `Gemfile`.
{% endstep %}

{% step %}
Add dependencies directly via Bundler:

```bash
bundle add sinatra
bundle add puma
```
{% endstep %}

{% step %}
Install (respecting the Gemfile):

```bash
bundle install
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Install Bundler if missing: `gem install bundler`.
{% endhint %}

***

## 🧪 Environment Groups

```ruby
group :development, :test do
	gem 'pry'
	gem 'rspec'
end

group :production do
	# production-only gems (APM, logging backends, etc.)
end
```

Skip installing dev/test groups at deploy time if desired:

```bash
bundle install --without development test
```

***

## 🧩 Example Gemfiles

{% tabs %}
{% tab title="Rails (Site/API)" %}
{% code title="Gemfile" %}
```ruby
source 'https://rubygems.org'

ruby '3.2.2'

gem 'rails', '~> 7.0.0'
gem 'puma',  '~> 5.0'
gem 'pg',    '~> 1.1'   # or 'sqlite3' for simple/local usage
gem 'bootsnap', '>= 1.4.4', require: false

group :development, :test do
	gem 'pry'
	gem 'rspec-rails'
end

group :production do
	# monitoring / caching / etc.
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

{% tab title="Minimal Bot" %}
{% code title="Gemfile" %}
```ruby
source 'https://rubygems.org'
ruby '3.2.2'

# Add only what you truly need
gem 'httparty', '~> 0.21'
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

## 🧾 Sample `config.ru` (Sinatra / Rack Site)

{% code title="config.ru" %}
```ruby
require 'bundler/setup'
require 'sinatra'
require 'dotenv/load' if ENV['RACK_ENV'] != 'production'

set :bind, '0.0.0.0'
set :port, (ENV['PORT'] || 8080)

get '/' do
	'Hello from Discloud Sinatra app!'
end

run Sinatra::Application
```
{% endcode %}

For bots you typically do NOT need `config.ru`; instead just point `MAIN` in [`discloud.config`](../../../configurations/discloud.config/) to your Ruby entry (e.g. `bot.rb`).

***

## 🧪 Updating Dependencies

```bash
# Update a single gem
bundle update puma

# Update all (careful – may introduce breaking changes)
bundle update

# See outdated gems
bundle outdated
```

Security patches: monitor advisories (e.g., RubySec / Dependabot) and schedule periodic `bundle update --patch`.

***

## 🧰 Common Commands Reference

```bash
# Initialize Gemfile
bundle init

# Add gem (writes Gemfile & installs)
bundle add <gem>

# Install with production-only groups
bundle install --without development test

# Check dependency graph issues
bundle check

# Clean unused gems (after prune)
bundle clean --force
```
