---
description: >-
  Aprenda como hospedar sites, APIs e dashboards na Discloud usando subdomínios
  e domínios personalizados.
icon: globe-pointer
---

# Websites e APIs

## 🌐 O que é um "Site" na Discloud?

Na **Discloud**, qualquer aplicação que use uma **porta de rede** e requeira **acesso externo** é considerada um **Site**. Isso inclui:

* 🖥️ **Websites** (Estáticos ou Dinâmicos)
* 🔌 **APIs** (REST, GraphQL, etc.)
* 📊 **Dashboards** (para Bots ou independentes)
* 🤖 **Bots com Interfaces Web**

Para permitir o acesso externo, a Discloud roteia o tráfego através de um proxy para a **porta 8080** e **host 0.0.0.0** da sua aplicação usando um **subdomínio** (ex: `minhaapp.discloud.app`).

***

## ✅ Requisitos

Para hospedar um site ou API, você deve atender a estes critérios:

{% hint style="success" %}
**Plano Platinum ou Superior** – Necessário para todas as aplicações `TYPE=site`.
{% endhint %}

{% hint style="success" %}
**Porta 8080 & Host 0.0.0.0** – Sua aplicação **deve** ouvir na porta `8080` e host `0.0.0.0` para ser acessível externamente.
{% endhint %}

{% hint style="success" %}
[**Subdomínio**](../faq/general-questions/how-to-create-a-subdomain.md) – Você deve registrar um subdomínio único na Discloud.
{% endhint %}

{% hint style="success" %}
[**`discloud.config`**](../configurations/discloud.config/) – Necessário para a maioria dos métodos de implantação. Se estiver usando o [**Quick Setup**](../how-to-host-using/discord-bot.md#quick-setup-step-by-step-guide) do Bot do Discord, o bot irá guiá-lo através da configuração.
{% endhint %}

{% hint style="success" %}
**RAM** – Um mínimo de **512MB** é recomendado para aplicações web.
{% endhint %}

***

## 🚀 Guia de Hospedagem Passo a Passo

{% stepper %}
{% step %}
**📡 Registrar um Subdomínio**

Antes de implantar, você precisa reservar seu endereço único no domínio `.discloud.app`.
{% endstep %}

{% step %}
**📝 Configurar `discloud.config`**

Seu arquivo [`discloud.config`](../configurations/discloud.config/) diz à Discloud como lidar com seu site. Você deve definir `TYPE=site` e incluir seu `ID`.

{% hint style="info" %}
Se você estiver usando o **Quick Setup** do Bot do Discord, não precisa criar este arquivo manualmente, o bot solicitará o subdomínio e outros detalhes durante o processo.
{% endhint %}

```ini
NAME=MinhaAPIIncrivel
TYPE=site
ID=meu-subdominio-unico
MAIN=src/index.js
RAM=512
VERSION=latest
```

* **`TYPE=site`**: Identifica a aplicação como um serviço web.
* **`ID`**: O nome do seu subdomínio registrado. **Não** inclua `.discloud.app` (ex: use `minha-app`, não `minha-app.discloud.app`).
* **`MAIN`**: O ponto de entrada da sua aplicação.
* **`RAM`**: Memória alocada (mín. 512MB para sites).
{% endstep %}

{% step %}
**🏗️ Lidando com Processos de Build**

Se a sua aplicação exigir uma etapa de build (como React, Next.js ou TypeScript), você tem duas opções:

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

Neste caso, certifique-se de que seu `MAIN` ou `START` aponte para o ponto de entrada correto dentro da sua pasta de build.
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
