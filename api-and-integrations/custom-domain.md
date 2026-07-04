---
description: Configure seu domínio para sua aplicação hospedada na Discloud.
icon: globe
---

# Domínio Personalizado

## 🧭 Visão Geral

Você pode mapear seu próprio domínio (ex. `yourdomain.com`) ou um subdomínio (ex. `dash.yourdomain.com`) para uma aplicação hospedada na Discloud. A plataforma serve o tráfego através do [subdomínio Discloud](../faq/general-questions/how-to-create-a-subdomain.md) da sua aplicação usando dois registros A apontando para nossos endereços IPv4 e valida a propriedade via registros TXT.

<figure><img src="../.gitbook/assets/custom-domain-flow.png" alt="Diagrama de fluxo do domínio personalizado"><figcaption></figcaption></figure>

***

## 📋 Requisitos

{% hint style="success" %}
[Plano Diamante ou superior](https://discloud.com/plans) é necessário para hospedar websites ou APIs.
{% endhint %}

{% hint style="success" %}
[Aplicação já hospedada](../how-to-host/websites-and-apis.md) usando um subdomínio da Discloud (ex. `exemplo.discloud.app`)
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
Digite seu domínio (ex. `seudominio.com`). Opcionalmente, especifique um subdomínio (ex. `dash`).
{% endstep %}

{% step %}
Clique em **+ Adicionar domínio**, insira seu domínio e depois clique em **Ver DNS** para visualizar os registros que precisa configurar.
{% endstep %}
{% endstepper %}

<div data-full-width="false"><figure><img src="../.gitbook/assets/Website-Custom-Domain.png" alt=""><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Website-Custom-Domain-DNS-A.png" alt="Lista de registros A mostrando 75.2.96.173 e 99.83.186.151"><figcaption></figcaption></figure></div>

***

## ✅ Verificar e Configurar DNS

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

Após o DNS resolver e os tokens validarem, abra a aplicação vinculada e acione a Reconstrução para que a vinculação se torne ativa.

<div data-full-width="false"><figure><img src="../.gitbook/assets/Website-Applications_Subdomain.png" alt="Lista de aplicações mostrando domínio personalizado"><figcaption></figcaption></figure> <figure><img src="../.gitbook/assets/Website-Applications_Rebuild.png" alt=""><figcaption></figcaption></figure></div>

***

### 📡 **Propagação DNS**

* Mudanças de DNS normalmente se propagam em alguns minutos.
* No entanto, **valores TTL** e **cache do resolvedor** podem causar alguns atrasos.
* Para verificar as mudanças em todo o mundo, confira [dnschecker.org](https://dnschecker.org/)
* Se alguns POPs ainda exibirem registros antigos, aguarde e verifique novamente mais tarde.

<figure><img src="../.gitbook/assets/dns-check-propagation.png" alt=""><figcaption></figcaption></figure>
