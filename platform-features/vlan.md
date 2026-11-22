---
description: >-
  Ligue aplicações e bancos de dados da Discloud numa rede interna, sem expor
  portas na internet pública.
icon: network-wired
---

# Rede Privada (VLAN)

## 🧭 Visão Geral

A VLAN liga aplicações e bancos de dados da Discloud numa **rede interna**. O tráfego não sai para a internet pública: um backend fala com um PostgreSQL ou um Redis pelo hostname interno, sem abrir nenhuma porta externa.

A VLAN **não** substitui o domínio, o subdomínio nem a rede pública do site. São caminhos diferentes:

| Rede               | Para que serve                                                                                                                                                  |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pública**        | Site ou API acessível na internet, pelo [subdomínio](../faq/general-questions/how-to-create-a-subdomain.md) ou por um [domínio personalizado](custom-domain.md) |
| **Privada (VLAN)** | Aplicação ↔ aplicação ou aplicação ↔ banco de dados **dentro** da Discloud, no mesmo cluster                                                                    |

<figure><img src="../.gitbook/assets/vlan-private-network.png" alt="Diagrama da rede privada (VLAN): o site recebe o tráfego público e fala com a API interna e com o banco de dados no mesmo cluster"><figcaption></figcaption></figure>

***

## 📋 Requisitos

Para usar a rede privada, você deve atender a estes critérios:

{% hint style="success" %}
[**Plano Diamond ou superior**](https://discloud.com/plans) – O plano que conta é o do **dono** da aplicação ou do banco de dados.
{% endhint %}

{% hint style="success" %}
**Mesmo cluster** – A VLAN não cruza clusters. As aplicações e os bancos de dados que se comunicam precisam estar no mesmo cluster.
{% endhint %}

{% hint style="info" %}
Numa aplicação compartilhada por uma [equipe](teams-and-permissions.md), o membro precisa da permissão `config_app` para mudar a rede privada. O plano que libera a VLAN continua sendo o do dono.
{% endhint %}

***

## ⚙️ Configurar

{% tabs %}
{% tab title="Painel" %}
[Painel da Discloud](https://discloud.com/dashboard) → aplicação → **Configurações** → card **Rede Privada (VLAN)**.

1. Ative o interruptor **Rede privada**.
2. Defina o **Hostname interno** (ex.: `api-interna`, `meu-cache`).
3. Clique em **Salvar**.

Abaixo do plano Diamond, o card fica desativado e mostra "Disponível a partir do plano Diamond".
{% endtab %}

{% tab title="discloud.config" %}
No upload ou no commit, use as chaves `VLAN` e `HOSTNAME` no [`discloud.config`](../configurations/discloud.config/):

{% code title="discloud.config" %}
```properties
NAME=Meu Serviço Mongo
VLAN=true
HOSTNAME=mymongoserver
```
{% endcode %}

| Chave      | Obrigatória | Função                                                         |
| ---------- | ----------- | -------------------------------------------------------------- |
| `VLAN`     | Sim         | Liga a rede privada nesta aplicação                            |
| `HOSTNAME` | Recomendada | Nome pelo qual as **outras** aplicações na VLAN encontram esta |
{% endtab %}

{% tab title="Banco de dados" %}
[Painel da Discloud](https://discloud.com/dashboard/databases) → banco de dados → **Configurações** → **Hostname · rede privada**.

A visão geral do banco já mostra o host, a porta e a URL da **conexão privada**. Esse host só responde para aplicações no mesmo cluster e com a VLAN ativada. Os formatos de URL estão em [Bancos de Dados](databases.md).
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Mudar a VLAN ou o hostname faz um **rebuild** da aplicação. Acompanhe o progresso até terminar.
{% endhint %}

{% hint style="info" %}
Se o painel e o `discloud.config` tiverem valores diferentes, vale o que foi aplicado no último deploy ou rebuild. Use só um dos dois para não se perder.
{% endhint %}

***

## 🧵 Regras do hostname

| Regra      | Valor                                                                         |
| ---------- | ----------------------------------------------------------------------------- |
| Caracteres | `a-z`, `0-9` e hífen (`-`)                                                    |
| Tamanho    | De 1 a 25 caracteres                                                          |
| Unicidade  | Não use o mesmo hostname em duas aplicações. O comportamento fica indefinido. |
| Maiúsculas | Prefira tudo em minúsculas                                                    |

No banco de dados, se o hostname ainda não foi definido, o painel mostra `{id}.discloud`. Prefira definir um hostname claro e estável.

***

## 🔗 Conectar duas aplicações

Para uma aplicação A falar com uma aplicação ou banco de dados B:

1. A e B precisam estar no **mesmo cluster**.
2. A VLAN precisa estar ativada nos lados que precisam ser alcançados, na aplicação que conecta e no serviço que escuta, conforme o caso.
3. As credenciais e a URL ficam nas [variáveis de ambiente](environment-variables.md), nunca no Git.
4. Depois de mudar a VLAN, o hostname ou as variáveis, faça rebuild ou um novo deploy.

{% hint style="info" %}
Se a aplicação estiver em outro cluster, vinculá-la a um [Projeto](projects.md) pode migrá-la para o cluster do Projeto. Aplicações com **Dockerfile** não migram automaticamente.
{% endhint %}

***

## 🧷 Exemplos

### 🗄️ Aplicação → banco de dados gerenciado

1. Crie o banco (PostgreSQL, MySQL, MongoDB, Redis ou Valkey). Isso exige o plano Diamond ou superior.
2. Copie a URL privada na visão geral do banco.
3. Na aplicação, no mesmo cluster, ative a VLAN e guarde a URL numa variável, como `DATABASE_URL`.
4. Faça rebuild da aplicação e confira a conexão nos logs.

<figure><img src="../.gitbook/assets/database-private-connection.png" alt="Diagrama da aplicação acessando o banco pela rede privada"><figcaption></figcaption></figure>

### 🔁 Aplicação → aplicação (API interna)

O serviço ativa a VLAN e define o hostname:

{% code title="discloud.config" %}
```properties
VLAN=true
HOSTNAME=billing-api
```
{% endcode %}

Outra aplicação, na mesma VLAN e no mesmo cluster, chama o serviço pelo hostname:

```
http://billing-api:8080/internal/...
```

A porta é a que o processo escuta **dentro** da aplicação, não a porta pública do site.

O mesmo vale para um banco hospedado numa aplicação. Com um MongoDB na aplicação de `HOSTNAME=mymongoserver`, o backend conecta assim:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import mongoose from "mongoose";

const uri = "mongodb://mymongoserver:27017/mydatabase";
//                            ^
//                            HOSTNAME da aplicação do MongoDB

async function main() {
  try {
    await mongoose.connect(uri);
    console.log("Conectado ao MongoDB com sucesso");
  } catch (error) {
    console.error("Erro de conexão MongoDB:", error);
    process.exit(1);
  }
}

main();
```
{% endtab %}

{% tab title="Node (Driver Nativo)" %}
```javascript
import { MongoClient } from "mongodb";
const uri = "mongodb://mymongoserver:27017/mydatabase";
const client = new MongoClient(uri);
await client.connect();
console.log("Ping:", await client.db().command({ ping: 1 }));
```
{% endtab %}

{% tab title="Python" %}
```python
from pymongo import MongoClient
client = MongoClient('mongodb://mymongoserver:27017/mydatabase')
print(client.admin.command('ping'))
```
{% endtab %}
{% endtabs %}

### ⚡ Cache Redis entre bots

1. Crie um Redis gerenciado, ou hospede o Redis numa aplicação com `VLAN=true` e `HOSTNAME=cache`.
2. Nos bots, no mesmo cluster e com a VLAN ativada, use `REDIS_URL=redis://default:SENHA@cache:PORTA`, ou o host e a porta que o painel mostrar.

***

## 🚫 O que a VLAN não faz

* Não publica o serviço na internet.
* Não libera o acesso do seu computador ao banco de dados. Para isso, use os [Templates](https://discloud.com/dashboard/templates) do painel (Tailscale, Tunnel TCP, Adminer ou SQLPad). O acesso público direto ao banco ainda não está no painel.
* Não substitui a autenticação. Continue usando usuário, senha e segredos nas variáveis de ambiente.
* Não liga aplicações de contas diferentes nem de clusters diferentes.

***

## 🛡️ Segurança

* Só as suas aplicações, ou as da equipe no Projeto, com a VLAN ativada e no mesmo cluster se alcançam.
* Desative a VLAN nas aplicações que não precisam ser acessadas internamente.
* Troque as senhas do banco se elas vazarem. A VLAN reduz a exposição, mas não substitui boas credenciais.
* Sites públicos continuam na rede pública. Use a VLAN só para o caminho interno, como API → banco de dados ou bot → cache.
