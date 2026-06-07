---
description: Complete guide to host Ruby applications on Discloud.
icon: gem
---

# Ruby

## 📁 **Preparing the Files**

Before uploading your project, you must **exclude unnecessary files** to optimize the deployment.

#### ❌ **Files to Exclude**

Ensure the following files and directories are **not** included in your [`.zip`](../../../faq/general-questions/wip-how-to-compress.md):

```diff
- Gemfile.lock
- .git
- tmp/
- log/
```

📌 **Use a** [**`.discloudignore`**](../../../configurations/.discloudignore.md) **file** to automatically exclude these files.

🔗 **Need help setting up your** [**`Gemfile`**](gemfile.md) **or find** [**main file**](../../../faq/general-questions/what-is-the-main-file.md)**?**

***

### 🌐 Hosting Your Site with Ruby on Rails

Before deploying your website or API on Discloud, ensure that you meet the following **requirements**:

{% hint style="success" %}
[Platinum plan or higher](https://discloud.com/plans) is required to host websites or APIs.
{% endhint %}

{% hint style="success" %}
[A subdomain must be created](../../../faq/general-questions/how-to-create-a-subdomain.md) before deployment.
{% endhint %}

{% hint style="danger" %}
Port `8080` is mandatory – Applications must listen on this port.
{% endhint %}

### ⚙️ Configuring Ruby on Rails

{% code title="config/application.rb" %}
```ruby
require_relative "boot"

require "rails/all"

# Requires the gems listed in the Gemfile, including those limited to :test, :development, or :production.
Bundler.require(*Rails.groups)

module RailsOnDiscloud
  class Application < Rails::Application
    # Initialize the default configuration for the originally generated Rails version.
    config.load_defaults 7.0
    # config.time_zone = "Central Time (US & Canada)"
    # config.eager_load_paths << Rails.root.join("extras")
    Rails.application.config.hosts = [
      IPAddr.new("0.0.0.0/0"),        # All IPv4 addresses.
      IPAddr.new("::/0"),             # All IPv6 addresses.
      "localhost",                    # Reserved domain localhost.
      "seusubdomínio.discloud.app"    # !!! Discloud Subdomain !!!
    ]
  end
end
```
{% endcode %}

***

## ✍️ Deploying **Your Application**

Once your project is **configured and compressed**, you can choose one of the following **deployment methods** on Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Upload and manage your application via the web interface.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Deploy directly through Discloud’s Discord bot commands.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integrate with VS Code for seamless project management.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use the command-line interface for quick and efficient deployment.</td><td></td><td></td><td></td></tr></tbody></table>
