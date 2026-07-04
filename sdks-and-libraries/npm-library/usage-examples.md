---
description: >-
  Exemplos e casos de uso para a biblioteca NPM discloud.app, cobrindo
  gerenciamento de aplicações, monitoramento, operações de equipe e muito mais.
icon: vial
---

# Exemplos de Uso

{% hint style="info" %}
**Importante**: Para obter seu Token da API necessário nos exemplos abaixo, veja [aqui](../../faq/general-questions/how-can-i-get-my-discloud-api-token.md).

**Configuração Necessária**: Certifique-se de ter completado o guia [**Introdução**](getting-started.md) antes de usar estes exemplos.
{% endhint %}

***

## 👤 Gerenciamento de Usuário

### 📄 Obtendo Informações do Usuário

```javascript
const { discloud } = require("discloud.app");

try {
  const user = await discloud.user.fetch();

  console.log("Informações do usuário:", user);
} catch (error) {
  console.error("Falha ao buscar usuário:", error.message);
}
```

## 📱 Gerenciamento de Aplicações

### 🚀 Fazendo Upload de uma Nova Aplicação

{% tabs %}
{% tab title="Do Caminho do Arquivo" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.create({
    file: "./my-bot.zip", // Caminho para seu arquivo ZIP
  });

  console.log("Upload bem-sucedido!");
} catch (error) {
  console.error("Upload falhou:", error.message);
}
```
{% endtab %}

{% tab title="Do Buffer/Blob" %}
```javascript
const fs = require("fs");
const { discloud } = require("discloud.app");

try {
  const fileData = fs.readFileSync("./my-bot.zip");

  await discloud.apps.create({
    file: {
      data: fileData, // Buffer ou Blob
      name: "my-bot.zip", // Nome do arquivo original
    },
  });

  console.log("Upload bem-sucedido!");
} catch (error) {
  console.error("Upload falhou:", error.message);
}
```
{% endtab %}

{% tab title="Do Stream" %}
```javascript
const fs = require("fs");
const { discloud, streamToFile } = require("discloud.app");

try {
  const stream = fs.createReadStream("./my-bot.zip");
  const file = await streamToFile(stream, "my-bot.zip");

  await discloud.apps.create({ file });
  console.log("Upload bem-sucedido!");
} catch (error) {
  console.error("Upload falhou:", error.message);
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Antes do upload:** Certifique-se de que seu arquivo ZIP contenha o arquivo [`discloud.config`](https://github.com/discloud/docs/blob/portuguese/configuracoes/discloud.config) e siga as [**diretrizes de preparação**](../../development-environment/supported-languages/javascript/) para sua linguagem.
{% endhint %}

### 🔄 Atualizando (Fazendo Commit) uma Aplicação

{% tabs %}
{% tab title="Caminho do arquivo / URL" %}
```javascript
const { discloud } = require("discloud.app");

await discloud.apps.update("APP_ID", {
  file: "FILE_PATH/FILE_NAME.zip",
});
```
{% endtab %}

{% tab title="Blob | Buffer | File | RawFile | ReadableStream" %}
```javascript
const { discloud } = require("discloud.app");
const fs = require("fs");

await discloud.apps.update("APP_ID", {
  file: {
    data: fs.readFileSync("FILE_PATH/FILE_NAME.zip"),
    name: "FILE_NAME.zip",
  },
});
```
{% endtab %}
{% endtabs %}

### 📱 Buscando Informações da Aplicação

{% tabs %}
{% tab title="Aplicação Única" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const app = await discloud.apps.fetch("your_app_id");
  console.log("Informações da aplicação:", app);
} catch (error) {
  console.error("Falha ao buscar aplicação:", error.message);
}
```
{% endtab %}

{% tab title="Todas as Aplicações" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const apps = await discloud.apps.fetch("all");
  console.log("Aplicações:", apps);
} catch (error) {
  console.error("Falha ao buscar aplicações:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 🗑️ Excluindo Aplicações

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.delete("your_app_id");
  console.log("Aplicação excluída com sucesso!");
} catch (error) {
  console.error("Falha ao excluir aplicação:", error.message);
}
```

{% hint style="danger" %}
**Aviso:** Excluir uma aplicação é **permanente** e não pode ser desfeito. Certifique-se de fazer backup de seus dados antes da exclusão.
{% endhint %}

***

## ⚡ Controle de Aplicações

### 🟢 Iniciando Aplicações

{% tabs %}
{% tab title="Aplicação Única" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.start("your_app_id");
  console.log("Aplicação iniciada com sucesso!");
} catch (error) {
  console.error("Falha ao iniciar aplicação:", error.message);
}
```
{% endtab %}

{% tab title="Todas as Aplicações" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.start("all");
  console.log("Todas as aplicações iniciadas!");
} catch (error) {
  console.error("Falha ao iniciar aplicações:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 🔴 Parando Aplicações

{% tabs %}
{% tab title="Aplicação Única" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.stop("your_app_id");
  console.log("Aplicação parada com sucesso!");
} catch (error) {
  console.error("Falha ao parar aplicação:", error.message);
}
```
{% endtab %}

{% tab title="Todas as Aplicações" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.stop("all");
  console.log("Todas as aplicações paradas!");
} catch (error) {
  console.error("Falha ao parar aplicações:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 🔄 Reiniciando Aplicações

{% tabs %}
{% tab title="Aplicação Única" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.restart("your_app_id");
  console.log("Aplicação reiniciada com sucesso!");
} catch (error) {
  console.error("Falha ao reiniciar aplicação:", error.message);
}
```
{% endtab %}

{% tab title="Todas as Aplicações" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.restart("all");
  console.log("Todas as aplicações reiniciadas com sucesso!");
} catch (error) {
  console.error("Falha ao reiniciar aplicações:", error.message);
}
```
{% endtab %}
{% endtabs %}

***

## 📊 Monitoramento e Diagnósticos

### 📈 Verificando Status da Aplicação

{% tabs %}
{% tab title="Status de Aplicação Única" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const status = await discloud.apps.status("your_app_id");
  console.log("Status obtido com sucesso!");
} catch (error) {
  console.error("Falha ao obter status:", error.message);
}
```
{% endtab %}

{% tab title="Status de Todas as Aplicações" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const statusMap = await discloud.apps.status("all");
  console.log("Todos os status obtidos com sucesso!");
} catch (error) {
  console.error("Falha ao obter status:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 📋 Visualizando Logs da Aplicação

{% tabs %}
{% tab title="Logs de Aplicação Única" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const logs = await discloud.apps.terminal("your_app_id");
  console.log("Logs obtidos com sucesso!");
} catch (error) {
  console.error("Falha ao obter logs:", error.message);
}
```
{% endtab %}

{% tab title="Logs de Todas as Aplicações" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const logsMap = await discloud.apps.terminal("all");
  console.log("Todos os logs obtidos com sucesso!");
} catch (error) {
  console.error("Falha ao obter logs:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 💻 Enviando Comandos do Terminal

```javascript
const { discloud } = require("discloud.app");

try {
  const result = await discloud.apps.console("your_app_id", "ls -la");
  console.log("Resultado do comando:", result);
} catch (error) {
  console.error("Comando falhou:", error.message);
}
```

### 💾 Operações de Backup

#### 📦 Criando Backups

{% tabs %}
{% tab title="Backup de Aplicação Única" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const backup = await discloud.apps.backup("your_app_id");
  console.log("Backup criado com sucesso!");
} catch (error) {
  console.error("Backup falhou:", error.message);
}
```
{% endtab %}

{% tab title="Backup de Todas as Aplicações" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const backups = await discloud.apps.backup("all");
  console.log("Todos os backups criados com sucesso!");
} catch (error) {
  console.error("Backup falhou:", error.message);
}
```
{% endtab %}
{% endtabs %}

***

## 👥 Gerenciamento de Equipe

### 👨‍💼 Gerenciando Moderadores da Aplicação

{% tabs %}
{% tab title="Buscar Membros da Equipe" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const team = await discloud.appTeam.fetch("your_app_id");
  console.log("Membros da equipe obtidos com sucesso!");
} catch (error) {
  console.error("Falha ao buscar equipe:", error.message);
}
```
{% endtab %}

{% tab title="Adicionar Membro da Equipe" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appTeam.create("your_app_id", "user_id", [
    "backup_app", // Pode criar backups
    "commit_app", // Pode atualizar a aplicação
    "edit_ram", // Pode modificar alocação de RAM
    "logs_app", // Pode visualizar logs da aplicação
    "restart_app", // Pode reiniciar a aplicação
    "start_app", // Pode iniciar a aplicação
    "status_app", // Pode visualizar status da aplicação
    "stop_app", // Pode parar a aplicação
  ]);

  console.log("Moderador adicionado com sucesso!");
} catch (error) {
  console.error("Falha ao adicionar moderador:", error.message);
}
```
{% endtab %}

{% tab title="Editar Permissões" %}
```javascript
const { discloud, ModPermissions } = require("discloud.app");

try {
  await discloud.appTeam.edit("your_app_id", "user_id", [
    ModPermissions.backup_app, // Pode criar backups
    ModPermissions.commit_app, // Pode atualizar a aplicação
    ModPermissions.edit_ram, // Pode modificar alocação de RAM
    ModPermissions.logs_app, // Pode visualizar logs da aplicação
    ModPermissions.restart_app, // Pode reiniciar a aplicação
    ModPermissions.start_app, // Pode iniciar a aplicação
    ModPermissions.status_app, // Pode visualizar status da aplicação
    ModPermissions.stop_app, // Pode parar a aplicação
  ]);

  console.log("Permissões atualizadas com sucesso!");
} catch (error) {
  console.error("Falha ao editar permissões:", error.message);
}
```
{% endtab %}

{% tab title="Remover Membro da Equipe" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appTeam.delete("your_app_id", "user_id");
  console.log("Moderador removido com sucesso!");
} catch (error) {
  console.error("Falha ao remover moderador:", error.message);
}
```
{% endtab %}
{% endtabs %}

***

## ⚙️ Gerenciamento do Sistema

### 🔧 Gerenciando Alocação de RAM

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.ram("your_app_id", 512);
  console.log("RAM atualizada com sucesso!");
} catch (error) {
  console.error("Atualização de RAM falhou:", error.message);
}
```

{% hint style="warning" %}
#### **Requisitos de RAM**

* Aplicações bot: mínimo 100MB
* Aplicações website: mínimo 512MB
* Verifique os limites do seu plano antes de aumentar a RAM
{% endhint %}

### 🎨 Atualizando Perfil da Aplicação

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.profile("your_app_id", {
    name: "Meu Bot Incrível",
    avatarURL: "https://example.com/avatar.png",
  });

  console.log("Perfil atualizado com sucesso!");
} catch (error) {
  console.error("Atualização de perfil falhou:", error.message);
}
```

{% hint style="info" %}
#### **Detalhes da Atualização do Perfil**

* `name`: Opcional. Novo nome para sua aplicação (máximo 30 caracteres).
* `avatarURL`: Opcional. URL da nova imagem de avatar. Formatos suportados: GIF, JPG, JPEG, PNG.
{% endhint %}

### 📦 Gerenciamento de Pacotes APT

#### 📥 Instalando Pacotes APT

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appApt.install("your_app_id", [
    "tools",
    "canvas",
    "tesseract",
    "puppeteer",
    "selenium",
    "java",
    "ffmpeg",
    "libgl",
    "openssl",
    "mysql",
    "unixodbc",
  ]);

  console.log("Pacotes instalados com sucesso!");
} catch (error) {
  console.error("Instalação falhou:", error.message);
}
```

#### 🗑️ Desinstalando Pacotes APT

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appApt.uninstall("your_app_id", ["canvas", "ffmpeg"]);
  console.log("Pacotes desinstalados com sucesso!");
} catch (error) {
  console.error("Desinstalação falhou:", error.message);
}
```
