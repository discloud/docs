---
description: >-
  Mapa do painel Discloud: menus laterais e caminhos para achar apps, bancos,
  domínios, VPS, CDN e configurações.
icon: map-location-dot
---

# Onde fica cada coisa no painel?

O painel fica em [discloud.com/dashboard](https://discloud.com/dashboard). A navegação principal é a **barra lateral** (sidebar). Alguns itens só aparecem depois que você abre um app, um banco, um VPS ou um projeto.

{% hint style="info" %}
Alguns menus dependem do **plano** ou de permissão em equipe. Se um item estiver bloqueado ou sumir, confira o plano da conta e o acesso ao recurso.
{% endhint %}

***

## 📌 Menu principal (sempre na sidebar)

| Onde            | Caminho                | O que é                                      |
| --------------- | ---------------------- | -------------------------------------------- |
| Overview        | `/dashboard/overview`  | Resumo da conta                              |
| Projetos        | `/dashboard/projects`  | Agrupar apps e bancos                        |
| Apps            | `/dashboard`           | Lista de aplicações                          |
| Bancos de dados | `/dashboard/databases` | Databases gerenciados                        |
| Domínios        | `/dashboard/domains`   | Subdomínios Discloud e domínio personalizado |
| VPS             | `/dashboard/vps`       | Cota e máquinas VPS                          |
| CDN             | `/dashboard/cdn`       | Arquivos públicos na CDN                     |

Storage pode aparecer na sidebar, mas ainda não está disponível para uso.

***

## 📱 Dentro de uma aplicação

Abra um app na lista (ou em `/dashboard/app/{id}`). A sidebar passa a mostrar o menu **daquele app**:

| Item                  | Caminho                            |
| --------------------- | ---------------------------------- |
| Overview              | `/dashboard/app/{id}`              |
| Logs                  | `/dashboard/app/{id}/logs`         |
| Deploy                | `/dashboard/app/{id}/deploy`       |
| Console               | `/dashboard/app/{id}/console`      |
| Métricas              | `/dashboard/app/{id}/metrics`      |
| Backups               | `/dashboard/app/{id}/backups`      |
| Atividade             | `/dashboard/app/{id}/activity`     |
| Variáveis de ambiente | `/dashboard/app/{id}/env`          |
| Arquivos              | `/dashboard/app/{id}/files`        |
| Edge                  | `/dashboard/app/{id}/edge` (sites) |
| Configurações         | `/dashboard/app/{id}/settings`     |

Para **voltar** à lista de apps, use o link de voltar no topo da sidebar do app.

***

## 🗄️ Dentro de um banco de dados

Abra um database em `/dashboard/databases/{id}`:

| Item          | Caminho                     |
| ------------- | --------------------------- |
| Overview      | `/dashboard/databases/{id}` |
| Logs          | `.../logs`                  |
| Métricas      | `.../metrics`               |
| Backups       | `.../backups`               |
| DB Studio     | `.../studio`                |
| Configurações | `.../settings`              |

Criar um banco novo: `/dashboard/databases/create`.

***

## 🖥️ Dentro de uma VPS

| Item                     | Caminho                        |
| ------------------------ | ------------------------------ |
| Lista / comprar recursos | `/dashboard/vps`               |
| Overview da máquina      | `/dashboard/vps/{id}`          |
| Configurações            | `/dashboard/vps/{id}/settings` |

***

## 📁 Dentro de um projeto

| Item                 | Caminho                    |
| -------------------- | -------------------------- |
| Overview             | `/dashboard/projects/{id}` |
| Acesso               | `.../access`               |
| Variáveis do projeto | `.../env`                  |
| Configurações        | `.../settings`             |

***

## 🛠️ Ferramentas (grupo na sidebar)

| Item       | Caminho                |
| ---------- | ---------------------- |
| Builds     | `/dashboard/builds`    |
| Snapshots  | `/dashboard/snapshots` |
| Atividade  | `/dashboard/activity`  |
| Templates  | `/dashboard/templates` |
| API Keys   | `/dashboard/api-key`   |
| Env global | `/dashboard/env`       |

***

## ⚙️ Conta, equipe e integrações

| Item                 | Onde                                             |
| -------------------- | ------------------------------------------------ |
| Equipes              | `/dashboard/teams`                               |
| GitHub               | `/dashboard/github`                              |
| Conta / perfil       | menu do usuário → Conta (`/dashboard/account`)   |
| Assinatura / billing | menu do usuário → Billing (`/dashboard/billing`) |

***

## 🔎 Atalhos úteis

| Quero…                        | Vá em                                                               |
| ----------------------------- | ------------------------------------------------------------------- |
| Excluir ou reiniciar um app   | Lista de **Apps** (`/dashboard`) — selecione e use a barra de ações |
| Subdomínio ou domínio próprio | **Domínios**                                                        |
| Token da API                  | **API Keys** (ferramentas)                                          |
| Variáveis de todas as apps    | **Env global** (ferramentas) ou env de cada app                     |
| Arquivos estáticos públicos   | **CDN**                                                             |
| Servidor Linux com SSH        | **VPS**                                                             |

{% content-ref url="../general-questions/how-to-delete-an-application.md" %}
[how-to-delete-an-application.md](../general-questions/how-to-delete-an-application.md)
{% endcontent-ref %}
