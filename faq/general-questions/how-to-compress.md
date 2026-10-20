---
description: >-
  Aprenda a criar o arquivo .zip do seu projeto do jeito certo para enviá-lo à
  Discloud.
---

# Como comprimir?

Para enviar uma aplicação à Discloud, você precisa de um arquivo **`.zip`** com o projeto. O mais importante é **o que fica dentro dele**: ao abrir o `.zip`, os arquivos do projeto devem aparecer logo de cara, sem nenhuma pasta por fora.

***

## 📂 O que deve estar dentro do `.zip`

O `.zip` deve começar direto na [raiz do projeto](what-is-the-root-of-the-project.md), onde ficam o `discloud.config` e o [arquivo principal](what-is-the-main-file.md).

{% tabs %}
{% tab title="✅ Correto" %}
```
meu-bot.zip
├── discloud.config
├── package.json
└── src/
    └── index.js
```

Ao abrir o `.zip`, os arquivos do projeto aparecem logo no primeiro nível.
{% endtab %}

{% tab title="❌ Incorreto" %}
```
meu-bot.zip
└── meu-bot/
    ├── discloud.config
    ├── package.json
    └── src/
        └── index.js
```

A pasta `meu-bot/` ficou por fora. Assim, o `discloud.config` e o arquivo principal não estão na raiz do `.zip`.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Comprima o conteúdo da pasta, não a pasta.** Entre na pasta do projeto, selecione os arquivos e pastas que estão lá dentro e comprima. Se você comprimir a pasta do projeto inteira, ela entra no `.zip` e todo o projeto fica um nível abaixo.
{% endhint %}

***

## 🗑️ O que deixar de fora

Não envie arquivos que não são necessários para rodar a aplicação. Isso deixa o upload menor e mais rápido.

```diff
- node_modules
- venv
- .git
- .DS_Store
- __pycache__
```

{% hint style="info" %}
Use um arquivo [`.discloudignore`](../../configurations/.discloudignore.md) para listar os arquivos e pastas que devem ficar de fora dos seus envios.
{% endhint %}

***

## 🛠️ Como criar o `.zip`

{% tabs %}
{% tab title="🪟 Windows" %}
{% stepper %}
{% step %}
Abra a pasta do projeto e selecione todo o conteúdo (`Ctrl` + `A`).
{% endstep %}

{% step %}
Clique com o botão direito na seleção e escolha **Compactar para arquivo ZIP** (Windows 11) ou **Enviar para > Pasta compactada** (Windows 10).
{% endstep %}

{% step %}
Dê um nome ao arquivo, por exemplo `meu-bot.zip`.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🍎 macOS" %}
{% stepper %}
{% step %}
Abra a pasta do projeto no Finder e selecione todo o conteúdo (`Cmd` + `A`).
{% endstep %}

{% step %}
Clique com o botão direito na seleção e escolha **Comprimir**.
{% endstep %}

{% step %}
O macOS cria um arquivo `Arquivo.zip`. Renomeie-o se quiser, por exemplo `meu-bot.zip`.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="🐧 Linux" %}
No terminal, dentro da pasta do projeto, execute:

```bash
zip -r ../meu-bot.zip . -x "node_modules/*" ".git/*"
```

O `.zip` é criado na pasta de cima, com o conteúdo do projeto direto na raiz. Use `-x` para deixar de fora outras pastas que não precisam ser enviadas.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Envie sempre um arquivo **`.zip`**. Outros formatos, como `.rar` ou `.7z`, não são aceitos.
{% endhint %}

***

## 🔄 Atualizando uma aplicação

Para mudar só alguns arquivos de uma aplicação que já está na Discloud, você não precisa enviar o projeto inteiro. Veja [**Como fazer commit?**](how-to-commit.md).

***

## ❓ Ainda precisa de ajuda?

Veja [**Soluções de Problemas**](../troubleshooting-solutions/) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
