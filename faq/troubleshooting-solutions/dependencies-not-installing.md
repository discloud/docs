---
description: >-
  Como resolver erros de instalação de dependências e de build ao enviar uma
  aplicação para a Discloud.
---

# Por que as dependências não instalam?

Durante o deploy, a Discloud instala as dependências listadas no arquivo de dependências da sua linguagem. Se essa etapa falha, a aplicação não inicia. Os [logs](../general-questions/how-to-access-the-application-logs.md) mostram qual pacote deu erro.

***

## 📄 O arquivo de dependências

Confira se o arquivo certo está na [raiz do projeto](../general-questions/what-is-the-root-of-the-project.md) e se lista tudo o que o código usa:

| Linguagem  | Arquivo                                                                                                             |
| ---------- | ------------------------------------------------------------------------------------------------------------------- |
| JavaScript | [`package.json`](../../development-environment/supported-languages/javascript/package.json.md)                      |
| Python     | [`requirements.txt`](../../development-environment/supported-languages/python/requirements.txt.md)                  |
| Java       | Um `.jar` já compilado. Veja [como construir](../general-questions/how-to-build-and-package-a-java-application.md). |

{% hint style="warning" %}
Não envie pastas como `node_modules` ou `venv`. A Discloud instala as dependências a partir do arquivo. Use um [`.discloudignore`](../../configurations/.discloudignore.md) para deixá-las de fora.
{% endhint %}

***

## 🔍 Causas comuns

{% hint style="warning" %}
#### **Pacote que não existe ou com nome errado**

Um erro de digitação no nome ou uma versão que não existe faz a instalação falhar. Teste localmente com `npm install` ou `pip install -r requirements.txt` antes de enviar.
{% endhint %}

{% hint style="warning" %}
#### **Versão da linguagem incompatível**

Alguns pacotes exigem uma versão mínima do Node.js ou do Python. Defina a versão certa com a opção `VERSION` do [`discloud.config`](../../configurations/discloud.config/). Veja as [versões disponíveis](../../configurations/discloud.config/versions.md).
{% endhint %}

{% hint style="warning" %}
#### **Pacote que precisa de bibliotecas do sistema**

Pacotes como `canvas` ou bibliotecas de áudio e vídeo dependem de bibliotecas do Linux. Instale-as com a opção [`APT`](../../configurations/discloud.config/apt.md) do `discloud.config`, por exemplo `APT=canvas` ou `APT=ffmpeg`.
{% endhint %}

{% hint style="warning" %}
#### **Pacote que só funciona no Windows ou no macOS**

A Discloud roda em Linux. Pacotes feitos só para outro sistema não instalam. Procure uma alternativa compatível com Linux.
{% endhint %}

{% hint style="warning" %}
#### **Lockfile de outro gerenciador**

Um `package-lock.json` desatualizado ou gerado em outro sistema pode causar conflitos. Gere de novo localmente ou deixe-o de fora do envio.
{% endhint %}

***

## 🛠️ Como testar antes de enviar

{% stepper %}
{% step %}
**Instale do zero**

Apague `node_modules` ou o ambiente virtual e instale de novo, só a partir do arquivo de dependências.
{% endstep %}

{% step %}
**Rode a aplicação**

Inicie a aplicação localmente com o mesmo comando que a Discloud vai usar.
{% endstep %}

{% step %}
**Envie de novo**

Se funcionou localmente, envie de novo e acompanhe os [logs](../general-questions/how-to-access-the-application-logs.md) durante o deploy.
{% endstep %}
{% endstepper %}

***

## ❓ Ainda precisa de ajuda?

Veja [**Soluções de Problemas**](./) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
