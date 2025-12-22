---
description: Guia completo para hospedar aplicações Python na Discloud.
icon: python
---

# Python

## 📁 **Preparando os Arquivos**

Antes de fazer upload do seu projeto, você deve **excluir arquivos desnecessários** para otimizar o deploy.

#### ❌ **Arquivos a Excluir**

Certifique-se de que os seguintes arquivos e diretórios **não** sejam incluídos no seu [`.zip`](../../../faq/general-questions/em-andamento-como-comprimir.md):

```diff
- .cache/
- .git/
- venv/
```

📌 **Use um arquivo** [**`.discloudignore`**](../../../configurations/.discloudignore.md) **para excluir automaticamente esses arquivos.**

🔗 **Precisa de ajuda para configurar seu** [**`requirements.txt`**](requirements.txt.md) **ou encontrar o** [**arquivo principal**](../../../faq/general-questions/what-is-the-main-file.md)**?**

***

## ✍️ Fazendo Deploy **da Sua Aplicação**

Uma vez que seu projeto esteja **configurado e comprimido**, você pode escolher um dos seguintes **métodos de deploy** na Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Faça upload e gerencie sua aplicação via interface web.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Faça deploy diretamente através dos comandos do bot Discord da Discloud.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integre com VS Code para gerenciamento contínuo de projetos.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use a interface de linha de comando para deploy rápido e eficiente.</td><td></td><td></td><td></td></tr></tbody></table>
