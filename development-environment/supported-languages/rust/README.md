---
description: Guia completo para hospedar aplicações Rust na Discloud.
icon: rust
---

# Rust

## 📁 **Preparando os Arquivos**

Antes de fazer upload do seu projeto, você deve **excluir arquivos desnecessários** para otimizar o deploy.

#### ❌ **Arquivos a Excluir**

Certifique-se de que os seguintes arquivos e diretórios **não** sejam incluídos no seu [`.zip`](../../../faq/general-questions/how-to-compress.md):

```diff
- Cargo.lock
- target/
- .git/
```

📌 **Use um arquivo** [**`.discloudignore`**](../../../configurations/.discloudignore.md) **para excluir automaticamente esses arquivos.**

🔗 **Precisa de ajuda para configurar seu** [**`Cargo.toml`**](cargo.toml.md) **ou encontrar o** [**arquivo principal**](../../../faq/general-questions/what-is-the-main-file.md)**?**

***

## 🌐 Hospedando Seu Site com Rocket

Antes de fazer deploy do seu website ou API na Discloud, certifique-se de que você atenda aos seguintes **requisitos**:

{% hint style="success" %}
[Plano Platinum ou superior](https://discloud.com/plans) é necessário para hospedar websites ou APIs.
{% endhint %}

{% hint style="success" %}
[Um subdomínio deve ser criado](../../../faq/general-questions/how-to-create-a-subdomain.md) antes do deploy.
{% endhint %}

{% hint style="danger" %}
Porta `8080` é obrigatória – As aplicações devem escutar nesta porta.
{% endhint %}

***

## 🚀 Configurando `Rocket`

[Rocket](https://rocket.rs/) é um framework web para Rust que, a partir da versão 0.5, funciona no Rust estável. Por padrão, o Rocket escuta em `127.0.0.1:8000`. Para a Discloud, crie um arquivo `Rocket.toml` na raiz do projeto para que ele escute em `0.0.0.0:8080`:

{% code title="Rocket.toml" %}
```toml
[default]
address = "0.0.0.0"
port = 8080
```
{% endcode %}

***

## ✍️ Fazendo Deploy **da Sua Aplicação**

Uma vez que seu projeto esteja **configurado e comprimido**, você pode escolher um dos seguintes **métodos de deploy** na Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Faça upload e gerencie sua aplicação via interface web.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/discord-bot/">discord-bot</a></td><td align="center">Faça deploy diretamente através dos comandos do bot Discord da Discloud.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integre com VS Code para gerenciamento contínuo de projetos.</td><td></td><td></td><td></td></tr><tr><td><a href="../../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use a interface de linha de comando para deploy rápido e eficiente.</td><td></td><td></td><td></td></tr></tbody></table>
