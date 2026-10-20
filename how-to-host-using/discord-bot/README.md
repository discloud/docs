---
description: >-
  Aprenda a hospedar rapidamente suas aplicações através do nosso servidor
  Discord usando nosso bot.
icon: robot
---

# Bot do Discord

A Discloud permite que você **hospede aplicações diretamente do Discord**, tornando o upload rápido e acessível sem precisar usar um painel ou ferramentas de linha de comando.

{% hint style="info" %}
O bot usa **comandos de barra (slash)**. Veja a lista completa em [**Comandos do Bot**](commands.md).
{% endhint %}

***

## 🔑 Verificação de Conta

Antes de hospedar aplicações usando o **Discloud Bot**, você precisa **verificar sua conta** no servidor Discord da Discloud.

#### **🤔 Como verificar sua conta:**

{% stepper %}
{% step %}
Entre no [**Servidor Discord da Discloud**](https://discord.discloudbot.com/).
{% endstep %}

{% step %}
Siga as instruções disponíveis no canal de verificação.
{% endstep %}

{% step %}
Após concluir a verificação, você receberá o cargo **`Verified pt-br`**.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Depois da verificação, você terá acesso ao canal [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962), onde poderá gerenciar suas aplicações.
{% endhint %}

***

## 🚀 Hospedando Sua Aplicação

Há **duas maneiras** de fazer o upload de uma aplicação usando o Bot da Discloud:

<table><thead><tr><th width="212">Método</th><th>Melhor Para</th><th>Como Funciona</th></tr></thead><tbody><tr><td><a href="./#configuracao-avancada"><strong>⚙️ Configuração Avançada (recomendado)</strong></a></td><td>Usuários que querem fazer o <strong>upload com um único comando</strong>, com as configurações já definidas.</td><td>Configure tudo no arquivo <a href="../../configurations/discloud.config/"><code>discloud.config</code></a> e use <code>/upconfig</code>.</td></tr><tr><td><a href="./#configuracao-rapida-guia-passo-a-passo"><strong>⚡ Configuração Rápida (legado)</strong></a></td><td>Usuários que <strong>preferem uma configuração guiada</strong> através das perguntas do bot.</td><td>O bot perguntará os detalhes necessários após executar <code>/up</code>.</td></tr></tbody></table>

{% hint style="warning" %}
#### **Notas Importantes**

* Se seu [**arquivo principal**](../../faq/general-questions/what-is-the-main-file.md) **não estiver no** [**diretório raiz**](../../faq/general-questions/what-is-the-root-of-the-project.md), você **deve** usar Configuração Avançada ou movê-lo para a raiz.
* Se você estiver hospedando um **bot sem ID** (ex.: WhatsApp ou Telegram), use Configuração Avançada e a Discloud gerará o ID automaticamente.
{% endhint %}

{% tabs %}
{% tab title="📝 Configuração Avançada" %}
{% stepper %}
{% step %}
Crie o arquivo [`discloud.config`](../../configurations/discloud.config/).
{% endstep %}

{% step %}
Comprima seu projeto em um arquivo [`.zip`](../../faq/general-questions/em-andamento-como-comprimir.md).
{% endstep %}

{% step %}
Faça upload do seu projeto.

* Vá para [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) no **Servidor Discord da Discloud**.
*   Execute o seguinte comando:

    ```
    /upconfig
    ```
* Envie seu arquivo [**.zip**](../../faq/general-questions/em-andamento-como-comprimir.md) quando solicitado.
{% endstep %}

{% step %}
Sua aplicação será hospedada automaticamente.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="⚡ Configuração Rápida (Guia Passo a Passo)" %}
{% hint style="warning" %}
A Configuração Rápida é o **método antigo** e continua disponível, mas recomendamos a **Configuração Avançada** com `/upconfig`: as configurações ficam guardadas no `discloud.config` e servem para todos os métodos de upload.
{% endhint %}

{% tabs %}
{% tab title="🤖 Bot" %}
{% stepper %}
{% step %}
Prepare seu projeto.

* Certifique-se de que os arquivos da sua aplicação estejam estruturados corretamente.
* Comprima seu projeto em um arquivo [`.zip`](../../faq/general-questions/em-andamento-como-comprimir.md).
{% endstep %}

{% step %}
Faça upload do seu projeto.

* Vá para [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) no **Servidor Discord da Discloud**.
*   Execute o seguinte comando:

    ```
    /up
    ```
{% endstep %}

{% step %}
Forneça as Informações Necessárias.

* **Digite o** [**ID da Aplicação**](../../faq/general-questions/how-can-i-get-my-discord-bot-id.md) (para bots do Discord).
* **Digite o** [**Nome do Arquivo Principal**](../../faq/general-questions/what-is-the-main-file.md) (ex.: `index.js`, `main.py`, `main.go`).
* **Especifique a RAM** para seu bot (ex.: `100` para 100MB).

{% hint style="info" %}
Ao especificar a quantidade de RAM, você não precisa incluir unidades como "MB". Basta inserir o valor numérico, por exemplo, "100" para 100MB.

```
          BOTs requerem um mínimo de 100MB de RAM.
```
{% endhint %}
{% endstep %}

{% step %}
Envie seu arquivo [`.zip`](../../faq/general-questions/em-andamento-como-comprimir.md) quando solicitado.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🌐 Site" %}
{% stepper %}
{% step %}
Prepare seu projeto.

* Certifique-se de que os arquivos da sua aplicação estejam estruturados corretamente.
* Comprima seu projeto em um arquivo [`.zip`](../../faq/general-questions/em-andamento-como-comprimir.md).
{% endstep %}

{% step %}
Faça upload do seu projeto.

* Vá para [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) no **Servidor Discord da Discloud**.
*   Execute o seguinte comando:

    ```
    /upsite
    ```
{% endstep %}

{% step %}
Forneça as Informações Necessárias.

* **Escolha um** [**Subdomínio**](../../faq/general-questions/how-to-create-a-subdomain.md).
* **Digite o** [**Nome do Arquivo Principal**](../../faq/general-questions/what-is-the-main-file.md) (ex.: `index.html`, `index.php`).
* **Especifique a RAM** para seu site (ex.: `512` para 512MB).

{% hint style="info" %}
Ao especificar a quantidade de RAM, você não precisa incluir unidades como "MB". Basta inserir o valor numérico, por exemplo, "512" para 512MB.

```
           Sites requerem um mínimo de 512MB de RAM.
```
{% endhint %}
{% endstep %}

{% step %}
Envie seu arquivo [`.zip`](../../faq/general-questions/em-andamento-como-comprimir.md) quando solicitado.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## **❓ Ainda precisa de ajuda?**

Verifique a [**Seção FAQ**](https://app.gitbook.com/s/vUqkKIFudeQ2TQOirm35/faq) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
