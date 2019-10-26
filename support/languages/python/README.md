---
description: Aprenda a hospedar seu bot em Python na DisCloud
---

# Python

## 📥 Main Files

**`main.py`** and **`requirements.txt`**

![The main file of your bot, that is, the local where is the bot.run\(\). USUALLY is main.py](../../../.gitbook/assets/capturar%20%281%29.PNG)

{% hint style="warning" %}
**Any other files as necessary in your bot without being these two files can be added.** \(this goes for cogs too\).
{% endhint %}

{% page-ref page="../../../faq/what-is-the-main-file.md" %}

## Requirements

The `requirements.txt` need to have the libraries used in your bot, by default, need to have at least the librarie `discord.py`, in case you use the librarie `disco-py` just replace.

{% hint style="warning" %}
The libraries **IS NOT the ones you import** but the ones you install.  
Example.: **`import PIL`** but your install using**`pip install pillow`**, should soon be placed the **pillow** and not **PIL** in your `requirements.txt` file
{% endhint %}

{% page-ref page="example-of-requirements.txt.md" %}

## Preparing your bot to send to DisCloud

• Zip your files.

{% page-ref page="../../../faq/how-to-compact-your-files.md" %}

![Exemplo no Windows](../../../.gitbook/assets/image%20%2812%29.png)



## ✍ Hosting your bot

{% hint style="info" %}
Choose the method to host your bot on DisCloud:
{% endhint %}

{% page-ref page="../../how-to-host/website.md" %}

{% page-ref page="../../how-to-host/discord.md" %}

## ✅ Finished <a id="finalizado"></a>

Finish, in some seconds or minutes, your bot will be online.

![](../../../.gitbook/assets/capturar.PNG)

