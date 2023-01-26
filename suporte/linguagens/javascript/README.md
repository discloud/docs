---
description: Aprenda a hospedar seu bot em JavaScript na DisCloud
---

# 🟨 JavaScript

## :file\_folder: Arquivos

Você não deve enviar todos os arquivos de sua aplicação para o `.zip`, existem algumas exceções, elas são:

```diff
- Pasta node_modules
- Arquivo package-lock.json
- Pasta .git
```

> * Dúvidas para encontrar o seu arquivo principal? [Clique aqui](../../faq/arquivo-principal.md#arquivos-principais-gerais)
> * Dúvidas em criar o seu  arquivo `package.json`? [Clique aqui](criar-package.json.md)

{% content-ref url="criar-package.json.md" %}
[criar-package.json.md](criar-package.json.md)
{% endcontent-ref %}

### :compression: Compactando os Arquivos

Selecione apenas os arquivos necessários, como mencionado em cima e crie o seu **.zip**

![](<../../../.gitbook/assets/image (6).png>)

Para mais detalhes sobre como **Compactar os seus Arquivos** de acordo com o seu **Sistema Operativo**, pode consultar em baixo:

{% content-ref url="../../faq/zip.md" %}
[zip.md](../../faq/zip.md)
{% endcontent-ref %}

## ✍ Hospedando o seu bot

{% hint style="info" %}
Escolha o método para hospedar seu Bot na Discloud:
{% endhint %}

{% content-ref url="../../hospedar/bots/dashboard.md" %}
[dashboard.md](../../hospedar/bots/dashboard.md)
{% endcontent-ref %}

{% content-ref url="../../hospedar/bots/discord.md" %}
[discord.md](../../hospedar/bots/discord.md)
{% endcontent-ref %}

{% content-ref url="../../hospedar/bots/vscode.md" %}
[vscode.md](../../hospedar/bots/vscode.md)
{% endcontent-ref %}

{% content-ref url="../../hospedar/bots/cli.md" %}
[cli.md](../../hospedar/bots/cli.md)
{% endcontent-ref %}

## :earth\_americas: Hospedando o Seu Site

{% hint style="info" %}
Esta funcionalidade necessita de alguns requisitos básicos para poder ser utilizada, por favor consulte os requisitos [aqui](../../hospedar/sites/#requisitos) antes de continuar
{% endhint %}

### Utilizando o Express

O **Express** é uma framework muito utilizada na construção de Sites e APIs.

Por padrão o **Express** está configurado para ouvir a porta **`3000`**, você precisa de configurar para ouvir a porta **`8080`**, procure pela seguinte linha geralmente se encontra no seu [arquivo principal](../../faq/arquivo-principal.md).

```javascript
app.listen(8080);
```

