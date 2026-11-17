---
description: >-
  O que verificar quando o bot aparece online no Discord mas não responde a
  comandos ou mensagens.
---

# Por que meu bot não responde?

Se o bot aparece **online** no Discord mas ignora comandos e mensagens, a aplicação está rodando. O problema quase sempre está nas permissões do Discord ou na configuração do bot, e não na Discloud.

***

## 🔎 Comece pelos logs

Abra os [logs](../general-questions/how-to-access-the-application-logs.md) da aplicação e procure erros logo depois da inicialização. Algumas mensagens comuns:

| Mensagem nos logs                         | O que significa                                                    |
| ----------------------------------------- | ------------------------------------------------------------------ |
| `Used disallowed intents`                 | O código pede uma intent que não está ativada no Developer Portal. |
| `An invalid token was provided`           | O token do bot está errado, expirou ou foi regenerado.             |
| `Missing Access` ou `Missing Permissions` | O bot não tem permissão no servidor ou no canal.                   |

***

## ⚙️ Intents

O Discord só entrega eventos que o bot declara nas **intents**. Algumas delas, as **privilegiadas**, também precisam ser ativadas no [Discord Developer Portal](https://discord.com/developers/applications), em **Bot → Privileged Gateway Intents**:

* **Message Content Intent**, para ler o conteúdo das mensagens (comandos com prefixo, como `!ping`).
* **Server Members Intent**, para eventos e listas de membros.
* **Presence Intent**, para status e atividades dos usuários.

Depois de ativar no portal, declare as mesmas intents no código:

{% tabs %}
{% tab title="discord.js" %}
```javascript
const { Client, GatewayIntentBits } = require("discord.js");

const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.MessageContent,
  ],
});
```
{% endtab %}

{% tab title="discord.py" %}
```python
import discord

intents = discord.Intents.default()
intents.message_content = True

client = discord.Client(intents=intents)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Se o bot usa só **slash commands**, a Message Content Intent não é necessária.
{% endhint %}

***

## 🧩 Slash commands

Se os comandos de barra não aparecem ou não respondem:

* Confira se os comandos foram **registrados** pelo código. Comandos globais podem levar um tempo para aparecer.
* Confira se o bot foi convidado com o escopo **`applications.commands`**, além do escopo `bot`.
* Responda à interação em até **3 segundos**. Se a ação demora mais, use um `deferReply` (discord.js) ou `defer` (discord.py) antes.

***

## 🔐 Permissões no servidor

* Confira o cargo do bot nas configurações do servidor e nas permissões de cada canal.
* O bot precisa de **Ver canal** e **Enviar mensagens** no canal onde deve responder.
* Se mudou as permissões no convite, convide o bot de novo com o link atualizado.

***

## 🔑 Token

Se o token foi regenerado no Developer Portal, o antigo para de funcionar. Atualize o token nas [variáveis de ambiente](../../platform-features/environment-variables.md) da aplicação e faça um rebuild ou um novo deploy.

***

## ❓ Ainda precisa de ajuda?

Veja [**Soluções de Problemas**](./) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
