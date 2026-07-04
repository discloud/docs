---
description: Aprenda como hospedar bots de Discord na Discloud.
icon: robot
---

# Bots

## 🤖 O que é um "Bot" na Discloud?

Na **Discloud**, um **Bot** é qualquer aplicação que roda continuamente mas **não** requer uma porta externa para acesso. Isso normalmente inclui:

* 🤖 **Bots de Discord** (discord.js, discord.py, JDA, etc.)
* 💬 **Bots de Telegram**
* ⚙️ **Scripts de Automação**

***

## ✅ Requisitos

Para hospedar um bot, você deve atender a estes critérios:

{% hint style="success" %}
**Qualquer Plano** – Bots podem ser hospedados em qualquer plano, incluindo o plano Grátis (com limitações).
{% endhint %}

{% hint style="success" %}
[**`discloud.config`**](https://github.com/discloud/docs/blob/portuguese/configurations/discloud.config) – Necessário para a maioria dos métodos de implantação. Se estiver usando o [**Quick Setup**](../how-to-host-using/discord-bot.md#quick-setup-step-by-step-guide) do Bot do Discord, o bot irá guiá-lo através da configuração.
{% endhint %}

{% hint style="info" %}
**RAM** – Certifique-se de alocar RAM suficiente para as necessidades do seu bot (mín. 100MB).
{% endhint %}

***

## 🚀 Guia de Hospedagem Passo a Passo

{% stepper %}
{% step %}
**📝 Configurar `discloud.config`**

{% hint style="info" %}
Se você estiver usando o **Quick Setup** do Bot do Discord, não precisa criar este arquivo manualmente, o bot do Discord solicitará as informações durante o processo.
{% endhint %}

```ini
NAME=MeuBotLegal
TYPE=bot
MAIN=index.js
RAM=100
VERSION=latest
```

* **`TYPE=bot`**: Identifica a aplicação como um bot/serviço de segundo plano.
* **`MAIN`**: O ponto de entrada da sua aplicação. [Saiba mais sobre o arquivo principal.](../faq/general-questions/what-is-the-main-file.md)
* **`RAM`**: Memória alocada (mín. 100MB).
{% endstep %}

{% step %}
**🏗️ Lidando com Processos de Build**

Se o seu bot exigir uma etapa de build (como TypeScript ou Java), você tem duas opções:

{% tabs %}
{% tab title="Discloud Build (Recomendado)" %}
Deixe a Discloud lidar com o processo de build durante a implantação. Adicione o comando `BUILD` ao seu `discloud.config`.

```ini
BUILD=npm run build
START=npm run start
```
{% endtab %}

{% tab title="Build Local" %}
Faça o build do seu projeto localmente e envie os arquivos resultantes.

{% hint style="danger" %}
**Não use uma pasta chamada `dist`** para a saída do seu build local. A Discloud reserva o diretório `dist` para seu processo de build interno. Use um nome diferente como `build`, `out` ou `output`.
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Para aplicações Java, você **deve** fazer o build localmente e enviar o arquivo `.jar`. [Veja o guia de build Java](../faq/general-questions/how-to-build-and-package-a-java-application.md).
{% endhint %}
{% endstep %}

{% step %}
**🚀 Upload e Implantação**

Você pode enviar seu projeto usando qualquer um de nossos métodos suportados:

* 🖥️ [**Dashboard**](../how-to-host-using/dashboard.md)
* ⌨️ [**CLI**](../how-to-host-using/cli.md)
* 🟦 [**Extensão do VS Code**](../how-to-host-using/visual-studio-code.md)
* 🤖 [**Bot do Discord**](../how-to-host-using/discord-bot.md)
* 🐙 [**Integração com GitHub**](../api-and-integrations/github-integration.md)

{% hint style="info" %}
Antes de enviar, certifique-se de [comprimir seu projeto corretamente](../faq/general-questions/em-andamento-como-comprimir.md) e excluir arquivos desnecessários usando um arquivo [`.discloudignore`](../configurations/.discloudignore.md).
{% endhint %}
{% endstep %}
{% endstepper %}
