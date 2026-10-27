---
description: >-
  Canais e melhores práticas para obter ajuda com a Discloud: fóruns da
  comunidade, chat, áreas de doadores e suporte direto da equipe.
icon: bullseye-arrow
---

# Onde Obter Ajuda

## 🧾 Visão Geral

Existem múltiplas superfícies de suporte dependendo do que você precisa: solução de problemas da comunidade, perguntas sobre uso da plataforma, problemas de cobrança / conta ou escalação privada. Esta página explica onde postar e como perguntar efetivamente.

{% hint style="info" %}
A equipe se concentra em problemas da plataforma Discloud (upload, comportamento de hospedagem, conta, cobrança). Perguntas gerais de codificação são orientadas pela comunidade.
{% endhint %}

***

## 🗂️ Canais de Suporte

| Canal                                                                                           | Tipo                          | Público                | Uso Típico                                                 |
| ----------------------------------------------------------------------------------------------- | ----------------------------- | ---------------------- | ---------------------------------------------------------- |
| [Ticket Modmail (Direto)](https://discord.com/channels/@me/930852077045940224/)                 | Privado                       | Você ↔ Equipe          | Cobrança, conta, dados sensíveis, preocupações de política |
| [chat](https://discord.com/channels/584490943034425391/1051122908103192636)                     | Chat público                  | Todos os usuários      | Perguntas rápidas da plataforma, discussão leve            |
| [dev-help (Fórum)](https://discord.com/channels/584490943034425391/1052629984444948501)         | Público (em threads)          | Todos os usuários      | Ajuda da comunidade com código / configs                   |
| [donators-chat](https://discord.com/channels/584490943034425391/1051124971763679232)            | Público (restrito a doadores) | Usuários de plano pago | Discussão da comunidade de doadores                        |
| [donators-support (Fórum)](https://discord.com/channels/584490943034425391/1051124971763679232) | Público (restrito a doadores) | Usuários de plano pago | Perguntas técnicas relacionadas ao plano                   |
| [Documentação](https://docs.discloud.com/)                                                      | Autoatendimento               | Todos                  | Guias e referências oficiais                               |

***

## 🎫 Modmail (Ticket Direto da Equipe)

Use modmail para problemas que não devem ser públicos:

* Gerenciamento de cobrança ou assinatura
* Erros específicos da conta (suspensões, anomalias de acesso)
* Relatórios de segurança ou abuso
* Logs / PII sensíveis que devem permanecer privados

{% stepper %}
{% step %}
Abra um DM com [Modmail da Discloud](https://discord.com/channels/@me/930852077045940224/) para iniciar um ticket.
{% endstep %}

{% step %}
Forneça resumo conciso: tipo de problema + ID da app afetada / plano.
{% endstep %}

{% step %}
Anexe logs ou capturas relevantes (não sensíveis).
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
Não envie tokens brutos, chaves API ou dumps completos de variáveis de ambiente em tickets. Remova ou oculte os segredos antes de anexar.
{% endhint %}

***

## 🤝 Fórum da Comunidade: dev-help

Perguntas e respostas entre usuários. A equipe pode ocasionalmente responder, mas respostas não são garantidas.

### ✅ Poste Efetivamente

<table><thead><tr><th width="300">Elemento</th><th>Por Que Importa</th></tr></thead><tbody><tr><td>Objetivo claro</td><td>Ajuda outros a entenderem o resultado desejado</td></tr><tr><td>Passos para reproduzir</td><td>Permite validação e reprodução</td></tr><tr><td>Trecho do erro</td><td>Foca atenção (cole porção mínima)</td></tr><tr><td>Básicos do ambiente</td><td>Linguagem, versão do runtime, nível do plano (se relevante)</td></tr><tr><td>O que você tentou</td><td>Evita sugestões duplicadas</td></tr></tbody></table>

### 🚫 Evite

<table><thead><tr><th width="300">Armadilha</th><th>Abordagem Melhor</th></tr></thead><tbody><tr><td>Vago: "Não funciona"</td><td>Descreva resultado esperado vs atual</td></tr><tr><td>Logs enormes não formatados</td><td>Forneça linhas relevantes</td></tr><tr><td>Comparações de plataforma off-topic</td><td>Mantenha escopo para resolver seu problema</td></tr><tr><td>Tags multilinguagem irrelevantes</td><td>Marque apenas as tecnologias realmente usadas</td></tr></tbody></table>

{% hint style="success" %}
Pesquise threads existentes primeiro, sua resposta pode já existir.
{% endhint %}

***

## 🔐 Proteja Dados Sensíveis

Nunca compartilhe publicamente:

| Tipo de Dado        | Exemplo                                          |
| ------------------- | ------------------------------------------------ |
| Tokens / Chaves API | Token de bot, chaves de serviço                  |
| Senhas              | Credenciais de banco de dados / painel           |
| URLs Privadas       | Endpoints de callback internos contendo segredos |
| Info Pessoal        | Email, identificadores de cobrança               |

Use placeholders: `SEU_TOKEN_AQUI`, `exemplo-db-host`.

{% hint style="danger" %}
Se você acidentalmente vazou uma credencial, revogue / rotacione imediatamente e notifique a equipe se o risco se estender além da sua conta.
{% endhint %}

***

## 📚 Aprenda e Desenvolva Habilidades

Parceiros / conteúdo de aprendizado recomendados gratuitos:

{% tabs %}
{% tab title="JavaScript" %}
{% embed url="https://www.youtube.com/watch?list=PL9tY_tDo_Q0C0hs1aGgtJbEH1EBlyzZdG&v=lQAJ-T1QTYc" %}
{% endtab %}

{% tab title="TypeScript" %}
{% embed url="https://www.youtube.com/watch?list=PL9tY_tDo_Q0DOAzTaPnWYsryfNLsz1K6U&v=4pIo-p6pX34" %}
{% endtab %}
{% endtabs %}

***

## 🚀 Antes de Perguntar, Verifique

| Item                                                                                                 | Por Que                                       |
| ---------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| Consultou a documentação?                                                                            | Recurso pode já estar documentado             |
| Changelog / anúncios recentes                                                                        | Comportamento poderia ser mudança intencional |
| Páginas de [FAQ](general-questions/) / [solução de problemas](troubleshooting-solutions/) existentes | Respostas comuns cobertas                     |
| [Limites do plano](https://discloud.com/plans)                                                       | Alguns erros são relacionados a quota         |
