---
description: >-
  Referência completa da REST API da Discloud: autenticação, endpoints e grupos
  de recursos.
icon: webhook
---

# Visão Geral da API

### 🌐 URL Base

Todas as requisições apontam para:

```
https://api.discloud.app/v2
```

***

### 🔑 Autenticação

Toda requisição exige o header `api-token` com o seu token pessoal:

```bash
api-token: SEU_TOKEN_AQUI
```

Consulte [Autenticação](./#autenticacao) para saber como obter e proteger o token.

***

### ⚡ Início Rápido

{% stepper %}
{% step %}
Obtenha seu token da API no Dashboard.
{% endstep %}

{% step %}
Faça sua primeira requisição para confirmar que o token funciona:

```bash
curl -X GET \
  -H "api-token: SEU_TOKEN_AQUI" \
  https://api.discloud.app/v2/user
```

Uma resposta `200 OK` com seus dados de usuário confirma que a autenticação está correta.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Nunca exponha seu token em código público ou repositórios Git. Armazene-o em variáveis de ambiente. Consulte [Autenticação](./#autenticacao) para boas práticas de segurança.
{% endhint %}
