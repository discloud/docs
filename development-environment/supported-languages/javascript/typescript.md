---
description: Guia completo para hospedar aplicações TypeScript na Discloud.
---

# TypeScript

## 📁 Preparando os Arquivos

Antes de fazer o upload do seu projeto, você deve excluir arquivos desnecessários para otimizar o deploy.

#### ❌ Arquivos a Excluir

Certifique-se de que os seguintes arquivos e diretórios não estejam incluídos no seu [`.zip`](../../../faq/general-questions/how-to-compress.md):

```diff
- package-lock.json
- node_modules/
- .cache/
- .git/
```

📌 Use um arquivo [`.discloudignore`](../../../configurations/.discloudignore.md) para excluir esses arquivos automaticamente.

🔗 Precisa de ajuda para configurar o seu [`package.json`](package.json.md) ou encontrar o [arquivo principal](../../../faq/general-questions/what-is-the-main-file.md)?

<details>

<summary>📦 Sobre a pasta dist (TypeScript: bot e site)</summary>

{% hint style="info" %}
Em aplicações TypeScript, a pasta `dist/` é reservada para a saída do BUILD da Discloud, tanto em `TYPE=bot` quanto em `TYPE=site`. Se você definir `BUILD=...` no seu [`discloud.config`](../../../configurations/discloud.config/), a Discloud gera a pasta `dist/` para você. Não comprima a `dist/` nem envie arquivos para dentro dela.
{% endhint %}

**⚙️ Build automático (recomendado)**

1. Adicione `BUILD` no `discloud.config` (ex.: `BUILD=npm run build`).
2. Configure o `tsconfig.json` para gerar a saída em `dist/` e adicione os scripts ao `package.json`.
3. Executamos o `BUILD` antes do `START` e sua aplicação roda a partir da `dist/`.

Exemplo de `discloud.config` (bot):

```properties
TYPE=bot
MAIN=dist/index.js
BUILD=npm run build
START=npm run start
RAM=100
VERSION=latest
ID=meu-bot-ts
```

Exemplo de `discloud.config` (site):

```properties
TYPE=site
ID=meusite
MAIN=dist/server.js
BUILD=npm run build
START=npm run start
RAM=512
VERSION=latest
```

**👜 Build feito localmente**

1. Gere a saída em `build/` (não use `dist/`).
2. Não inclua `BUILD` no `discloud.config`.
3. Aponte o `MAIN` para o arquivo de entrada dentro da pasta `build/`.

Exemplo (bot):

```properties
TYPE=bot
MAIN=build/index.js
RAM=100
VERSION=latest
ID=meu-bot-ts
```

Exemplo (site):

```properties
TYPE=site
ID=meusite
MAIN=build/server.js
RAM=512
VERSION=latest
```

</details>

***

## ⚙️ Configuração do Projeto TypeScript

Normalmente você compila TypeScript para JavaScript com o `tsc` e executa os arquivos compilados.

### package.json (scripts)

```json
{
  "name": "my-ts-app",
  "version": "1.0.0",
  "main": "dist/index.js",
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js"
  },
  "dependencies": {},
  "devDependencies": {
    "typescript": "^5.6.0"
  }
}
```

### tsconfig.json (mínimo)

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "CommonJS",
    "outDir": "dist",
    "rootDir": "src",
    "esModuleInterop": true,
    "strict": true
  },
  "include": ["src"]
}
```

{% hint style="info" %}
A Discloud instala as dependências definidas no seu projeto. Garanta que o `typescript` esteja presente (como devDependency já serve) para que a etapa de `BUILD` consiga executar o `tsc`.
{% endhint %}

***

## 🌐 Hospedando Sites e APIs com Express (TypeScript)

Antes de fazer o deploy do seu site ou API na Discloud, garanta que você atende aos seguintes requisitos:

{% hint style="success" %}
É necessário o [plano Platinum ou superior](https://discloud.com/plans) para hospedar sites ou APIs.
{% endhint %}

{% hint style="success" %}
[É preciso criar um subdomínio](../../../faq/general-questions/how-to-create-a-subdomain.md) antes do deploy.
{% endhint %}

{% hint style="danger" %}
A porta `8080` é obrigatória – as aplicações devem escutar nessa porta.
{% endhint %}

### Exemplo com Express (TS)

```ts
import express from "express";

const app = express();

app.get("/", (_req, res) => {
  res.send("Olá, Discloud com TypeScript!");
});

const PORT = Number(process.env.PORT) || 8080;
app.listen(PORT, () => console.log(`Servidor rodando na porta ${PORT}`));
```

***

## ✍️ Fazendo Deploy da Sua Aplicação

Uma vez que seu projeto esteja configurado e comprimido, você pode escolher um dos seguintes métodos de deploy na Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Faça upload e gerencie sua aplicação via interface web.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot/">discord-bot</a></td><td align="center">Faça deploy diretamente através dos comandos do bot Discord da Discloud.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integre com VS Code para gerenciamento contínuo de projetos.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use a interface de linha de comando para deploy rápido e eficiente.</td><td></td><td></td><td></td></tr></tbody></table>

***

## 🔎 Resumo rápido das particularidades do TypeScript na Discloud

* A `dist/` é reservada para os builds da Discloud tanto em `TYPE=bot` quanto em `TYPE=site`.
* Se você fizer o build localmente, gere a saída em `build/` e aponte o `MAIN` para `build/...`.
* Em TypeScript, sempre defina `BUILD` e `START` no `discloud.config` quando enviar os arquivos-fonte; o `MAIN` deve apontar para o arquivo JS de entrada em execução (normalmente `dist/index.js`).
* Em sites/APIs, seu servidor deve escutar na porta `8080`.
