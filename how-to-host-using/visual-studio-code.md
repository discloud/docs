---
description: Como hospedar sua aplicação via a extensão Discloud no Visual Studio Code.
icon: plug
---

# Visual Studio Code

A [**Extensão Discloud para VSCode**](https://marketplace.visualstudio.com/items?itemName=discloud.discloud) permite que você **hospede e gerencie suas aplicações** diretamente do [**Visual Studio Code**](https://code.visualstudio.com/), eliminando a necessidade de usar um painel web ou comandos do bot Discord.

***

## 🛠️ Instalando a Extensão Discloud

{% stepper %}
{% step %}
Abra o VSCode no seu computador.
{% endstep %}

{% step %}
Vá para a aba Extensões (`Ctrl + Shift + X`).

* Na barra de pesquisa, digite: **"Discloud"** e clique em **"Instalar"**.
{% endstep %}
{% endstepper %}

***

## 🔑 Fazendo Login na Discloud

Antes de fazer o upload, você precisa fazer login na sua **conta Discloud**.

{% stepper %}
{% step %}
Clique na **aba da Extensão Discloud** na **barra lateral do VSCode**.
{% endstep %}

{% step %}
Clique em **"Enviar seu token Discloud"** e insira seu [**Token da API Discloud**](../faq/general-questions/how-can-i-get-my-discloud-api-token.md).

<figure><img src="../.gitbook/assets/VSCode-Extension_Login.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
Após o login, suas **aplicações Discloud** aparecerão dentro da aba da extensão.
{% endstep %}
{% endstepper %}

***

## 🚀 Fazendo Upload da Sua Aplicação

Com a **Extensão VSCode**, você pode fazer o upload do seu app em apenas alguns cliques!

{% stepper %}
{% step %}
Preparando seu projeto.

* Certifique-se de que seu projeto contenha todos os arquivos necessários:
  * [**`discloud.config`**](https://github.com/discloud/docs/blob/portuguese/configurations/discloud.config) (arquivo de configuração).
  * **Dependências** necessárias para sua linguagem de programação (ex.: `package.json` para Node.js, `requirements.txt` para Python).
* **Verifique o** [**Guia de Linguagens**](../development-environment/supported-languages/) para garantir que seu projeto esteja estruturado corretamente.
{% endstep %}

{% step %}
Fazendo upload da sua aplicação.

<figure><img src="../.gitbook/assets/VSCode-Extension_Upload.gif" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

***

## 📌 Dicas e Truques

### 📂 **Usando `.discloudignore` para Excluir Arquivos**

Se você quiser **excluir certos arquivos ou diretórios** do upload, pode criar um arquivo [`.discloudignore`](../configurations/.discloudignore.md) na raiz do seu projeto.

***

## **❓ Ainda precisa de ajuda?**

Verifique a [**Seção FAQ**](https://app.gitbook.com/s/vUqkKIFudeQ2TQOirm35/faq) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
