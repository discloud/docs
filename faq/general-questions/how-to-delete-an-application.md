---
description: >-
  Exclua uma aplicação pelo Painel da Discloud: selecione na lista de apps, use
  Excluir na barra de ações e confirme no modal.
icon: trash
---

# Como excluir uma aplicação?

## 🗑️ Visão geral

No painel, a exclusão **não** fica dentro da página do app. Você exclui pela **lista de aplicações**: marca o(s) app(s) e usa a barra de ações em lote (**Excluir**).

Dá para excluir **um ou vários** apps de uma vez.

{% hint style="danger" %}
A exclusão é **permanente**. Os dados da aplicação são perdidos. Em alguns casos ainda pode haver [Snapshots](../../platform-features/snapshots.md) na conta — não confunda com backup completo.
{% endhint %}

***

## 🚀 Passo a passo

{% stepper %}
{% step %}
**Abrir a lista de apps**

No [Painel da Discloud](https://discloud.com/dashboard), vá até a área de **aplicações** (lista de apps da conta).
{% endstep %}

{% step %}
**Selecionar a aplicação**

Na tabela, marque a **checkbox** à esquerda do app que quer excluir. O painel mostra algo como “1 app selecionado” e libera a barra de ações.

<figure><img src="../../.gitbook/assets/delete-app-1-list.png" alt="Lista de apps com MeuBot selecionado e barra Iniciar Parar Reiniciar Excluir"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Clicar em Excluir**

Na barra de ações (Iniciar / Parar / Reiniciar / **Excluir**), clique em **Excluir** (ícone de lixeira).

<figure><img src="../../.gitbook/assets/delete-app-2-actions.png" alt="Barra de ações em lote com o botão Excluir destacado"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Confirmar no modal**

Abre um modal pedindo confirmação. Ele lista o nome e o ID do(s) app(s). Leia o aviso e clique em **Sim, deletar** — ou **Cancelar** se mudou de ideia.

<figure><img src="../../.gitbook/assets/delete-app-3-modal.png" alt="Modal de confirmação listando MeuBot para exclusão"><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

***

## ✅ O que acontece depois

* O painel chama a exclusão de cada app selecionado.
* Se der certo, o app some da lista.
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
As imagens desta página são **protótipos** fiéis ao fluxo do painel (sitev3). A UI real pode ter pequenos detalhes diferentes (idioma, tema, labels).
{% endhint %}
