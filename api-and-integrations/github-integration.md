---
description: Hospede apps do GitHub na Discloud em 3 passos.
icon: github
---

# Integração com GitHub

## ✅ **Pré-requisitos**

{% stepper %}
{% step %}
**Consistência da Conta GitHub**

{% hint style="warning" %}
A conta GitHub usada para **login na Discloud** E **propriedade do repositório deve ser a mesma.**
{% endhint %}

> **Consequências de incompatibilidade**:
>
> * Repositórios não aparecerão
> * Falhas de uploads
> * Erros de permissão
{% endstep %}

{% step %}
**Arquivo** [**`discloud.config`**](../configurations/discloud.config/) **Válido**

Deve existir no **diretório raiz** do seu repositório.

> ⚠️ **A validação falha se**:
>
> * Arquivo ausente
> * Sintaxe inválida
{% endstep %}
{% endstepper %}

***

## 🔄 **Conectar GitHub e Configurar Acesso**

{% stepper %}
{% step %}
Iniciar Conexão GitHub

* Vá para [Painel Discloud](https://discloud.com/dashboard) → aba **Integração GitHub**
*   Clique em **Login** → Autorize Discloud via GitHub OAuth

    <figure><img src="../.gitbook/assets/GitHub-Integration_Login.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
Configurar Acesso ao Repositório

* Volte para **Integração GitHub** → Clique em **Configurar**
* Escolha o alvo da instalação.
* Defina permissões:
  * 🔓 _Todos os repositórios_
  * 🔒 _Selecionar repositórios específicos_
{% endstep %}
{% endstepper %}

***

## 🚀 **Upload do GitHub**

{% stepper %}
{% step %}
**Iniciar Upload**

* Vá para [Painel Discloud](https://discloud.com/dashboard)
* Clique em "**+ Upload"** (canto superior direito)
* Selecione "**GitHub"** no menu
{% endstep %}

{% step %}
**Configuração e Upload**

{% hint style="info" %}
#### **🔐 Variáveis de Ambiente Seguras**

Use arquivos [`.env`](../faq/general-questions/arquivo-.env.md) localmente para desenvolvimento, mas certifique-se de que eles sejam adicionados ao `.gitignore` para evitar exposição acidental no GitHub. Ao fazer o upload via integração GitHub da Discloud, **adicione segredos de produção diretamente na seção "Variáveis de Ambiente"** durante a configuração.
{% endhint %}
{% endstep %}
{% endstepper %}

<figure><img src="../.gitbook/assets/GitHub-Integration_Upload.gif" alt=""><figcaption></figcaption></figure>
