---
description: >-
  Baixe versões antigas das suas aplicações, inclusive depois que uma app foi
  excluída.
icon: clock-rotate-left
---

# Snapshots

## 🕒 O que são Snapshots?

Snapshots são **backups versionados** das suas aplicações, reunidos em um único lugar da conta. Servem para baixar uma versão antiga do código e dos arquivos de uma app, inclusive depois que ela foi excluída.

{% hint style="info" %}
Snapshots são diferentes da página **Backups** de cada app, que guarda as cópias diárias automáticas e gera o backup manual na hora.
{% endhint %}

***

## 📋 Requisitos

* Listar e baixar snapshots está disponível em **todos os planos**.
* Não existe um botão de "criar snapshot" no painel. As versões são criadas de outras formas (veja abaixo).

***

## 📍 Onde fica

[Painel da Discloud](https://discloud.com/dashboard) → **Snapshots** (no grupo Ferramentas).

Cada app da lista mostra quantas **versões** tem, o tamanho total e a data do último backup. A lista é dividida em páginas. Use a busca por ID para encontrar uma app rápido.

***

## 🧬 De onde vêm os snapshots

Os snapshots são criados de duas formas:

* **Pela API**, com a [API de Snapshot](../../api-and-integrations/api-overview/snapshot.md).
* **Automaticamente, quando uma aplicação é excluída.**

<figure><img src="../../.gitbook/assets/snapshots-sources.png" alt="Diagrama das origens dos snapshots e do download"><figcaption></figcaption></figure>

Ou seja, excluir uma app não faz você perder na hora a última versão dela. Essa versão aparece em Snapshots para download enquanto estiver dentro do prazo de retenção da Discloud.

***

## ⬇️ Baixar uma versão

{% stepper %}
{% step %}
**Abrir Snapshots**

No painel, abra **Snapshots**.
{% endstep %}

{% step %}
**Encontrar a app**

Localize a app na lista. Se precisar, busque pelo ID.
{% endstep %}

{% step %}
**Ver as versões**

Clique em **Ver versões**. As versões também são divididas em páginas.
{% endstep %}

{% step %}
**Baixar**

Na versão que você quer, clique em **Baixar** ou em **Copiar link**. O link é temporário. Se o navegador bloquear o download, use **Copiar link** e abra em outra aba.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Algumas versões mostram um prazo, como "Expira em X dias". Depois disso, elas saem da lista.
{% endhint %}

***

## 🔀 Snapshots, Backups e Deploy

| Recurso               | Para que serve                                                                         |
| --------------------- | -------------------------------------------------------------------------------------- |
| **Snapshots**         | Histórico de versões de cada app na conta. Útil depois de excluir uma app.             |
| **Backup manual**     | Cópia na hora, pela visão geral da app.                                                |
| **Backup automático** | Cópia diária por \~7 dias (Diamond ou superior), na página Backups da app ou do banco. |
| **GitHub / Commit**   | Código-fonte no repositório. Não substitui o snapshot dos arquivos da app hospedada.   |

O snapshot **não** restaura a app com um clique. Você baixa o arquivo e hospeda de novo, ou reaproveita o conteúdo como fizer sentido para o seu projeto.

***

## 💡 Boas práticas

* Antes de excluir uma app importante, faça também um **backup manual** e guarde fora da Discloud.
* Depois de excluir, confira **Snapshots** logo. Não espere o fim da retenção.
* Em uma equipe, quem baixa precisa da permissão certa no recurso. O dono da conta vê nesta tela os snapshots das apps dele.
* Não dependa só do snapshot para compliance ou retenção longa. Baixe e arquive o que for obrigatório guardar.
