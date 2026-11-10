---
description: >-
  Controle o tráfego do seu site na borda da Discloud com rules e redirects,
  antes de a requisição chegar na aplicação.
icon: shield-halved
---

# Edge

## 🛡️ O que é o Edge?

O Edge controla o tráfego do seu site **antes** da requisição chegar na aplicação. Bloqueios, manutenção, headers, reescrita de URL e redirecionamentos acontecem na borda da Discloud, no [domínio personalizado](custom-domain.md) do app.

Ele não substitui o código do site. O que o Edge resolve, o app nem chega a processar.

***

## 📍 Onde fica

[Painel da Discloud](https://discloud.com/dashboard) → aplicação (site) → **Edge**.

Há duas abas:

| Aba           | Para que serve                                                                                                                     |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **Rules**     | Condições + ações. Bloquear, responder na borda, redirecionar com regra, reescrever URL, mexer em headers ou no texto da resposta. |
| **Redirects** | Redirecionamento simples de um caminho do seu domínio para outra URL.                                                              |

***

## 📋 Requisitos

Para usar o Edge, você deve atender a estes critérios:

{% hint style="success" %}
**Site** – A aplicação precisa ser um site. Bots não têm Edge.
{% endhint %}

{% hint style="success" %}
[**Domínio personalizado**](custom-domain.md) – O site precisa de um domínio personalizado ativo. Um [subdomínio](../faq/general-questions/how-to-create-a-subdomain.md) `*.discloud.app` não serve.
{% endhint %}

{% hint style="warning" %}
**Domínio fora do formato legado** – Se o domínio estiver no formato legado, abra **Domínios** no app e migre antes.
{% endhint %}

{% hint style="success" %}
[**Plano Ruby ou superior**](https://discloud.com/plans) – Vale o plano do dono do site. Em app compartilhado por uma equipe, o plano do membro não conta.
{% endhint %}

{% hint style="info" %}
**Permissão para configurar o app** – Dono, admin ou developer. O Viewer só visualiza, se a tela abrir.
{% endhint %}

***

## 🔀 Ordem do tráfego

Cada visita passa nesta ordem:

<figure><img src="../.gitbook/assets/edge-traffic-flow.png" alt="Diagrama do tráfego passando por Rules e Redirects antes da aplicação"><figcaption></figcaption></figure>

1. **Rules.** A plataforma olha as rules **ativas**, da maior prioridade para a menor. A **primeira** que bater em todas as condições é a que vale. As de baixo não rodam nessa visita.
2. **Redirects.** Se nenhuma rule interrompeu o pedido, os redirects ativos do domínio são avaliados.
3. **Aplicação.** O que sobrou segue para o site normalmente.

{% hint style="info" %}
Uma rule de "bloquear `/admin`" na frente impede que um redirect ou o app vejam esse caminho.
{% endhint %}

***

## 📜 Rules

Uma rule tem nome, status (ativa ou pausada), uma ou mais **condições** e uma ou mais **ações**.

* **Condições são um E.** Todas precisam ser verdadeiras. "Caminho começa com `/admin`" e "país é Brasil" só dispara quando os dois batem.
* **Ações rodam na ordem** em que estão na rule.
* **Prioridade** é a ordem da lista. Subir a rule faz ela ser testada antes.

### Condições

| Condição          | Exemplo                        |
| ----------------- | ------------------------------ |
| Caminho da URL    | começa com `/admin`            |
| Método HTTP       | é `POST`                       |
| Cabeçalho         | `User-Agent` contém `bot`      |
| Query string      | a chave `debug` existe         |
| País do visitante | é `BR`, ou não é `BR` nem `PT` |

Operadores: é, não é, começa com, termina com, contém, não contém, tem qualquer valor, é desconhecido.

### Ações

| Ação                         | O que faz                                                                                 |
| ---------------------------- | ----------------------------------------------------------------------------------------- |
| Responder na borda           | Devolve um status e um corpo sem chamar o app. Ex.: `403` Forbidden, `503` de manutenção. |
| Redirecionar                 | Manda o visitante para uma URL (`301` permanente ou `302` temporário).                    |
| Reescrever URL               | Troca o caminho que o app recebe. O visitante continua vendo a URL original.              |
| Definir header de resposta   | Acrescenta um header, por exemplo `X-Frame-Options: DENY`.                                |
| Remover header de resposta   | Tira headers como `Server` e `X-Powered-By`.                                              |
| Substituir texto na resposta | Troca um trecho do HTML/texto que o app devolveu.                                         |

Em URL de redirect e em rewrite dá para reaproveitar o pedido original:

* `{http.request.uri.path}`: caminho (`/blog/post`)
* `{http.request.uri.query}`: query string, sem o `?`

Exemplo de redirect que preserva o caminho: `https://novo.exemplo.com{http.request.uri.path}`.

### Modelos prontos

Na criação dá para começar de um modelo e ajustar:

* Bloquear um path, um método, um User-Agent ou um país
* Liberar só alguns países (bloqueia o resto)
* Página de manutenção (`503`)
* Redirect condicional e rewrite de URL
* Header de segurança, remoção de headers, troca de texto
* Bloqueio quando a query `debug` existir

{% hint style="warning" %}
O modelo é só um rascunho. Salve depois de revisar nome, condições e ações.
{% endhint %}

***

## ↪️ Redirects

Use quando a regra é só "este caminho deste domínio vai para esta URL". Não precisa repetir o host de origem: o redirect vale para o domínio do app.

| Campo                  | Como preencher                                                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| URL de destino         | Endereço completo, com `https://`.                                                                                                    |
| Caminho de origem      | `*` para o domínio inteiro, ou um caminho. O `*` só pode ficar **no final** (`/docs*`). Tem de começar com `/`, exceto o `*` sozinho. |
| Tipo                   | **301** permanente (mudança definitiva, bom para SEO) ou **302** temporário (campanha, teste).                                        |
| Preservar caminho      | O pedaço da URL depois do match segue para o destino.                                                                                 |
| Preservar query string | `?utm=...` e o resto continuam no destino.                                                                                            |

### Exemplos

| Origem                         | Destino                        | Efeito                                                                       |
| ------------------------------ | ------------------------------ | ---------------------------------------------------------------------------- |
| `*` + preservar caminho        | `https://www.exemplo.com`      | `exemplo.com/preco?plano=pro` vira `https://www.exemplo.com/preco?plano=pro` |
| `/docs*` sem preservar caminho | `https://docs.exemplo.com`     | Tudo em `/docs...` cai na home da documentação                               |
| `/promo*` tipo 302             | `https://campanha.exemplo.com` | Redirect temporário de campanha                                              |

Redirects também podem ficar pausados. Pausar não apaga a regra.

***

## 🚫 O que o Edge não faz

* Não protege bot, [banco de dados](databases.md) nem [VPS](../how-to-host/vps.md).
* Não funciona em subdomínio gratuito da Discloud.
* Não edita o código do app. Rewrite muda a URL interna. Substituir texto só altera a resposta já gerada.
* Não é um firewall de IP nem um WAF genérico. O controle é o que você configurou em Rules e Redirects.
* O Viewer de uma equipe não cria nem edita.
