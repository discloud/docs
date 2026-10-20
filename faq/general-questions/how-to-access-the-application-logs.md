---
description: >-
  Veja os logs da sua aplicação na Discloud para entender erros e acompanhar o
  que está acontecendo.
---

# Como acessar os logs da aplicação?

Os **logs** mostram tudo o que a sua aplicação escreve no terminal: mensagens de inicialização, avisos e erros. São o primeiro lugar para olhar quando a aplicação não inicia, fica offline ou não se comporta como esperado.

***

## 📋 Onde ver os logs

{% tabs %}
{% tab title="🖥️ Painel" %}
{% stepper %}
{% step %}
Abra o [**Painel da Discloud**](https://discloud.com/dashboard) e vá em **Aplicações**.
{% endstep %}

{% step %}
Clique na sua aplicação.
{% endstep %}

{% step %}
No menu lateral, clique em **Logs**.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Na página de logs você pode:

* **Buscar** um texto nos logs.
* Escolher o **período** que quer ver (por exemplo, a última hora).
* Ativar **Ao vivo** para ver os novos logs assim que aparecem.
* Mostrar ou esconder o **Timestamp** de cada linha.
* Filtrar por nível: **Trace**, **Debug**, **Info**, **Warn**, **Error** e **Fatal**.
{% endhint %}
{% endtab %}

{% tab title="🤖 Bot do Discord" %}
{% stepper %}
{% step %}
Vá ao canal [**`#🔌・commands`**](https://discord.com/channels/584490943034425391/1051126795883261962) no **Servidor Discord da Discloud**.
{% endstep %}

{% step %}
Execute o comando:

```
/logs
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="⌨️ CLI" %}
Execute:

```bash
discloud app logs <ID_DA_APLICACAO>
```

Veja como instalar e entrar na [CLI](../../how-to-host-using/cli.md).
{% endtab %}

{% tab title="🟦 VS Code" %}
{% stepper %}
{% step %}
Abra a aba da **Discloud** na barra lateral do VS Code.
{% endstep %}

{% step %}
Na lista **Apps**, clique com o botão direito na aplicação e escolha **Obter logs do app**.
{% endstep %}
{% endstepper %}

Veja como instalar e entrar na [extensão do VS Code](../../how-to-host-using/visual-studio-code.md).
{% endtab %}

{% tab title="🔌 API" %}
Faça uma requisição `GET` para:

```
/app/{appID}/logs
```

Veja os detalhes do endpoint em [**Aplicações**](../../api-and-integrations/api-overview/applications.md).
{% endtab %}
{% endtabs %}

***

## 🔍 O que procurar nos logs

* **Erros na inicialização:** confira se o [arquivo principal](what-is-the-main-file.md) e o [`discloud.config`](../../configurations/discloud.config/) estão corretos.
* **Dependências não encontradas:** confira se todas estão listadas no arquivo de dependências da sua linguagem (por exemplo, `package.json` ou `requirements.txt`).
* **A aplicação para sozinha:** veja [**Diagnosticando Aplicações Offline**](../troubleshooting-solutions/diagnosing-offline-applications.md).

{% hint style="info" %}
Ao pedir ajuda no suporte, envie a parte dos logs com o erro. Isso ajuda a encontrar o problema muito mais rápido.
{% endhint %}

***

## ❓ Ainda precisa de ajuda?

Veja [**Soluções de Problemas**](../troubleshooting-solutions/) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
