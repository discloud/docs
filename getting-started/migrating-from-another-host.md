---
description: >-
  Como trazer um bot, site ou API de outra hospedagem para a Discloud, com o
  equivalente de cada configuração.
icon: truck-arrow-right
---

# Migrar de Outra Hospedagem

Se a sua aplicação já roda em outra hospedagem, a migração costuma ser rápida. A maior parte do trabalho é traduzir a configuração para o [`discloud.config`](../configurations/discloud.config/).

***

## 🔁 Equivalências

| Na outra hospedagem                    | Na Discloud                                                                                                          |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `Procfile` com `worker: node index.js` | `TYPE=bot` e `MAIN=index.js` no `discloud.config`                                                                    |
| `Procfile` com `web: ...`              | `TYPE=site` e um [subdomínio](../faq/general-questions/how-to-create-a-subdomain.md), com o servidor na porta `8080` |
| Comando de build                       | Opção `BUILD` no `discloud.config`                                                                                   |
| Comando de start                       | Opção `START` no `discloud.config`                                                                                   |
| Variáveis de ambiente do painel        | [Variáveis de ambiente](../platform-features/environment-variables.md) da Discloud                                   |
| Versão do runtime                      | Opção `VERSION` no `discloud.config`                                                                                 |
| Pacotes do sistema                     | Opção [`APT`](../configurations/discloud.config/apt.md) no `discloud.config`                                         |
| Domínio próprio                        | [Domínio personalizado](../platform-features/custom-domain.md)                                                       |

***

## 🚀 Passo a passo

{% stepper %}
{% step %}
**Crie o `discloud.config`**

Na [raiz do projeto](../faq/general-questions/what-is-the-root-of-the-project.md), crie o `discloud.config` com o tipo, o arquivo principal e a RAM. Use as equivalências acima.
{% endstep %}

{% step %}
**Leve as variáveis**

Copie as variáveis de ambiente da hospedagem antiga. No painel da Discloud, a opção **Colar .env** importa várias de uma vez.
{% endstep %}

{% step %}
**Ajuste a porta (sites e APIs)**

O servidor precisa escutar na porta `8080`.
{% endstep %}

{% step %}
**Envie**

Comprima o projeto sem pastas como `node_modules` e envie pelo método que preferir. Veja os [Bots](bots.md) e os [Websites e APIs](websites-and-apis.md) para o passo a passo.
{% endstep %}

{% step %}
**Desligue a hospedagem antiga**

Com a aplicação rodando na Discloud, desligue a antiga. Um bot do Discord ligado em dois lugares com o mesmo token responde duas vezes.
{% endstep %}
{% endstepper %}
