---
description: Configure seu domínio para sua aplicação hospedada na Discloud.
icon: globe
---

# Domínio Personalizado

## 🧭 Visão Geral

Você pode mapear seu próprio domínio (ex. `seudominio.com`) ou um subdomínio (ex. `dash.seudominio.com`) para uma aplicação hospedada na Discloud. A plataforma serve o tráfego através do [subdomínio Discloud](../faq/general-questions/how-to-create-a-subdomain.md) da sua aplicação usando dois registros A apontando para nossos endereços IPv4.

{% hint style="info" %}
**Platinum vs Diamond.** Com [Platinum ou superior](https://discloud.com/plans) você já hospeda sites e APIs usando o [subdomínio](../faq/general-questions/how-to-create-a-subdomain.md) que a Discloud fornece (`.discloud.app`, `.discloud.dev` e outros no futuro). O **domínio personalizado** é o recurso à parte: apontar o _seu_ domínio para a aplicação. Isso exige [Diamond ou superior](https://discloud.com/plans).
{% endhint %}

<figure><img src="../.gitbook/assets/custom-domain-flow.png" alt="Diagrama de fluxo do domínio personalizado"><figcaption></figcaption></figure>

***

## 📋 Requisitos

{% hint style="success" %}
[Plano Platinum ou superior](https://discloud.com/plans) – necessário para hospedar websites ou APIs (via subdomínio Discloud).
{% endhint %}

{% hint style="success" %}
[Plano Diamond ou superior](https://discloud.com/plans) – necessário para adicionar um **domínio personalizado** à aplicação.
{% endhint %}

{% hint style="success" %}
[Aplicação já hospedada](../getting-started/websites-and-apis.md) usando um subdomínio da Discloud (ex. `exemplo.discloud.app`)
{% endhint %}

{% hint style="success" %}
Um domínio registrado que você controla (Cloudflare, Hostinger, GoDaddy, Namecheap, etc.)
{% endhint %}

{% hint style="success" %}
Capacidade de adicionar / modificar registros A
{% endhint %}

***

## 🏗️ Adicione Seu Domínio (Painel)

{% stepper %}
{% step %}
Abra o [Painel da Discloud](https://discloud.com/dashboard) → seção [`Domínios`](https://discloud.com/dashboard/domains).
{% endstep %}

{% step %}
Clique em **+ Adicionar domínio** e digite seu domínio (ex. `seudominio.com`). Opcionalmente, especifique um subdomínio (ex. `dash`).
{% endstep %}

{% step %}
Clique em **Ver DNS** para visualizar os registros que precisa configurar.
{% endstep %}
{% endstepper %}

<div data-full-width="false"><figure><img src="../.gitbook/assets/Website-Custom-Domain.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Website-Custom-Domain-DNS-A.png" alt="Lista de registros A mostrando 75.2.96.173 e 99.83.186.151"><figcaption></figcaption></figure></div>

***

## ✅ Configurar DNS

Embora qualquer provedor de DNS funcione, abaixo estão cenários com abas para clareza.

{% tabs %}
{% tab title="Domínio Raiz" %}
**Registros**

| Tipo | Nome                      | Valor           |
| ---- | ------------------------- | --------------- |
| A    | `@` (ou raiz do provedor) | `75.2.96.173`   |
| A    | `@` (ou raiz do provedor) | `99.83.186.151` |
{% endtab %}

{% tab title="Subdomínio" %}
**Exemplo: `dash.seudominio.com`**

<table><thead><tr><th width="169">Tipo</th><th width="383">Nome</th><th>Valor</th></tr></thead><tbody><tr><td>A</td><td><code>dash</code></td><td><code>75.2.96.173</code></td></tr><tr><td>A</td><td><code>dash</code></td><td><code>99.83.186.151</code></td></tr></tbody></table>

Múltiplos subdomínios (ex. `api`, `app`) repetem este padrão independentemente.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
#### **Proxy do Cloudflare**

Se você usar **Cloudflare**, é obrigatório desabilitar o **Proxy** (certifique-se de que está definido como **DNS Only** / **Nuvem Cinza**, não a Laranja). Isso garante a emissão correta do certificado SSL.
{% endhint %}

<figure><img src="../.gitbook/assets/Cloudflare-Custom-Domain-DNS.png" alt=""><figcaption></figcaption></figure>

***

## 🔄 Reconstruir a Aplicação

Após o DNS propagar, abra a aplicação vinculada e acione a Reconstrução para que a vinculação se torne ativa.

<div data-full-width="false"><figure><img src="../.gitbook/assets/Website-Applications_Subdomain.png" alt="Lista de aplicações mostrando domínio personalizado"><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Website-Applications_Rebuild.png" alt=""><figcaption></figcaption></figure></div>

***

### 📡 **Propagação DNS**

* Mudanças de DNS normalmente se propagam em alguns minutos.
* No entanto, **valores TTL** e **cache do resolvedor** podem causar alguns atrasos.
* Para verificar as mudanças em todo o mundo, confira [dnschecker.org](https://dnschecker.org/)
* Se alguns POPs ainda exibirem registros antigos, aguarde e verifique novamente mais tarde.

<figure><img src="/broken/files/2cc3bHRnuLJuXAOUL5gJ" alt=""><figcaption></figcaption></figure>

***

## 🛡️ Controlar o tráfego com o Edge

Com o domínio ativo, você pode bloquear caminhos, colocar o site em manutenção, mexer em headers e criar redirecionamentos na borda da Discloud, antes de o pedido chegar na aplicação.

{% content-ref url="edge.md" %}
[edge.md](edge.md)
{% endcontent-ref %}
