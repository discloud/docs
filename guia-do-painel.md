---
description: >-
  Inventário de how-tos do painel dash v4: o que ensinar, status e links. Fonte
  para usuários e agentes de IA (com imagens quando o how-to existir).
icon: table-columns
---

# Guia do Painel

## 🎯 Para que serve

Este catálogo lista **tudo que dá para ensinar a usar no painel** (dash v4 em `/dashboard`).

* **Usuários** — encontram o how-to certo com passos e imagens.
* **Agentes de IA** — leem esta página para saber o que já está documentado, o que falta, a rota real e o padrão de UI.

Interface de referência: **somente dash v4** (`sitev3` → `routes/dashboard` + `$lib/v4`). Não usar o painel legado `/v3/`.

{% hint style="info" %}
How-tos com imagens usam **packs** (3–4 mockups fiéis à UI). Já publicado: [Como excluir uma aplicação?](faq/general-questions/how-to-delete-an-application.md).
{% endhint %}

***

## ✅ Publicado (com imagens)

| How-to                                                                               | Rota                                                              | Pack                 |
| ------------------------------------------------------------------------------------ | ----------------------------------------------------------------- | -------------------- |
| [Como excluir uma aplicação?](faq/general-questions/how-to-delete-an-application.md) | `/dashboard` → AppsTable → bulk Excluir → modal digitar `excluir` | lista + bulk + modal |

***

## 📦 Apps (lista `/dashboard`)

| How-to                                          | Rota / UI                   | Prioridade | Status    |
| ----------------------------------------------- | --------------------------- | ---------- | --------- |
| Excluir aplicação                               | AppsTable + modal `excluir` | Alta       | **Feito** |
| Iniciar / parar / reiniciar app(s)              | bulk-bar                    | Alta       | Pendente  |
| Fazer upload / criar app                        | `/dashboard/app/create`     | Alta       | Pendente  |
| Filtrar apps (status, tipo, linguagem, projeto) | AppsTable filtros           | Média      | Pendente  |
| Abrir overview do app                           | `/dashboard/app/{id}`       | Alta       | Pendente  |

***

## 📱 App (contexto `/dashboard/app/{id}`)

| How-to                                | Rota                        | Prioridade | Status                            |
| ------------------------------------- | --------------------------- | ---------- | --------------------------------- |
| Ver logs                              | `.../logs`                  | Alta       | Parcial (FAQ antiga, sem pack v4) |
| Deploy / GitHub deploy                | `.../deploy`                | Alta       | Pendente                          |
| Console web                           | `.../console`               | Média      | Pendente                          |
| Métricas                              | `.../metrics`               | Média      | Pendente                          |
| Backups da app                        | `.../backups`               | Alta       | Parcial (produto Backups)         |
| Atividade da app                      | `.../activity`              | Baixa      | Pendente                          |
| Variáveis de ambiente da app          | `.../env`                   | Alta       | Parcial (produto Env)             |
| Explorer de arquivos                  | `.../files`                 | Alta       | Pendente                          |
| Edge (rules / redirects)              | `.../edge`                  | Alta       | Parcial (produto Edge)            |
| Domínios do app                       | `.../domains`               | Alta       | Pendente                          |
| Configurações / excluir pelo overview | `.../settings` + modal nome | Alta       | Pendente                          |

***

## 🌐 Domínios

| How-to                                | Rota                 | Prioridade | Status            |
| ------------------------------------- | -------------------- | ---------- | ----------------- |
| Criar subdomínio Discloud             | `/dashboard/domains` | Alta       | Parcial (FAQ)     |
| Adicionar domínio personalizado + DNS | `/dashboard/domains` | Alta       | Parcial (produto) |
| Remover subdomínio / domínio          | modal type-confirm   | Média      | Pendente          |

***

## 🗄️ Bancos de dados

| How-to                   | Rota                          | Prioridade | Status   |
| ------------------------ | ----------------------------- | ---------- | -------- |
| Criar database           | `/dashboard/databases/create` | Alta       | Pendente |
| Lista / ações em massa   | `/dashboard/databases`        | Média      | Pendente |
| Overview, logs, métricas | `/dashboard/databases/{id}/…` | Média      | Pendente |
| Backups e restore        | `.../backups`                 | Alta       | Parcial  |
| DB Studio                | `.../studio`                  | Alta       | Pendente |
| Configurações / excluir  | `.../settings`                | Alta       | Pendente |

***

## 🖥️ VPS

| How-to                         | Rota                        | Prioridade | Status                |
| ------------------------------ | --------------------------- | ---------- | --------------------- |
| Comprar cota RAM/SSD           | `/dashboard/vps` → recursos | Alta       | Parcial (produto VPS) |
| Criar máquina                  | sheet criar VPS             | Alta       | Pendente              |
| SSH / overview                 | `/dashboard/vps/{id}`       | Alta       | Pendente              |
| Reiniciar / recriar / settings | overview + settings         | Alta       | Pendente              |
| Excluir VPS (type-confirm)     | settings                    | Alta       | Pendente              |

***

## ☁️ CDN e add-ons

| How-to                        | Rota             | Prioridade | Status            |
| ----------------------------- | ---------------- | ---------- | ----------------- |
| Comprar / ajustar add-on CDN  | billing / CDN    | Alta       | Parcial (produto) |
| Upload / pastas / URL pública | `/dashboard/cdn` | Alta       | Pendente          |
| Excluir arquivo/pasta         | modal CDN        | Média      | Pendente          |

***

## 📁 Projetos e equipes

| How-to                        | Rota                    | Prioridade | Status            |
| ----------------------------- | ----------------------- | ---------- | ----------------- |
| Criar projeto                 | `/dashboard/projects`   | Alta       | Pendente          |
| Adicionar apps/DBs ao projeto | detalhe projeto         | Alta       | Pendente          |
| Acesso / env do projeto       | `.../access`, `.../env` | Média      | Pendente          |
| Criar equipe e permissões     | `/dashboard/teams`      | Alta       | Parcial (produto) |

***

## 🛠️ Ferramentas

| How-to             | Rota                   | Prioridade | Status        |
| ------------------ | ---------------------- | ---------- | ------------- |
| Builds / operações | `/dashboard/builds`    | Média      | Pendente      |
| Snapshots          | `/dashboard/snapshots` | Alta       | Parcial       |
| Atividade da conta | `/dashboard/activity`  | Baixa      | Pendente      |
| Templates          | `/dashboard/templates` | Média      | Pendente      |
| API token          | `/dashboard/api-key`   | Alta       | Parcial (FAQ) |
| Env global         | `/dashboard/env`       | Alta       | Pendente      |
| Conectar GitHub    | `/dashboard/github`    | Alta       | Pendente      |
| Overview / tour    | `/dashboard/overview`  | Baixa      | Pendente      |

***

## 👤 Conta e billing

| How-to                      | Rota                 | Prioridade | Status   |
| --------------------------- | -------------------- | ---------- | -------- |
| Conta / perfil              | `/dashboard/account` | Média      | Pendente |
| Assinatura, planos, add-ons | `/dashboard/billing` | Alta       | Parcial  |

***

## 🧭 Nav do painel (sidebar)

Principais: Overview · Projetos · Apps · Databases · Domínios · VPS · CDN · (Storage em breve).

Ferramentas: Builds · Snapshots · Atividade · Templates · API Keys · Env global.

Config: Equipes · GitHub · Conta · Billing.

***

## 📐 Padrão de pack de imagens

1. Ler o Svelte da rota em dash v4.
2. HTML mockup com tokens Newman.
3. Screenshot (browser + http.server local).
4. Upload GitBook `insert_files` + página com stepper.
5. Atualizar **esta tabela** (Status → Feito + link).

{% hint style="success" %}
Próximos packs sugeridos (ordem): **iniciar/parar/reiniciar** → **upload app** → **criar subdomínio** → **domínio personalizado** → **criar database** → **CDN upload** → **criar VPS**.
{% endhint %}
