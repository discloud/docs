---
description: >-
  Crie bancos de dados gerenciados (PostgreSQL, MySQL, MongoDB, Redis e Valkey)
  pelo Painel da Discloud ou use um MongoDB Atlas externo.
icon: database
---

# Bancos de Dados

## 🧭 Visão Geral

Aplicações Discloud podem se conectar a:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="databases.md#managed-databases">#managed-databases</a></td><td>Bancos de dados gerenciados que você cria pelo Painel da Discloud.</td><td></td><td></td><td></td></tr><tr><td><a href="databases.md#external-mongodb-atlas">#external-mongodb-atlas</a></td><td>Provedor de banco de dados como serviço MongoDB Atlas externo que você configura manualmente.</td><td></td><td></td><td></td></tr></tbody></table>

***

## 🗄️ Bancos de Dados Gerenciados <a href="#managed-databases" id="managed-databases"></a>

Crie um banco de dados direto no [Painel da Discloud](https://discloud.com/dashboard/databases):

{% stepper %}
{% step %}
Abra a seção **Banco de dados** e clique em [**Criar database**](https://discloud.com/dashboard/databases/create).
{% endstep %}

{% step %}
Escolha o **motor** e a **versão**. No PostgreSQL, você pode ativar as extensões opcionais **pgvector** e **PostGIS**.
{% endstep %}

{% step %}
Defina o **nome do serviço** e as **credenciais** (nome da base de dados, usuário e senha). Redis e Valkey pedem apenas a senha.
{% endstep %}

{% step %}
Se quiser, escolha um **projeto** e ajuste a **RAM**. Depois clique em **Criar base de dados**.
{% endstep %}
{% endstepper %}

### Motores disponíveis

| Motor      | Versão padrão | RAM mínima |
| ---------- | ------------- | ---------- |
| PostgreSQL | 17            | 512 MB     |
| MySQL      | 9.0           | 512 MB     |
| MongoDB    | 8.0           | 512 MB     |
| Redis      | 8.0           | 100 MB     |
| Valkey     | 7.2           | 100 MB     |

{% hint style="info" %}
A RAM dos bancos de dados conta para o limite de RAM do seu plano, junto com as aplicações.
{% endhint %}

### Ferramentas para gerenciar bancos de dados

Na seção [**Templates**](https://discloud.com/dashboard/templates) do Painel há ferramentas prontas para trabalhar com bancos de dados, como o **Adminer Painel SQL**, o **SQLPad editor** e o **Tunnel TCP**, que conecta o seu PC a um banco de dados na Discloud.

{% hint style="info" %}
#### **Precisa de Outro Motor?**

Abra um [ticket de suporte](https://discord.com/channels/@me/930852077045940224/) no [servidor Discord](https://discord.discloudbot.com/) com o nome do motor, versão e caso de uso. A equipe avalia a viabilidade.
{% endhint %}

***

## 🌍 Usando MongoDB Atlas Externo <a href="#external-mongodb-atlas" id="external-mongodb-atlas"></a>

Se você optar pelo MongoDB Atlas em vez de um banco de dados gerenciado:

{% stepper %}
{% step %}
Crie um cluster gratuito ou pago em [https://www.mongodb.com/](https://www.mongodb.com/)
{% endstep %}

{% step %}
Em Network Access, adicione IP: `0.0.0.0/0` (Permitir de Qualquer Lugar) para que os contêineres Discloud possam se conectar.
{% endstep %}

{% step %}
Copie a string de conexão do cluster (**Connect → Drivers**) e salve-a como variável de ambiente (ex.: `MONGODB_URI` no seu [`.env`](../faq/general-questions/.env-file.md)).
{% endstep %}

{% step %}
Teste a conectividade localmente antes de fazer o upload, se possível.
{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="Vídeo explicativo recomendado" %}
{% embed url="https://youtu.be/kGPY9ZuJ0b0" %}
{% endtab %}
{% endtabs %}
