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

Você escolhe o motor, a versão e a RAM. A Discloud sobe o banco, mostra as credenciais e deixa suas aplicações se conectarem a ele pela **rede privada** (VLAN), no mesmo cluster.

{% hint style="info" %}
A RAM dos bancos de dados conta para o limite de RAM do seu plano, junto com as aplicações.
{% endhint %}

### Requisitos

| Recurso                         | Plano mínimo                              |
| ------------------------------- | ----------------------------------------- |
| Criar um banco gerenciado       | [**Diamond**](https://discloud.com/plans) |
| Hostname na rede privada (VLAN) | **Diamond**                               |
| Backup automático diário        | **Diamond**                               |
| DB Studio                       | **Ruby**                                  |

Em um banco compartilhado por uma equipe, o membro acessa conforme as permissões dele. O plano que libera Studio, VLAN e backup automático é o do **dono** do banco.

### Onde fica

[Painel da Discloud](https://discloud.com/dashboard/databases) → **Banco de dados**. Dentro de cada banco:

| Página            | Para que serve                                                                     |
| ----------------- | ---------------------------------------------------------------------------------- |
| **Visão geral**   | Status, credenciais, URL de conexão e as ações iniciar, parar, reiniciar e excluir |
| **Logs**          | Saída do banco, ao vivo e em histórico                                             |
| **Métricas**      | Memória, CPU, disco e rede                                                         |
| **Backups**       | Cópias diárias, backup na hora, download e restore                                 |
| **Studio**        | Editor visual e queries (Ruby ou superior)                                         |
| **Configurações** | Nome exibido, hostname na VLAN, RAM e exclusão                                     |

### Motores disponíveis

| Motor          | RAM mínima | Credenciais na criação        | Extensões opcionais       |
| -------------- | ---------- | ----------------------------- | ------------------------- |
| **PostgreSQL** | 512 MB     | Nome da base, usuário e senha | **pgvector**, **PostGIS** |
| **MySQL**      | 512 MB     | Nome da base, usuário e senha | Nenhuma                   |
| **MongoDB**    | 512 MB     | Nome da base, usuário e senha | Nenhuma                   |
| **Redis**      | 100 MB     | Só a senha                    | Nenhuma                   |
| **Valkey**     | 100 MB     | Só a senha                    | Nenhuma                   |

As versões disponíveis aparecem na tela de criação e podem mudar. Confira sempre o que o painel mostra.

* **pgvector** adiciona busca por similaridade de vetores ao PostgreSQL.
* **PostGIS** adiciona dados geográficos e consultas espaciais ao PostgreSQL.

{% hint style="info" %}
#### **Precisa de Outro Motor?**

Abra um [ticket de suporte](https://discord.com/channels/@me/930852077045940224/) no [servidor Discord](https://discord.discloudbot.com/) com o nome do motor, versão e caso de uso. A equipe avalia a viabilidade.
{% endhint %}

***

## 🚀 Criar um banco de dados

{% stepper %}
{% step %}
**Abrir a criação**

Abra a seção **Banco de dados** e clique em [**Criar database**](https://discloud.com/dashboard/databases/create).
{% endstep %}

{% step %}
**Escolher motor e versão**

Escolha o **motor** e a **versão**. No PostgreSQL, ative **pgvector** e **PostGIS** se precisar.
{% endstep %}

{% step %}
**Preencher os dados**

* **Nome do serviço:** o nome do banco na Discloud. De 2 a 32 caracteres, começando com letra ou número. Aceita letras, números, `_` e `-`.
* **Credenciais:** nome da base, usuário e senha. O usuário **não** pode ser `root`. Redis e Valkey pedem só a senha, com no mínimo 8 caracteres.
{% endstep %}

{% step %}
**Projeto e RAM**

Se quiser, vincule o banco a um **Projeto**. Ajuste a **RAM** sem ficar abaixo do mínimo do motor.
{% endstep %}

{% step %}
**Criar**

Clique em **Criar base de dados** e acompanhe os logs. O banco pode levar alguns instantes para ficar **Online** depois da mensagem de sucesso.
{% endstep %}
{% endstepper %}

### Status e ações

Na visão geral, o status pode ser **Online**, **Offline**, **Erro** ou **RAM** (o banco parou por falta de memória). Dali você pode **iniciar**, **parar**, **reiniciar** ou **excluir** o banco.

{% hint style="danger" %}
Excluir um banco de dados é **permanente**. Os dados e o serviço são apagados.
{% endhint %}

***

## 🔌 Conexão privada (VLAN)

O banco **não fica na internet pública**. Só aplicações na Discloud, no **mesmo cluster** e com a [**VLAN**](../configurations/discloud.config/vlan.md) ativada, conseguem acessá-lo.

<figure><img src="../.gitbook/assets/database-private-connection.png" alt="Diagrama da aplicação acessando o banco pela rede privada"><figcaption></figcaption></figure>

No card **Conexão privada** da visão geral você copia:

| Campo                          | Conteúdo                                                                     |
| ------------------------------ | ---------------------------------------------------------------------------- |
| **Host**                       | O hostname na VLAN, ou `{id}.discloud` se o hostname ainda não foi definido. |
| **Porta**                      | A porta do motor na rede privada.                                            |
| **Database / Usuário / Senha** | As credenciais do motor. No Redis e no Valkey, o usuário é `default`.        |
| **URL**                        | A string de conexão pronta, no formato do motor.                             |

Formatos de URL que o painel monta:

{% code title="URL de conexão" %}
```
postgresql://USER:PASS@HOST:PORT/DB
mysql://USER:PASS@HOST:PORT/DB
mongodb://USER:PASS@HOST:PORT/DB?authSource=admin
redis://default:PASS@HOST:PORT
```
{% endcode %}

### Conectar uma aplicação

{% stepper %}
{% step %}
**Ativar a VLAN**

Nas configurações da aplicação, ative a **rede privada (VLAN)**. Isso exige o plano Diamond ou superior no dono da aplicação.
{% endstep %}

{% step %}
**Usar o mesmo cluster**

A aplicação precisa estar no mesmo cluster do banco. Um **Projeto** ajuda a manter os dois juntos.
{% endstep %}

{% step %}
**Guardar a URL nas variáveis**

Cole o host, a porta ou a URL nas **variáveis de ambiente** da aplicação, nunca no Git.
{% endstep %}

{% step %}
**Fazer rebuild ou deploy**

Faça rebuild ou um novo deploy da aplicação para ela receber as variáveis.
{% endstep %}
{% endstepper %}

### Acesso de fora da Discloud

O acesso público direto ao banco ainda **não** está disponível. Para acessá-lo do seu computador ou administrá-lo, use os [**Templates**](https://discloud.com/dashboard/templates) do Painel:

* [**Tailscale**](https://discloud.com/dashboard/templates/tailscale-discloud), para alcançar a rede privada a partir da sua máquina.
* **Tunnel TCP**, que conecta o seu PC a um banco de dados na Discloud.
* **Adminer Painel SQL** e **SQLPad editor**, para administrar o banco pelo navegador.

***

## 📊 Logs e métricas

* **Logs:** saída do banco ao vivo e por intervalo de tempo, com busca, filtro por severidade, copiar, baixar e limpar. Ajuda a diagnosticar falhas na inicialização, falta de memória e erros do motor.
* **Métricas:** gráficos de memória (com o limite), CPU, leitura e escrita em disco e rede, em períodos de 1 a 30 dias. Use para dimensionar a RAM e perceber quando o banco está no limite.

***

## 💾 Backups

Banco de dados → **Backups**.

| Ação                     | Detalhe                                                                     |
| ------------------------ | --------------------------------------------------------------------------- |
| **Backup automático**    | Uma cópia por dia, guardada por cerca de **7 dias** (Diamond ou superior).  |
| **Criar backup**         | Gera uma cópia na hora. O progresso aparece na própria página.              |
| **Baixar / Copiar link** | Abre a janela de download com um link temporário.                           |
| **Restore**              | **Cria um banco novo** a partir do backup. O banco atual não é sobrescrito. |

No restore você pode definir o nome do banco novo, a RAM (mínimo de 100 MB) e o Projeto. Acompanhe a criação até o banco novo aparecer na lista.

<figure><img src="../.gitbook/assets/database-backup-restore.png" alt="Diagrama do restore criando um banco novo a partir de um backup"><figcaption></figcaption></figure>

***

## 🧪 DB Studio

Banco de dados → **Studio**. É um editor dentro do painel e exige o plano **Ruby ou superior** no dono do banco.

| Recurso                                   | PostgreSQL / MySQL                        | MongoDB               | Redis / Valkey    |
| ----------------------------------------- | ----------------------------------------- | --------------------- | ----------------- |
| Listar tabelas ou coleções                | Sim                                       | Sim                   | Não               |
| Aba **Dados** (criar, editar, excluir)    | Sim                                       | Sim (documentos JSON) | Não               |
| Aba **Estrutura**                         | Colunas, chave primária e índices         | Metadados da coleção  | Não               |
| Aba **Query**                             | SQL                                       | Comandos e `find`     | Limitada ao motor |
| Criar, excluir ou esvaziar tabela/coleção | Sim                                       | Sim                   | Não               |
| Importar SQL                              | Sim, por arquivo ou texto, até **100 MB** | Não                   | Não               |
| Exportar                                  | CSV, SQL ou JSON                          | Sim                   | Não               |

{% hint style="warning" %}
* O banco precisa estar **online**.
* A importação de SQL bloqueia comandos perigosos, como `DROP DATABASE`, `GRANT`, `REVOKE` e `CREATE USER`.
* Sem uma chave primária conhecida, editar ou excluir uma linha exige a aba **Query**.
* A exportação tem limite por lote. Para volumes grandes, use a aba **Query**.
* As queries têm limite de uso e tempo máximo de cerca de 30 segundos. Se falhar, simplifique a query.
{% endhint %}

***

## ⚙️ Configurações

Banco de dados → **Configurações**.

| Campo                                     | Efeito                                                                                      |
| ----------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Nome na lista**                         | Só muda o nome exibido.                                                                     |
| **Hostname · rede privada**               | Nome do host na VLAN. Exige Diamond ou superior no dono. Mudar faz um **rebuild** do banco. |
| **RAM total (MB)**                        | Entre **100** e **16384**. Conta na cota do dono. Mudar também pode fazer rebuild.          |
| **Iniciar / Parar / Reiniciar / Excluir** | As mesmas ações da visão geral.                                                             |

Ao salvar uma mudança de hostname ou de RAM, o painel mostra o progresso do rebuild. Espere terminar antes de apontar as aplicações de novo.

Em um banco compartilhado por uma equipe, alterar configurações ou fazer rebuild exige a permissão `commit_app`, e alterar a RAM exige `edit_ram`.

Para automatizar, veja a [API de Banco de Dados](api-overview/database.md).

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

{% hint style="info" %}
Com o Atlas, as páginas de banco gerenciado da Discloud (Studio, Backups e Métricas) não se aplicam.
{% endhint %}

{% tabs %}
{% tab title="Vídeo explicativo recomendado" %}
{% embed url="https://youtu.be/kGPY9ZuJ0b0" %}
{% endtab %}
{% endtabs %}
