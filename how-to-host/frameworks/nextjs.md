---
description: Guia prático para hospedar aplicações Next.js na Discloud.
icon: 'n'
---

# Next.js

## 🧭 Introdução

Este guia passo a passo mostra como preparar, configurar e fazer o deploy de uma aplicação **Next.js** na Discloud.

Existem duas abordagens principais:

* [**Opção A (recomendada)**](nextjs.md#opcao-a-deploy-sem-servidor-custom-next.js-built-in) – usar o `next build` + `next start` **sem servidor custom** (apenas o server interno do Next.js).
* [**Opção B**](nextjs.md#opcao-b-custom-server-com-express) – usar um **servidor custom** com **Express**, útil se você precisa de **rotas extras, middlewares customizados ou integrações específicas**.

Além disso, mostramos uma [**alternativa com export estático**](nextjs.md#alternativa-export-estatico-next.js-como-site-estatico), ideal para sites puramente estáticos.

{% hint style="info" %}
Este guia assume que você já tem um projeto Next.js funcionando localmente.
{% endhint %}

***

## 📋 Requisitos

{% hint style="success" %}
[Plano Platinum ou superior](https://discloud.com/plans) é necessário para hospedar websites ou APIs.
{% endhint %}

{% hint style="success" %}
[Um subdomínio deve ser criado](../../faq/general-questions/how-to-create-a-subdomain.md) antes do deploy.
{% endhint %}

{% hint style="danger" %}
Porta `8080` é obrigatória – As aplicações devem escutar nesta porta.
{% endhint %}

***

## 🧱 Pré-requisitos locais

Antes de continuar, você vai precisar:

* **Node.js** instalado na sua máquina.
* Um **projeto Next.js** criado (ex.: `npx create-next-app`).
* Uma **conta na Discloud** com **subdomínio configurado**.
* Opcionalmente: **Git**, **VSCode** e/ou **CLI da Discloud** para facilitar o fluxo.

Se ainda não tiver familiaridade com o ambiente, confira:

{% content-ref url="../../development-environment/local-environment/nodejs.md" %}
[nodejs.md](../../development-environment/local-environment/nodejs.md)
{% endcontent-ref %}

***

## 🧹 Preparando os arquivos do projeto

Antes de compactar seu projeto em `.zip`, crie um arquivo [**`.discloudignore`**](../../configurations/.discloudignore.md) na raiz do projeto para excluir arquivos e pastas desnecessárias do upload:

```
node_modules/
dist/
.next/
.env
.env.local
.git
package-lock.json
```

{% hint style="info" %}
O arquivo `.discloudignore` funciona de forma semelhante a um `.gitignore`, mas é usado pela Discloud para ignorar arquivos no momento do upload.
{% endhint %}

***

## 📦 `package.json` – scripts recomendados

Dentro do seu [`package.json`](../../development-environment/supported-languages/javascript/package.json.md), garanta que os scripts principais do Next.js estejam definidos. Um exemplo básico:

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start -p 8080",
    "export": "next export"
  }
}
```

{% hint style="danger" %}
É importante que o **comando `start` use a porta `8080`** (`next start -p 8080`), pois essa é a porta padrão exigida pela Discloud para websites.
{% endhint %}

***

<details>

<summary>✅ Opção A – Deploy sem servidor custom (Next.js "built-in")</summary>

Nesta opção, você usa somente o servidor interno do Next (`next start`), sem precisar de `server.js`.

**🔁 Fluxo básico**

1.  Rodar o build localmente (opcional, mas recomendado):

    ```bash
    npm run build
    ```
2.  Testar localmente:

    ```bash
    npm run start
    ```
3. Se tudo estiver funcionando, preparar o `.zip` e enviar para a Discloud.

**⚙️** [**`discloud.config`**](../../configurations/discloud.config) **(exemplo)**

```
TYPE=site
MAIN=index.ts
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
ID=meu-nextjs-app
```

</details>

<details>

<summary>🧩 Opção B – Custom server com Express</summary>

Se você precisa de **rotas customizadas**, **middlewares** ou integrar outras libs antes de delegar ao Next, pode usar um **servidor Express** que usa o Next internamente.

**🧾 `server.js`**

Crie um arquivo `server.js` na raiz do projeto com o seguinte conteúdo:

```js
const express = require("express");
const next = require("next");

const dev = process.env.NODE_ENV !== "production";
const app = next({ dev });
const handle = app.getRequestHandler();

const PORT = process.env.PORT || 8080;

app.prepare().then(() => {
  const server = express();

  server.get("/hello", (req, res) => {
    return res.send("Olá, Discloud!");
  });

  server.all("*", (req, res) => {
    return handle(req, res);
  });

  server.listen(PORT, () => {
    console.log(`Servidor rodando na porta ${PORT}`);
  });
});
```

**📦** [**`package.json`**](../../development-environment/supported-languages/javascript/package.json.md) **(com servidor custom)**

Atualize seus scripts para utilizar o `server.js` em produção:

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "node server.js"
  }
}
```

**⚙️** [**`discloud.config`**](../../configurations/discloud.config) **(custom server)**

```
TYPE=site
MAIN=server.js
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
ID=meu-nextjs-app-custom-server
```

{% hint style="info" %}
Use esta opção apenas se realmente precisar de um servidor custom. Para a maioria dos projetos, a **Opção A** (sem servidor custom) é mais simples e suficiente.
{% endhint %}

</details>

<details>

<summary>🧾 Alternativa – Export estático (Next.js como site estático)</summary>

Se o seu projeto não depende de **SSR** ou **API Routes**, você pode usar o `next export` para gerar um site totalmente **estático**.

**📦** [**`package.json`**](../../development-environment/supported-languages/javascript/package.json.md) **(export estático)**

```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build && next export",
    "start": "npx serve -s out -l 8080"
  }
}
```

**⚙️** [**`discloud.config`**](../../configurations/discloud.config) **(estático)**

```
TYPE=site
BUILD=npm run build
START=npm run start
RAM=256
ID=meu-site-estatico
```

{% hint style="success" %}
Sites estáticos costumam consumir **menos RAM** e são ideais para blogs, landing pages e documentações simples.
{% endhint %}

</details>

***

## 🔐 Variáveis de ambiente

No Next.js, variáveis de ambiente públicas devem começar com `NEXT_PUBLIC_`.

* Defina variáveis pelo **Painel da Discloud**, **CLI** ou **API**.
* Tudo que começa com `NEXT_PUBLIC_` é embutido no bundle durante o **build**.

Exemplo:

```env
NEXT_PUBLIC_API_URL=https://meu-backend.discloud.app
API_SECRET_TOKEN=nao-colocar-no-front
```

Usando em componentes:

```js
const apiUrl = process.env.NEXT_PUBLIC_API_URL;
```

***

## 🗂️ Estrutura final recomendada do projeto

Uma estrutura típica de projeto Next.js para a Discloud pode ser:

```
my-next-app/
├─ discloud.config
├─ .discloudignore
├─ package.json
├─ next.config.js
├─ server.js        # opcional (apenas na Opção B)
├─ public/
└─ app/ ou pages/
	 ├─ page.js
	 └─ api/
			└─ hello.js
```

***

## 🚀 Fazendo o deploy na Discloud

Você pode fazer deploy do seu app Next.js usando qualquer um dos métodos suportados.

{% content-ref url="../../how-to-host-using/dashboard.md" %}
[dashboard.md](../../how-to-host-using/dashboard.md)
{% endcontent-ref %}

{% content-ref url="../../how-to-host-using/discord-bot.md" %}
[discord-bot.md](../../how-to-host-using/discord-bot.md)
{% endcontent-ref %}

{% content-ref url="../../how-to-host-using/visual-studio-code.md" %}
[visual-studio-code.md](../../how-to-host-using/visual-studio-code.md)
{% endcontent-ref %}

{% content-ref url="../../how-to-host-using/cli.md" %}
[cli.md](../../how-to-host-using/cli.md)
{% endcontent-ref %}

***

## 🛠️ Troubleshooting (erros comuns)

|                                       |                                                                                                                                                                                                                  |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Aplicação não abre / porta errada** | Verifique se o Next está usando a porta `8080` (`next start -p 8080` ou `PORT=8080`).                                                                                                                            |
| **Erro de plano / permissão**         | Confirme se sua conta possui o **plano correto** para websites/APIs.                                                                                                                                             |
| **Subdomínio não configurado**        | Certifique-se de ter seguido o guia de **subdomínio** antes do deploy.                                                                                                                                           |
| **Erros de build**                    | <ul><li>Execute localmente: <code>npm run build</code> e corrija qualquer erro antes de enviar.</li><li>Confira se todas as <strong>dependências</strong> estão listadas no <code>package.json</code>.</li></ul> |
| **Erros ao iniciar (`START`)**        | <ul><li>Verifique se o script <code>start</code> está correto.</li><li>Acompanhe os <strong>logs da Discloud</strong> para ver a mensagem de erro exata.</li></ul>                                               |
