---
description: Aprenda a hospedar seu bot em Python na DisCloud
---

# 🐍 Python

## 📥 Arquivos principais

**`main.py`** e **`requirements.txt`**

![O arquivo principal do seu bot, ou seja, o local onde está o bot.run(). GERALMENTE é main.py](<../../../.gitbook/assets/capturar (1).PNG>)

{% hint style="warning" %}
**Quaisquer outros arquivos que seja necessário em seu Bot sem ser esses dois podem ser adicionados**. (Isso vale para as cogs também).
{% endhint %}

{% content-ref url="../../faq/qual-o-arquivo-principal.md" %}
[qual-o-arquivo-principal.md](../../faq/qual-o-arquivo-principal.md)
{% endcontent-ref %}

## Requirements

O `requirements.txt` deve conter as bibliotecas usadas no seu Bot, por padrão, deve no mínimo conter a livraria `discord.py`, caso use a livraria `disco-py` basta substituir.

{% hint style="warning" %}
As bibliotecas **NÃO SÃO as que você importa**, e sim as que você instala.\
Ex.: **`import PIL`** mas você instala usando **`pip install pillow`**, logo deve ser colocado **pillow** e não **PIL** no seu arquivo `requirements.txt`
{% endhint %}

{% content-ref url="exemplo-do-requirements.txt.md" %}
[exemplo-do-requirements.txt.md](exemplo-do-requirements.txt.md)
{% endcontent-ref %}

## Preparando seu Bot para enviar para a Discloud

• Faça um **`.zip`** com os arquivos.

{% content-ref url="../../faq/como-compactar-zipar-os-meus-arquivos.md" %}
[como-compactar-zipar-os-meus-arquivos.md](../../faq/como-compactar-zipar-os-meus-arquivos.md)
{% endcontent-ref %}

![Exemplo no Windows](<../../../.gitbook/assets/image (13).png>)

## ✍ Hospedando o seu Bot

{% hint style="info" %}
Escolha o método para hospedar seu Bot na Discloud:
{% endhint %}

{% content-ref url="../../como-hospedar/website.md" %}
[website.md](../../como-hospedar/website.md)
{% endcontent-ref %}

{% content-ref url="../../como-hospedar/discord.md" %}
[discord.md](../../como-hospedar/discord.md)
{% endcontent-ref %}

## ✅ Finalizado <a href="#finalizado" id="finalizado"></a>

Pronto, em alguns segundos ou minutos, o seu Bot estará online.

![](../../../.gitbook/assets/capturar.PNG)
