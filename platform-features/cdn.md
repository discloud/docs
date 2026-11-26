---
description: >-
  Armazene e sirva arquivos públicos pela CDN da Discloud. A cota é um add-on
  independente do plano de bots e sites.
icon: cloud
tags:
  - novo
---

# CDN

## 📦 O que é a CDN?

A CDN da Discloud é um **armazenamento de arquivos públicos** da sua conta. Você sobe imagens, assets, documentos ou qualquer arquivo estático e recebe uma URL pública em `cdn.discloud.com`.

Ela **não** usa a RAM nem o disco do plano de bots e sites. A cota vem do [add-on CDN](/broken/pages/addons-product): você paga pelos **GB armazenados**. Tráfego de entrada e saída é ilimitado — não há cobrança por banda.

{% hint style="info" %}
A leitura dos arquivos é pública. Qualquer pessoa com a URL consegue baixar. Não guarde segredos, tokens nem backups privados na CDN.
{% endhint %}

***

## 📍 Onde fica

[Painel da Discloud](https://discloud.com/dashboard) → **CDN**.

* Lista arquivos e pastas da conta
* Upload (simples ou em partes para arquivos grandes)
* Criar / apagar pastas
* Ver uso e quota do add-on

A compra e o ajuste da cota ficam em **Assinatura → Add-ons** (tipo **CDN**). Detalhes em [Add-ons](/broken/pages/addons-product).

Para automatizar uploads e gestão, veja a [API de CDN](../api-and-sdks/api-overview/cdn.md).

***

## 📋 Requisitos

{% hint style="success" %}
**Add-on CDN ativo** – Sem o add-on (ou com 0 GB), o painel e a API recusam escrita. A leitura pública de URLs já existentes continua possível enquanto o arquivo existir.
{% endhint %}

Não há plano mínimo de bots/sites para usar a CDN. Free ou qualquer plano pode contratar o add-on.

***

## 💾 Cota

| Item             | Valor                                |
| ---------------- | ------------------------------------ |
| Unidade          | GB armazenados                       |
| Mínimo na compra | **50 GB**                            |
| Degrau           | de **50 em 50 GB**                   |
| Banda            | Ilimitada (sem cobrança por tráfego) |

O painel mostra **usado**, **quota** e **restante**. Se o arquivo não couber no espaço livre, o upload falha.

{% hint style="warning" %}
Cancelar o add-on CDN remove a cota de escrita. Planeje o que fazer com os arquivos antes de cancelar.
{% endhint %}

***

## 🔗 URLs públicas

Cada arquivo fica sob o ID da sua conta:

```
https://cdn.discloud.com/{seuUserId}/{caminho/relativo}
```

Exemplos:

| Path no painel / API | URL pública                                           |
| -------------------- | ----------------------------------------------------- |
| `images/logo.png`    | `https://cdn.discloud.com/{userId}/images/logo.png`   |
| `brand/favicon.ico`  | `https://cdn.discloud.com/{userId}/brand/favicon.ico` |

Você **não** envia o `userId` no path de upload. Envie só o caminho relativo.

***

## 📁 Regras de path

| Regra     | Detalhe                                            |
| --------- | -------------------------------------------------- |
| Formato   | Relativo, **sem** `/` no início                    |
| Segmentos | Letras, números, `.`, `_`, `-`                     |
| Proibido  | `..`, `//`, espaços, acentos, caracteres especiais |
| Pastas    | No máximo **8** níveis; path ≤ **512** caracteres  |

Válidos: `logo.png`, `images/goto.png`, `a/b/c/file.webp`\
Inválidos: `/logo.png`, `../x`, `minha pasta/a.png`

***

## ⬆️ Upload

{% tabs %}
{% tab title="Arquivo ≤ 100 MB" %}
Use o upload simples no painel (ou `PUT /cdn/upload` na API).

Informe o **path** de destino e o **tamanho em bytes**. A plataforma valida a quota antes de aceitar o stream.
{% endtab %}

{% tab title="Arquivo > 100 MB" %}
Use o fluxo **multipart** (várias partes). Cada parte intermediária tem mínimo de \~5 MB; o corpo de cada request HTTP fica limitado a \~100 MB.

No painel, o fluxo grande é tratado pela interface. Na API, veja [CDN](../api-and-sdks/api-overview/cdn.md).
{% endtab %}
{% endtabs %}

{% stepper %}
{% step %}
**Contratar a cota**

Em Assinatura → Add-ons (ou a partir da própria CDN), ative o add-on **CDN** com pelo menos 50 GB.
{% endstep %}

{% step %}
**Abrir a CDN**

Painel → **CDN**. Crie pastas se quiser organizar (`images/`, `docs/`, …).
{% endstep %}

{% step %}
**Enviar o arquivo**

Faça upload para o path desejado. Copie a URL pública e use no site, bot ou app.
{% endstep %}
{% endstepper %}

***

## 🛠️ O que dá para fazer

| Ação           | Efeito                               |
| -------------- | ------------------------------------ |
| Listar         | Navega pastas e arquivos da conta    |
| Upload         | Publica o arquivo na URL da CDN      |
| Sobrescrever   | Pode substituir um path já existente |
| Criar pasta    | Cria marcador de pasta vazia         |
| Apagar arquivo | Remove um path                       |
| Apagar pasta   | Remove tudo sob um prefixo           |

***

## 🚫 O que a CDN não é

* Não é o disco das suas aplicações nem da [VPS](/broken/pages/vps-product).
* Não é Object Storage S3 privado (produto separado / desativado na compra).
* Não autentica download: a URL é pública.
* Não substitui [domínio personalizado](custom-domain.md) nem o [Edge](edge.md) do site.

***

## 🧭 Próximos passos

{% content-ref url="/broken/pages/addons-product" %}
[Broken link](/broken/pages/addons-product)
{% endcontent-ref %}

{% content-ref url="../api-and-sdks/api-overview/cdn.md" %}
[cdn.md](../api-and-sdks/api-overview/cdn.md)
{% endcontent-ref %}
