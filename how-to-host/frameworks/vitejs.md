---
description: Guia prático para hospedar aplicações Vite na Discloud.
icon: bolt
---

# Vite

## 🧭 Introdução

Este guia passo a passo mostra como preparar, configurar e fazer o deploy de uma aplicação **Vite** na Discloud.

O processo envolve compilar seu projeto para a pasta `dist` e servir os arquivos estáticos usando o `vite preview` na porta `8080`. O Vite é conhecido por sua velocidade de build e suporte nativo a múltiplos frameworks e sintaxes, incluindo **React (JSX/TSX)**, **Vue**, **Svelte**, **Solid** e **Preact**.

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
* Um **projeto Vite** criado (ex.: `npm create vite@latest meu-app`).
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
.git
.vscode/
package-lock.json
```

{% hint style="info" %}
O arquivo `.discloudignore` funciona de forma semelhante a um `.gitignore`, mas é usado pela Discloud para ignorar arquivos no momento do upload.
{% endhint %}

***

## 📦 `package.json` – scripts recomendados

Dentro do seu [`package.json`](../../development-environment/supported-languages/javascript/package.json.md), garanta que os scripts de build e preview estejam corretamente definidos:

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview --port 8080 --host"
  }
}
```

{% hint style="info" %}
* `build` – compila o projeto para a pasta `dist`.
* `preview` – serve os arquivos compilados na porta `8080`. Na Discloud, o site já fica disponível automaticamente pelo subdomínio.
* `--host` – expõe o servidor no IP da máquina, permitindo acessar o preview de outros dispositivos na mesma rede durante testes locais. Pode omitir se não precisar disso.
* `dev` – executa em modo de desenvolvimento local na porta `5173` por padrão (não necessário para a Discloud).
{% endhint %}

***

## ⚙️ `vite.config.ts` – configuração obrigatória

Para que o Vite funcione corretamente na Discloud, você precisa configurar os `allowedHosts` no arquivo de configuração. Isso garante que o servidor de preview aceite requisições vindas do seu subdomínio ou domínio personalizado.

```ts
import { defineConfig } from "vite";

export default defineConfig({
  build: {
    outDir: "dist",
  },
  preview: {
    allowedHosts: [
      "meusubdominio.discloud.app", // seu subdomínio na Discloud
      // "meudominio.com.br",       // domínio personalizado (se aplicável)
    ],
  },
});
```

{% hint style="warning" %}
Substitua `meusubdominio.discloud.app` pelo subdomínio real registrado no painel da Discloud. Se você tiver um domínio personalizado, adicione-o ao array também, por exemplo `"meudominio.com.br"`.
{% endhint %}

{% hint style="danger" %}
Se os `allowedHosts` não estiverem configurados corretamente, o Vite rejeitará as requisições e sua aplicação não abrirá.
{% endhint %}

***

## 📄 Arquivo principal (MAIN)

A Discloud exige que o campo `MAIN` aponte para um arquivo `.ts` para identificar e buildar o projeto corretamente. Isso se aplica a **qualquer framework** — React (`.tsx`), Vue (`.vue`), Svelte (`.svelte`), ou qualquer outro.

Mesmo que o seu projeto seja em JSX, TSX, Svelte ou outra sintaxe, **você ainda precisa de um arquivo `.ts`** no `MAIN`. O `vite.config.ts` é a escolha mais natural e recomendada, já que todo projeto Vite costuma ter esse arquivo.

Caso o seu projeto não tenha nenhum arquivo `.ts`, crie um na raiz – pode ser um arquivo simples como `entry.ts`, que servirá apenas para satisfazer esse requisito.

{% hint style="danger" %}
O campo `MAIN` deve sempre apontar para um arquivo `.ts`. Apontar para um `.tsx`, `.vue`, `.svelte` ou `.jsx` não é suportado.
{% endhint %}

***

## ⚙️ `discloud.config` – exemplo

Aqui está uma configuração típica para uma aplicação Vite:

```
MAIN=vite.config.ts
TYPE=site
BUILD=npm run build
START=npm run preview
RAM=512
VERSION=latest
ID=meusubdominio.discloud.app
```

Para informações detalhadas sobre cada parâmetro de configuração e todas as opções disponíveis, consulte o guia completo:

{% content-ref url="../../configurations/discloud.config/" %}
[discloud.config](../../configurations/discloud.config/)
{% endcontent-ref %}

{% hint style="warning" %}
O campo `ID` deve ser o seu subdomínio completo, por exemplo `meusubdominio.discloud.app`.
{% endhint %}

***

## 🧪 Testando localmente (build para produção)

Antes de enviar para a Discloud, verifique se seu app compila e executa corretamente:

{% stepper %}
{% step %}
Compile o projeto localmente:

```bash
npm run build
```

Isto gera a pasta `dist` com os arquivos estáticos prontos para produção.
{% endstep %}

{% step %}
Teste o build para produção:

```bash
npm run preview
```

Verifique se o servidor inicia e responde às requisições (ex.: via `curl http://localhost:8080` ou acessando no navegador).
{% endstep %}

{% step %}
Pare o servidor e proceda com o deploy.
{% endstep %}
{% endstepper %}

***

## 🔐 Variáveis de ambiente

Se o seu projeto precisar de variáveis de ambiente, você pode incluir um arquivo `.env` diretamente no `.zip` enviado para a plataforma.

{% hint style="warning" %}
Não adicione o `.env` ao `.discloudignore` se precisar que ele seja enviado junto com o projeto.
{% endhint %}

No Vite, variáveis de ambiente públicas devem começar com `VITE_` para ficarem acessíveis no bundle do cliente:

```env
VITE_API_URL=https://meu-backend.discloud.app
```

Usando em componentes:

```ts
const apiUrl = import.meta.env.VITE_API_URL;
```

{% hint style="danger" %}
Nunca exponha segredos sensíveis no frontend. Apenas variáveis com prefixo `VITE_` ficam acessíveis no bundle do cliente — as demais ficam disponíveis apenas durante o build.
{% endhint %}

***

## 🗂️ Estrutura final recomendada do projeto

Uma estrutura típica de projeto Vite para a Discloud pode ser:

```
meu-vite-app/
├─ discloud.config
├─ .discloudignore
├─ .env                 # opcional, se precisar de variáveis
├─ package.json
├─ vite.config.ts
├─ tsconfig.json
├─ index.html
├─ public/
└─ src/
   ├─ main.ts
   ├─ App.vue           # ou App.tsx, App.svelte, etc.
   └─ ...
```

***

## 🚀 Fazendo o deploy na Discloud

Você pode fazer deploy do seu app Vite usando qualquer um dos métodos suportados.

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

|                                         |                                                                                                                                                                                                                  |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Aplicação não abre / porta errada**   | Verifique se o script `preview` usa `--port 8080` e se `allowedHosts` está configurado no `vite.config.ts`.                                                                                                      |
| **Erro de host não autorizado**         | Confirme que o seu subdomínio (ex.: `meusubdominio.discloud.app`) está listado em `preview.allowedHosts` no `vite.config.ts`.                                                                                    |
| **Pasta `dist` não encontrada**         | Verifique se `build.outDir` está definido como `"dist"` no `vite.config.ts` e execute `npm run build` localmente para confirmar.                                                                                 |
| **Erro de plano / permissão**           | Confirme se sua conta possui o **plano correto** para websites/APIs.                                                                                                                                             |
| **Subdomínio não configurado**          | Certifique-se de ter seguido o guia de **subdomínio** antes do deploy.                                                                                                                                           |
| **Nenhum arquivo `.ts` no projeto**     | Crie um arquivo `.ts` na raiz (ex.: `entry.ts`) e aponte para ele no campo `MAIN` do `discloud.config`.                                                                                                          |
| **Erros de build**                      | <ul><li>Execute localmente: `npm run build` e corrija qualquer erro antes de enviar.</li><li>Confira se todas as **dependências** estão listadas no `package.json`.</li></ul>                                    |
| **Erros ao iniciar (`START`)**          | <ul><li>Verifique se o script `preview` está correto no `package.json`.</li><li>Acompanhe os **logs da Discloud** para ver a mensagem de erro exata.</li></ul>                                                   |
