---
description: >-
  Boas práticas para guardar tokens e senhas da sua aplicação e o que fazer se
  um deles vazar.
---

# Como proteger meus tokens?

Tokens, senhas e chaves de API dão acesso à sua aplicação e às suas contas. Quem tiver o token do seu bot consegue controlá-lo.

***

## ✅ Boas práticas

* Guarde segredos nas [**variáveis de ambiente**](../../platform-features/environment-variables.md) do painel, nunca direto no código.
* Leia os valores no código pelas variáveis, por exemplo `process.env.TOKEN` ou `os.getenv("TOKEN")`.
* Não envie o arquivo [`.env`](.env-file.md) para o GitHub. Adicione-o ao `.gitignore`.
* Não guarde segredos no [`discloud.config`](../../configurations/discloud.config/).
* Não mostre tokens em prints, vídeos ou mensagens de suporte.
* Dê acesso às aplicações por [equipes](../../platform-features/teams-and-permissions.md), com o papel certo para cada pessoa, em vez de compartilhar a sua conta.

{% hint style="warning" %}
Um repositório público com um token, mesmo por pouco tempo, deve ser tratado como vazamento. Existem robôs que procuram tokens no GitHub o tempo todo.
{% endhint %}

***

## 🚨 Se um token vazou

{% stepper %}
{% step %}
**Gere um token novo**

Gere o token de novo no serviço de origem. No caso de um bot do Discord, use **Reset Token** no [Developer Portal](https://discord.com/developers/applications). O token antigo para de funcionar na hora.
{% endstep %}

{% step %}
**Atualize as variáveis**

Coloque o token novo nas variáveis de ambiente da aplicação e faça um rebuild ou um novo deploy.
{% endstep %}

{% step %}
**Não basta apagar o arquivo**

Se o token foi parar no Git, apagar o arquivo não basta: ele continua no histórico. Gerar um token novo é o que resolve.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
O mesmo vale para o [token da API da Discloud](how-can-i-get-my-discloud-api-token.md). Se ele vazar, gere um novo.
{% endhint %}
