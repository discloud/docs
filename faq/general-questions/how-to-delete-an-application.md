---
description: >-
  Exclua uma aplicação no painel dash v4: selecione na AppsTable, use Excluir na
  bulk-bar e confirme digitando excluir.
icon: trash
---

# Como excluir uma aplicação?

## 🗑️ Visão geral

No [Dashboard](https://discloud.com/dashboard) (dash v4), a exclusão é pela **lista de aplicações** (`AppsTable`): você marca o(s) app(s) e usa a **bulk-bar** → **Excluir**.

Dá para excluir **um ou vários** apps de uma vez.

{% hint style="danger" %}
A exclusão é **permanente e irreversível**. Para confirmar, o painel exige digitar a palavra **`excluir`**.

Em alguns casos ainda pode haver [Snapshots](../../platform-features/snapshots.md) na conta — isso não é um backup completo dos arquivos.
{% endhint %}

***

## 🚀 Passo a passo (dash v4)

{% stepper %}
{% step %}
**Abrir a lista de apps**

Abra o [Dashboard](https://discloud.com/dashboard). A lista principal usa a `AppsTable` (busca, View, filtros Status/Tipo/Linguagem/Projeto, Upload).
{% endstep %}

{% step %}
**Selecionar a aplicação**

Marque a **checkbox** à esquerda do app. Aparece a bulk-bar com “1 selecionado” e as ações Iniciar / Parar / Reiniciar / **Excluir**.

<figure><img src="../../.gitbook/assets/v4-delete-1-list.png" alt="AppsTable dash v4 com MeuBot selecionado e bulk-bar"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Clicar em Excluir**

Na bulk-bar, clique em **Excluir** (ícone de lixeira).

<figure><img src="../../.gitbook/assets/v4-delete-2-bulk.png" alt="Bulk-bar dash v4 com Excluir destacado"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Confirmar digitando excluir**

O modal lista o nome e o ID do(s) app(s). Digite **`excluir`** no campo e clique em **Excluir** — ou **Cancelar**.

<figure><img src="../../.gitbook/assets/v4-delete-3-modal.png" alt="Modal dash v4 pedindo para digitar excluir"><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

***

## ✅ O que acontece depois

* O painel exclui cada app selecionado.
* Em sucesso, o app some da lista (e você permanece em `/dashboard`).
* Se algum falhar, aparece um aviso; os outros podem ter sido excluídos mesmo assim.

***

## ⚠️ Antes de excluir

| Situação              | O que fazer                                                              |
| --------------------- | ------------------------------------------------------------------------ |
| Precisa dos arquivos  | Faça [backup](../../platform-features/backups.md) ou baixe o que importa |
| Domínio / subdomínio  | Liberam depois; o subdomínio pode ficar **Livre** de novo                |
| App em equipe         | Só quem tem permissão consegue excluir                                   |
| Quer histórico depois | Veja [Snapshots](../../platform-features/snapshots.md)                   |

{% hint style="info" %}
As imagens seguem a **dash v4** (`/dashboard`, `AppsTable`). Também dá para excluir pela overview do app (`/dashboard/app/{id}`), digitando o **nome** do app no modal.
{% endhint %}
