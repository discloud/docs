---
description: >-
  Introdução rápida às VPS: primeiro compre a cota (Comprar recursos), depois
  crie a máquina (Nova VPS).
icon: server
tags:
  - novo
---

# VPS

## 🖥️ Resumo

A VPS é um Linux na nuvem com **root** por SSH. Ela **não** usa a RAM do plano de bots e sites.

**Ordem obrigatória:**

1. **Comprar recursos** — cota de RAM + SSD (add-on).
2. **Nova VPS** — criar a máquina só **depois** que a cota estiver paga e com GB livres.

Comprar cota **não** liga servidor. Criar máquina **não** abre plano novo: só usa a cota.

| Passo            | Botão no painel      | Onde                |
| ---------------- | -------------------- | ------------------- |
| 1. Comprar cota  | **Comprar recursos** | Dashboard → **VPS** |
| 2. Criar máquina | **Nova VPS**         | Dashboard → **VPS** |
| 3. Acessar       | SSH (`root` + senha) | Overview da máquina |

{% hint style="info" %}
Mínimos usuais: **4 GB** RAM e **50 GB** SSD. Passo a passo completo (checkout, campos, vCPU, status, cancelar cota): página do produto.
{% endhint %}

{% hint style="danger" %}
Cancelar a cota VPS **destrói todas as máquinas** da conta.
{% endhint %}

***

## 📖 Documentação completa

{% content-ref url="../platform-features/vps.md" %}
[vps.md](../platform-features/vps.md)
{% endcontent-ref %}

{% content-ref url="../platform-features/addons.md" %}
[addons.md](../platform-features/addons.md)
{% endcontent-ref %}
