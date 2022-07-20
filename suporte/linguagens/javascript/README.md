---
description: Aprenda a hospedar seu bot em JavaScript na DisCloud
---

# 📦 JavaScript

## :file\_folder: Arquivos principais

Antes de tudo, **não envie todos os arquivos** de uma vez, você precisará colocar os arquivos do seu bot em uma pasta `.zip`. Não é necessário o upload dos arquivos `node_modules` e `package-lock.json`.

![](<../../../.gitbook/assets/image (36).png>)

Para mais detalhes sobre como **Compactar os seus Arquivos** e de acordo com o seu Sistema Operativo, pode consultar aqui abaixo:

{% content-ref url="../../faq/como-compactar-zipar-os-meus-arquivos.md" %}
[como-compactar-zipar-os-meus-arquivos.md](../../faq/como-compactar-zipar-os-meus-arquivos.md)
{% endcontent-ref %}



## ✍ Hospedando o seu bot

{% hint style="info" %}
Você pode aprender a hospedar seu bot na [versão website](../../como-hospedar/website.md) ou [Discord](../../como-hospedar/discord.md)
{% endhint %}

{% content-ref url="../../website/bots/via-painel-de-controle.md" %}
[via-painel-de-controle.md](../../website/bots/via-painel-de-controle.md)
{% endcontent-ref %}

{% content-ref url="../../como-hospedar/discord.md" %}
[discord.md](../../como-hospedar/discord.md)
{% endcontent-ref %}

## :earth\_americas: Hospedando o Seu Site

{% hint style="info" %}
Esta funcionalidade necessita de alguns requisitos básicos para poder ser utilizada, por favor consulte os requisitos [aqui](../../website/sites/#requisitos) antes de continuar
{% endhint %}

{% content-ref url="../../website/sites/" %}
[sites](../../website/sites/)
{% endcontent-ref %}

### Utilizando o Express

O **Express** é uma framework muito utilizada na construção de Sites e APIs.

Por padrão o **Express** está configurado para ouvir a porta **`3000`**, você precisa de configurar para ouvir a porta **`8080`**, procure pela seguinte linha geralmente se encontra no seu [arquivo principal](../../faq/qual-o-arquivo-principal.md).

```javascript
app.listen(8080);
```

