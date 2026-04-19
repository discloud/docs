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

### 📦 Requisito do TypeScript (importante)

Se o seu projeto usa TypeScript, certifique-se de instalá-lo em `dependencies` e não em `devDependencies`.

Alguns ambientes de deploy instalam apenas dependências de produção, o que pode causar falhas no build se o TypeScript não estiver disponível.

#### ✅ Exemplo correto

```json
{
  "dependencies": {
    "typescript": "^5.0.0"
  }
}
```

#### ❌ Exemplo incorreto

```json
{
  "devDependencies": {
    "typescript": "^5.0.0"
  }
}
```

***

## 📦 Alterando a pasta de build do Next.js (`.next` → `dist`)

Por padrão, o **Next.js** gera os arquivos de build na pasta `.next`.\
Mas em alguns cenários (deploy, padrões de projeto, integração com outras ferramentas), você pode querer usar uma pasta como `dist`.

O Next.js permite alterar a pasta de saída usando a configuração `distDir`.

#### 1. Edite o arquivo `next.config.js`

```js
const nextConfig = {
  distDir: 'dist',
}
```

#### 2. Rode o build normalmente

```bash
npm run build
```

#### 📁 Resultado

Antes:

```
.next/
```

Depois:

```
dist/
```

***



<details open>

<summary>✅ Deploy sem servidor custom (Next.js "built-in")</summary>

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
MAIN=index.ts
TYPE=site
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
ID=meu-nextjs-app
```

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
MAIN=out/index.html
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
