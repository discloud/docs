---
description: Aprenda a hospedar seu bot em Python na DisCloud
---

# Python

## 📥 Arquivos principais

**`main.py`** e **`requirements.txt`**

![O arquivo principal do seu bot, ou seja, o local onde est&#xE1; o bot.run\(\). GERALMENTE &#xE9; main.py](../../../.gitbook/assets/capturar%20%281%29.PNG)

{% hint style="warning" %}
**Quaisquer outros arquivos que seja necessário em seu Bot sem ser esses dois podem ser adicionados**. \(Isso vale para as cogs também\).
{% endhint %}

{% page-ref page="../../../faq/qual-o-arquivo-principal.md" %}

## Requirements

O `requirements.txt` deve conter as bibliotecas usadas no seu Bot, por padrão, deve no mínimo conter a livraria `discord.py`, caso use a livraria `disco-py` basta substituir.

{% hint style="warning" %}
As bibliotecas **NÃO SÃO as que você importa**, e sim as que você instala.  
Ex.: **`import PIL`** mas você instala usando **`pip install pillow`**, logo deve ser colocado **pillow** e não **PIL** no seu arquivo `requirements.txt`
{% endhint %}

{% page-ref page="example-of-requirements.txt.md" %}

## Preparando seu Bot para enviar para a Discloud

• Faça um **`.zip`** com os arquivos.

{% page-ref page="../../../faq/como-compactar-zipar-os-meus-arquivos.md" %}

![Exemplo no Windows](../../../.gitbook/assets/image%20%2811%29.png)



## ✍ Hospedando o seu Bot

{% hint style="info" %}
Escolha o método para hospedar seu Bot na Discloud:
{% endhint %}

{% page-ref page="../../how-to-host/website.md" %}

{% page-ref page="../../how-to-host/discord.md" %}

## ✅ Finalizado <a id="finalizado"></a>

Pronto, em alguns segundos ou minutos, o seu Bot estará online.

![](../../../.gitbook/assets/capturar.PNG)

