---
description: Como criar um Dockerfile compatível com a Discloud
icon: docker
---

# Dockerfile

## 🐳 O que é

Com um `Dockerfile`, você pode hospedar praticamente qualquer coisa na Discloud. Você define o ambiente da aplicação: runtime, dependências, comando de start e o que a imagem precisa para rodar.

Isso dá liberdade para misturar stacks, ferramentas e setups que o fluxo padrão por linguagem não cobre. Ao mesmo tempo, você continua usando o que a Discloud já oferece: painel, variáveis, volume, domínio e o restante da plataforma.

O arquivo principal do app passa a ser o `Dockerfile` (`MAIN=Dockerfile`).

{% hint style="info" %}
**Regra de ouro:** `MAIN=Dockerfile` · código na imagem (ex. `/app`) com dono **1000** · dados no volume `/home/discloud` · sites na porta pública **8080**.
{% endhint %}

***

## 📋 Requisitos

Para o app subir no fluxo de Dockerfile, você deve atender a estes critérios:

{% hint style="success" %}
Arquivo `Dockerfile` – Na raiz do projeto (ou no path que você indicar), com D maiúsculo.
{% endhint %}

{% hint style="success" %}
`MAIN=Dockerfile` – No `discloud.config`, ou selecione `Dockerfile` como arquivo principal no painel.
{% endhint %}

{% hint style="success" %}
UID 1000 – O processo e as pastas do código e do volume precisam pertencer ao usuário **1000**.
{% endhint %}

{% hint style="success" %}
`CMD` ou `ENTRYPOINT` – A imagem precisa definir como o app inicia.
{% endhint %}

{% hint style="warning" %}
Sites na porta 8080 – Se o app for hospedado como **site**, a porta pública é a **8080**. Outra porta não abre no subdomínio nem no domínio personalizado.
{% endhint %}

***

## 📄 discloud.config

No `discloud.config`, o arquivo principal precisa ser o Dockerfile:

{% code title="discloud.config" %}
```properties
NAME=Meu App
TYPE=site
MAIN=Dockerfile
RAM=512
ID=meu-app
```
{% endcode %}

| Chave  | Obrigatoriedade | Função                                        |
| ------ | --------------- | --------------------------------------------- |
| `MAIN` | Obrigatória     | Deve ser `Dockerfile` para entrar neste fluxo |
| `TYPE` | Recomendada     | `site` ou `bot` (padrão: `bot`)               |
| `ID`   | Sites           | Subdomínio do site                            |
| `RAM`  | Recomendada     | Em sites, mínimo prático 512 MB               |

{% hint style="info" %}
Sem `MAIN=Dockerfile`, a Discloud não usa o fluxo de Dockerfile. No painel, o equivalente é selecionar **Dockerfile** como arquivo principal. Detalhes gerais do arquivo estão em [discloud.config](discloud.config/).
{% endhint %}

Para bot / worker:

{% code title="discloud.config" %}
```properties
NAME=Meu Bot
TYPE=bot
MAIN=Dockerfile
RAM=100
```
{% endcode %}

***

## 👤 Usuário 1000 e permissões

A Discloud inicia o contêiner como `1000:1000`. Isso exige três coisas ao mesmo tempo:

1. O processo roda como UID **1000** (`USER 1000`)
2. A pasta onde o código é **copiado e executado** (ex.: `/app`) pertence ao **1000**
3. O volume `/home/discloud` também pertence ao **1000**, para a app conseguir gravar dados

`/app` é só um exemplo. Pode ser outro diretório, **desde que não seja** `/home/discloud` e tenha permissão **1000**.

```dockerfile
RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 . .

USER 1000
```

{% hint style="info" %}
Não basta só o `USER 1000`. A pasta do código (onde o `WORKDIR` aponta e de onde o `CMD` roda) tem que pertencer ao UID 1000. Sem isso, a app falha com erro de permissão.
{% endhint %}

{% hint style="warning" %}
Use `chown -R 1000:1000` nas pastas e `COPY --chown=1000:1000` nos arquivos. `Permission denied` é o erro mais comum quando isso falta.
{% endhint %}

{% hint style="info" %}
Em imagens que já têm UID 1000 (ex.: `node:*`), o `getent` evita erro de `UID is not unique`. O importante é a pasta do código e o volume ficarem com dono **1000**.
{% endhint %}

***

## 🌐 Porta 8080 (sites)

Se você hospedar o app como **site**, a porta que deve usar é a **8080**.

A Discloud conecta a porta **8080** ao subdomínio ou ao domínio personalizado. Essa é a **única porta exposta na rede pública**.

| Acesso                                       | Porta                         | Quando funciona                     |
| -------------------------------------------- | ----------------------------- | ----------------------------------- |
| Público (subdomínio / domínio personalizado) | **8080**                      | Sempre, para sites                  |
| Outra porta (ex.: 3000, 5000)                | Qualquer outra                | **Não** abre na internet            |
| Interno (VLAN / rede privada)                | A porta que o processo escuta | Só se a VLAN estiver ativada no app |

No código, faça o site escutar em `0.0.0.0:8080` (ou `process.env.PORT` apontando para `8080`).

```dockerfile
ENV PORT=8080
```

{% hint style="danger" %}
Se o site escutar em outra porta, o domínio público **não funciona**. Essa outra porta só seria alcançável internamente pela [rede privada (VLAN)](../platform-features/vlan.md), e apenas se o app estiver com a VLAN ativada.
{% endhint %}

Para **bots** (sem site HTTP público), a porta 8080 não é obrigatória. As demais regras continuam valendo.

***

## ▶️ CMD ou ENTRYPOINT

A Discloud sobe o processo definido na imagem. Sem `CMD` ou `ENTRYPOINT` válido, o app não inicia.

```dockerfile
CMD ["node", "server.js"]
```

O comando deve apontar para o código na pasta da imagem (ex.: `/app`), não para o volume.

***

## 📦 Volume (`/home/discloud`)

Separe mentalmente estes dois lugares:

| Lugar                         | Para quê                               | Persiste?                               |
| ----------------------------- | -------------------------------------- | --------------------------------------- |
| **Imagem** (ex.: `/app`)      | Código e dependências que **executam** | Recriado no rebuild da imagem           |
| **Volume** (`/home/discloud`) | Dados que a app **salva** em runtime   | **Sim**: sobrevive a reinício e rebuild |
| **Qualquer outro path**       | Temporário                             | **Não**: some no rebuild                |

O volume **não** é o lugar do código que vai rodar. É o lugar onde a aplicação, **já ligada**, grava o que precisa continuar existindo (uploads, arquivos gerados, bancos embutidos, etc.).

| Momento                                     | O que acontece em `/home/discloud`               |
| ------------------------------------------- | ------------------------------------------------ |
| **No build** (`COPY` / `RUN` no Dockerfile) | O que você colocar aí **não fica**.              |
| **Com o app ligado**                        | O que a app **criar ou salvar** aí **persiste**. |

{% hint style="danger" %}
`COPY index.js /home/discloud/` no Dockerfile **não** faz o `index.js` existir na inicialização. Código na imagem (ex.: `/app`); volume só para dados.
{% endhint %}

Exemplo de separação:

```dockerfile
RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 . .

USER 1000
CMD ["node", "index.js"]
```

No código da aplicação, grave o que precisa persistir em `/home/discloud`, por exemplo `/home/discloud/uploads`.

***

## 🔐 Variáveis de ambiente

Defina tokens, URLs e secrets no **painel da Discloud**. A app lê essas variáveis em runtime.

{% hint style="info" %}
Em apps com **Dockerfile próprio**, use as variáveis do painel para o runtime. O prefixo `BUILD_` do painel **não** é injetado no build do seu Dockerfile. O que a imagem precisa em build-time deve estar no próprio Dockerfile.
{% endhint %}

Veja também [Variáveis de Ambiente](../platform-features/environment-variables.md).

***

## 🧪 Exemplos

{% tabs %}
{% tab title="Node.js (site)" %}
```dockerfile
FROM node:20-slim

RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 package*.json ./
RUN npm ci --omit=dev
COPY --chown=1000:1000 . .

USER 1000
ENV PORT=8080

CMD ["node", "server.js"]
```
{% endtab %}

{% tab title="Python / FastAPI (site)" %}
```dockerfile
FROM python:3.12-slim

RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY --chown=1000:1000 . .

USER 1000
ENV PORT=8080

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
```
{% endtab %}

{% tab title="Bot / worker" %}
```dockerfile
FROM python:3.12-slim

RUN (getent passwd 1000 >/dev/null || useradd -u 1000 -m appuser) \
  && mkdir -p /app /home/discloud \
  && chown -R 1000:1000 /app /home/discloud

WORKDIR /app
COPY --chown=1000:1000 requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY --chown=1000:1000 . .

USER 1000

CMD ["python", "bot.py"]
```
{% endtab %}
{% endtabs %}

***

## 🛠️ Problemas comuns

| Problema                           | Causa comum                                | Solução                                                          |
| ---------------------------------- | ------------------------------------------ | ---------------------------------------------------------------- |
| App não entrou no fluxo Dockerfile | `MAIN` errado ou ausente                   | `MAIN=Dockerfile` no `discloud.config` (ou selecionar no painel) |
| Site não abre                      | Não escuta na porta pública 8080           | Escutar em `0.0.0.0:8080`; outra porta não vai para o domínio    |
| Permission denied                  | Pasta do código ou volume sem dono 1000    | `chown` + `COPY --chown=1000:1000` + `USER 1000`                 |
| App cai ao iniciar                 | `CMD`/`ENTRYPOINT` inválido ou path errado | Comando apontando para o código na imagem                        |
| Arquivo do `COPY` “sumiu”          | Foi para `/home/discloud` no build         | Código na imagem; volume só para dados em runtime                |
| Perdi dados no rebuild             | Salvou fora do volume                      | Gravar em `/home/discloud` com o app ligado                      |

***

## 🚫 O que não fazer

* Não use `MAIN=index.js` (ou outro arquivo) se a intenção é o fluxo de Dockerfile.
* Não coloque o código executável em `/home/discloud` no Dockerfile.
* Não espere que um `COPY` para o volume no build apareça na inicialização.
* Não use outra porta que não a **8080** para o site público. Só a 8080 vai para o subdomínio/domínio; outras portas ficam só internas (VLAN, se ativada).
* Não rode como root: o runtime força UID **1000**.
* Aplicações com Dockerfile **não migram automaticamente** entre clusters. Para mudar de cluster/Projeto, remova e hospede de novo.

***

## ✅ Resumo

1. Arquivo `Dockerfile` + **`MAIN=Dockerfile`**
2. `CMD` ou `ENTRYPOINT` apontando para o código na imagem
3. UID **1000** + permissão 1000 na pasta do código **e** no volume
4. Sites na porta pública **8080** (única exposta ao domínio)
5. Código na imagem (ex. `/app`), **nunca** no volume
6. Volume `/home/discloud` = onde a app **salva** o que deve viver; o que for no build para essa pasta **não fica**
