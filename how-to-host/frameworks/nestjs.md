---
description: Guia prático para hospedar aplicações NestJS na Discloud.
icon: feather
---

# NestJS

## 🧭 Introdução

Este guia passo a passo mostra como preparar, configurar e fazer o deploy de uma aplicação **NestJS** na Discloud.

O processo envolve compilar seu código TypeScript para a pasta `dist` e executar o JavaScript compilado na porta `8080`. Aplicações NestJS são simples de fazer deploy porque o framework gerencia rotas, injeção de dependências e organização de módulos automaticamente.

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
* Um **projeto NestJS** criado (ex.: `nest new meu-app`).
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
.env
.env.local
.git
.vscode/
package-lock.json
```

{% hint style="info" %}
O arquivo `.discloudignore` funciona de forma semelhante a um `.gitignore`, mas é usado pela Discloud para ignorar arquivos no momento do upload.
{% endhint %}

***

## 🔧 Configuração TypeScript – `tsconfig.build.json`

Garanta que seu `tsconfig.build.json` (ou `tsconfig.json`) esteja configurado para compilar para a pasta `dist`. Aqui está uma configuração típica:

```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist",
    "rootDir": "./src",
    "composite": false,
    "incremental": false
  },
  "exclude": ["node_modules", "dist"]
}
```

{% hint style="danger" %}
É importante que **`compilerOptions.outDir`** esteja definido como `"dist"`, pois a Discloud procurará pela sua aplicação compilada lá.
{% endhint %}

***

## 🚀 Ponto de entrada principal – `src/main.ts`

Garanta que seu `src/main.ts` escute na **porta 8080** e aceite a porta de variáveis de ambiente. Aqui está uma configuração típica:

```ts
import { NestFactory } from "@nestjs/core";
import { AppModule } from "./app.module";

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  const port = process.env.PORT ? Number(process.env.PORT) : 8080;

  await app.listen(port, "0.0.0.0");
  console.log(`Servidor rodando em http://0.0.0.0:${port}`);
}

bootstrap();
```

{% hint style="danger" %}
#### **Importante**

* **Porta 8080 é obrigatória.** Mesmo que você defina `PORT` no seu arquivo `.env`, ele deve ser `8080`.
* Vincule a `0.0.0.0` (não `localhost`) para que o tráfego externo possa chegar ao seu app.
{% endhint %}

***

## 📦 `package.json` – scripts recomendados

Dentro do seu [`package.json`](../../development-environment/supported-languages/javascript/package.json.md), garanta que os scripts de build e start estejam corretamente definidos:

```json
{
  "scripts": {
    "start": "node dist/main",
    "start:dev": "nest start --watch",
    "build": "nest build"
  }
}
```

{% hint style="info" %}
* `build` – compila TypeScript para `dist` via o CLI do Nest.
* `start` – executa a aplicação compilada a partir da pasta `dist`.
* `start:dev` – executa em modo watch localmente (não necessário para Discloud).
{% endhint %}

***

## ⚙️ `discloud.config` – exemplo

Aqui está uma configuração típica para uma aplicação NestJS:

```
MAIN=src/main.ts
TYPE=site
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
ID=meu-nestjs-app
```

Para informações detalhadas sobre cada parâmetro de configuração e todas as opções disponíveis, consulte o guia completo:

{% content-ref url="../../configurations/discloud.config/" %}
[discloud.config](../../configurations/discloud.config/)
{% endcontent-ref %}

{% hint style="warning" %}
Certifique-se de ajustar o campo `ID` para corresponder ao seu subdomínio registrado no painel da Discloud.
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

Isto gera a pasta `dist` com o JavaScript compilado.
{% endstep %}

{% step %}
Teste o build para produção:

```bash
npm run start
```

Verifique se o servidor inicia e responde às requisições (ex.: via `curl http://localhost:8080`).
{% endstep %}

{% step %}
Pare o servidor e proceda com o deploy.
{% endstep %}
{% endstepper %}

***

## 🔐 Variáveis de ambiente

No NestJS, variáveis de ambiente são tipicamente acessadas via `process.env`:

* Padrões comuns incluem `DATABASE_URL`, `API_KEY`, `REDIS_URL`, etc.

Exemplo em um serviço:

```ts
import { Injectable } from "@nestjs/common";

@Injectable()
export class ConfigService {
  getDatabaseUrl() {
    return process.env.DATABASE_URL || "sqlite:memory";
  }
}
```

{% hint style="info" %}
Para melhor segurança de tipo e validação, considere usar o pacote `@nestjs/config` para gerenciar variáveis de ambiente.
{% endhint %}

***

## 🗂️ Estrutura final recomendada do projeto

Uma estrutura típica de projeto NestJS para a Discloud pode ser:

```
meu-nest-app/
├─ discloud.config
├─ .discloudignore
├─ package.json
├─ tsconfig.json
├─ tsconfig.build.json
├─ src/
│  ├─ main.ts
│  ├─ app.module.ts
│  ├─ app.controller.ts
│  └─ app.service.ts
└─ dist/  (gerado após o build)
```

***

## 🚀 Fazendo o deploy na Discloud

Você pode fazer deploy do seu app NestJS usando qualquer um dos métodos suportados.

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
| **Aplicação não abre / porta errada** | Verifique se o NestJS está escutando na porta `8080` (`process.env.PORT \|\| 8080` em `main.ts`).                                                                                                                |
| **Pasta `dist` não encontrada**       | Verifique se `tsconfig.build.json` possui `"outDir": "./dist"` e execute `npm run build` localmente para confirmar.                                                                                              |
| **Erro de plano / permissão**         | Confirme se sua conta possui o **plano correto** para websites/APIs.                                                                                                                                             |
| **Subdomínio não configurado**        | Certifique-se de ter seguido o guia de **subdomínio** antes do deploy.                                                                                                                                           |
| **Erros de build**                    | <ul><li>Execute localmente: <code>npm run build</code> e corrija qualquer erro antes de enviar.</li><li>Confira se todas as <strong>dependências</strong> estão listadas no <code>package.json</code>.</li></ul> |
| **Erros ao iniciar (`START`)**        | <ul><li>Verifique se o script <code>start</code> está correto.</li><li>Acompanhe os <strong>logs da Discloud</strong> para ver a mensagem de erro exata.</li></ul>                                               |
