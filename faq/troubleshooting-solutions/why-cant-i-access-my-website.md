---
description: >-
  Lista de verificação para quando o seu site ou API hospedado na Discloud não
  abre.
---

# Por que não consigo acessar meu site?

Se o endereço do seu site ou API não abre, confira os itens abaixo. Na maioria dos casos, o problema é um deles.

***

## ✅ Lista de verificação

{% stepper %}
{% step %}
**Plano Platinum ou superior**

Sites e APIs precisam do [**Plano Platinum ou superior**](https://discloud.com/plans).
{% endstep %}

{% step %}
**`TYPE=site` no `discloud.config`**

O seu [`discloud.config`](../../configurations/discloud.config/) precisa ter `TYPE=site`. Com `TYPE=bot`, a aplicação não recebe acesso externo.
{% endstep %}

{% step %}
**`ID` com o subdomínio registrado**

O campo `ID` deve ter o nome de um [subdomínio registrado](../general-questions/how-to-create-a-subdomain.md) na sua conta, **sem** `.discloud.app` nem `.discloud.dev`:

```ini
TYPE=site
ID=meuapp
```
{% endstep %}

{% step %}
**Endereço certo: `.discloud.app` ou `.discloud.dev`**

Os subdomínios da Discloud podem ficar em `.discloud.app` ou em `.discloud.dev`. Não é você que escolhe: o domínio é escolhido automaticamente pela Discloud no momento da criação do subdomínio. Confira no [**Painel**](https://discloud.com/dashboard), na aba **Domínios**, qual é o endereço do seu subdomínio e abra esse.
{% endstep %}

{% step %}
**Porta 8080 e host 0.0.0.0**

A sua aplicação deve ouvir na porta **`8080`** e no host **`0.0.0.0`**. Se ela ouvir em outra porta ou em `localhost`/`127.0.0.1`, o tráfego não chega até ela.
{% endstep %}

{% step %}
**RAM suficiente**

Sites precisam de no mínimo **512MB** de RAM.
{% endstep %}

{% step %}
**Aplicação online**

Confira se a aplicação iniciou sem erros. Se ela travou ou parou, o site não abre. Veja [**Como acessar os logs da aplicação?**](../general-questions/how-to-access-the-application-logs.md).
{% endstep %}
{% endstepper %}

***

## 🌍 Usando domínio personalizado?

Se o problema é só no seu próprio domínio (e o subdomínio da Discloud funciona), confira a configuração de DNS em [**Domínio Personalizado**](../../api-and-integrations/custom-domain.md).

***

## 📚 Veja também

* [**Websites e APIs**](../../how-to-host/websites-and-apis.md)
* [**Como criar um subdomínio?**](../general-questions/how-to-create-a-subdomain.md)
* [**Diagnosticando Aplicações Offline**](diagnosing-offline-applications.md)

***

## ❓ Ainda precisa de ajuda?

Veja [**Soluções de Problemas**](./) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
