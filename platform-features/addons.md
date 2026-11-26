---
description: >-
  Add-ons são cobranças à parte do plano: cota extra que você contrata quando
  precisa, sem trocar de plano.
tags:
  - novo
---

# Add-ons

## ➕ O que é um add-on?

Um **add-on** na Discloud é um recurso **aditivo** e **independente do plano** (Free, Platinum, Diamond, …).

* O **plano** define o que a conta pode fazer com bots, sites, RAM de apps, bancos gerenciados, etc.
* O **add-on** é uma assinatura à parte: você escolhe quantos GB quer e paga por isso, em cima do plano que já tem.

Trocar de plano **não** inclui automaticamente a CDN nem a cota de VPS. Contratar um add-on **não** muda o plano.

{% hint style="info" %}
Hoje os add-ons compráveis são a **CDN** (armazenamento público) e a **cota VPS** (RAM + SSD para máquinas). Outros tipos podem existir no sistema, mas a compra na interface segue o que o catálogo liberar.
{% endhint %}

***

## 📍 Onde fica

[Painel da Discloud](https://discloud.com/dashboard) → **Assinatura** / **Billing** → seção **Add-ons**.

* A **CDN** aparece no grid de add-ons para comprar e ajustar GB.
* A **cota VPS** (RAM + SSD) é comprada e ajustada na área **VPS → Comprar recursos** (os dois entram juntos no checkout).

***

## 📦 Add-ons disponíveis

### CDN

|                 |                                                          |
| --------------- | -------------------------------------------------------- |
| Para que serve  | Guardar e servir arquivos públicos em `cdn.discloud.com` |
| Unidade         | GB armazenados                                           |
| Mínimo / degrau | 50 GB / de 50 em 50 GB                                   |
| Banda           | Ilimitada                                                |

Detalhes de uso: [CDN](/broken/pages/cdn-product).

### Cota VPS (RAM + SSD)

|                 |                                                                              |
| --------------- | ---------------------------------------------------------------------------- |
| Para que serve  | Pool de memória e disco para criar [máquinas VPS](/broken/pages/vps-product) |
| Unidade         | GB de RAM e GB de SSD NVMe                                                   |
| Mínimo / degrau | RAM 4 GB (passo 4) · SSD 50 GB (passo 50)                                    |
| Cobrança        | Os dois são contratados **juntos**                                           |

Comprar a cota **não** cria a máquina. Criar a máquina **não** abre um plano novo: só reserva GB que você já tem no pool.

{% hint style="danger" %}
Cancelar a assinatura da cota VPS **destrói todas as máquinas VPS** da conta.
{% endhint %}

Detalhes: [VPS](/broken/pages/vps-product).

***

## 💳 Como funciona a cobrança

| Conceito     | Plano                              | Add-on                                          |
| ------------ | ---------------------------------- | ----------------------------------------------- |
| O que limita | Apps, sites, bancos, perks do tier | Só a cota daquele produto                       |
| Assinatura   | Uma (plano)                        | Outra (ou itens no mesmo checkout do add-on)    |
| Aumentar     | Upgrade de plano                   | Aumentar quantity (GB)                          |
| Reduzir      | Downgrade (regras do plano)        | Só até o que já está **em uso**                 |
| Cancelar     | Afeta apps/sites conforme regras   | Afeta só aquele add-on (na VPS: destrói as VMs) |

Pró-rata e renovação seguem o fluxo de Assinatura do painel (cartão, PIX, etc., conforme disponível na conta).

***

## 🧭 Plano vs add-on — exemplos

| Situação                                      | O que fazer                                                    |
| --------------------------------------------- | -------------------------------------------------------------- |
| Quer hospedar um site no subdomínio Discloud  | Plano **Platinum+** — não é add-on                             |
| Quer domínio próprio no site                  | Plano **Diamond+** + [domínio personalizado](custom-domain.md) |
| Quer servir imagens estáticas com URL pública | Add-on **CDN**                                                 |
| Quer um Linux com root por SSH                | Add-on **cota VPS** + criar a máquina                          |

***

## 🚫 O que add-on não faz

* Não substitui o plano (não libera sites, bancos gerenciados, Edge, etc. sozinho).
* Não mistura cota: GB da CDN não viram RAM de bot; RAM da VPS não vira RAM de app.
* Não é “crédito genérico”: cada add-on tem tipo e regras próprias.
