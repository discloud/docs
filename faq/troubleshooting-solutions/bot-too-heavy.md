---
description: >-
  O que fazer quando o arquivo .zip da sua aplicação é grande demais para ser
  enviado.
---

# Bot muito pesado

Se o upload falha porque o arquivo é grande demais, o problema quase sempre está no **conteúdo do `.zip`**: ele leva arquivos que a Discloud não precisa receber.

***

## 🗑️ Deixe de fora o que não precisa ser enviado

{% hint style="warning" %}
#### **Pastas de dependências**

Pastas como `node_modules`, `venv` ou `.venv` costumam ser a maior parte do projeto. Não envie essas pastas: as dependências ficam listadas no arquivo de dependências da sua linguagem (por exemplo, `package.json` ou `requirements.txt`).
{% endhint %}

{% hint style="warning" %}
#### **Saída de build**

Se você usa o comando `BUILD` no [`discloud.config`](../../configurations/discloud.config/), a Discloud gera o build durante o deploy. Nesse caso, não envie a pasta gerada pelo build local.
{% endhint %}

{% hint style="warning" %}
#### **Arquivos de mídia grandes**

Vídeos, imagens e áudios grandes deixam o `.zip` pesado. Guarde esses arquivos em um serviço de armazenamento externo e carregue-os pela URL.
{% endhint %}

{% hint style="warning" %}
#### **Arquivos de controle e cache**

Pastas como `.git` e `__pycache__` não são necessárias para rodar a aplicação.
{% endhint %}

{% hint style="info" %}
Use um arquivo [`.discloudignore`](../../configurations/.discloudignore.md) para que esses arquivos fiquem de fora automaticamente. Veja também [**Como comprimir?**](../general-questions/how-to-compress.md).
{% endhint %}

***

## 🔀 Use outro método de envio

Ao enviar pelo **Bot do Discord**, o `.zip` é um anexo de mensagem, por isso também precisa caber no **limite de anexos do Discord**. Para projetos maiores, prefira um destes métodos:

* 🖥️ [**Painel de Controle**](../../how-to-host-using/dashboard.md)
* ⌨️ [**CLI**](../../how-to-host-using/cli.md)
* 🟦 [**Extensão do VS Code**](../../how-to-host-using/visual-studio-code.md)

***

## ❓ Ainda precisa de ajuda?

Veja [**Soluções de Problemas**](./) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
