---
description: >-
  Aprenda como diagnosticar e resolver problemas comuns com aplicações que
  falham em permanecer online na Discloud.
---

# Diagnosticando Aplicações Offline

Se sua aplicação **encerra inesperadamente** na Discloud, é importante analisar **o que pode estar causando o problema**. Este guia ajudará você a **identificar, depurar e resolver** problemas comuns relacionados a aplicações indo offline.

***

## 🛑 **Comportamentos Comuns de Aplicação e Causas**

Quando uma aplicação encerra inesperadamente, o **comportamento** pode fornecer pistas sobre a causa raiz.

{% stepper %}
{% step %}
Inicia e imediatamente encerra.

* Indica um **problema crítico** impedindo a inicialização adequada.
* Causas prováveis: **limitações de RAM, dependências ausentes, configurações incorretas ou erros no código de inicialização**.
{% endstep %}

{% step %}
Encerra durante uma ação específica.

* Acontece quando a aplicação é **acionada por um comando ou evento específico**.
* Causas prováveis: **exceções não capturadas, uso alto de recursos ou falhas de API**.
{% endstep %}
{% endstepper %}

***

## ⚠️ **Causas Potenciais e Correções**

{% hint style="warning" %}
#### **RAM Insuficiente**

Se sua aplicação **excede sua memória alocada**, ela pode ser **forçadamente encerrada**.

✔ **Monitore o uso de RAM** e otimize seu código.\
✔ Considere **aumentar a RAM** no seu arquivo [`discloud.config`](../../configurations/discloud.config/).
{% endhint %}

{% hint style="warning" %}
#### **Erros de Código e Exceções**

Exceções não tratadas ou **bugs no seu código** podem causar travamentos.

✔ Verifique os **logs** para mensagens de erro.\
✔ **Teste localmente** antes de fazer o upload na Discloud.
{% endhint %}

{% hint style="danger" %}
#### **Aplicações gratuitas offline são apagadas após 30 dias**

Uma aplicação do plano gratuito que fica **offline** permanece na sua conta por apenas **30 dias**. Depois desse prazo, ela é **apagada automaticamente**.

✔ Se não quiser perder a aplicação, coloque-a online de novo antes desse prazo.\
✔ Faça um **backup** dos arquivos se quiser guardá-los.
{% endhint %}

{% hint style="danger" %}
#### **Plano pago expirado: aplicações offline são apagadas 45 dias após o snapshot**

Se o seu plano pago **expirar** e não for renovado, a Discloud desliga as suas aplicações e mantém apenas **1 aplicação online**, com **100 MB** disponíveis, como no plano gratuito.

As aplicações que ficarem **offline** recebem um **snapshot** e permanecem na sua conta por **45 dias** depois que ele é gerado. Depois desse prazo, elas são **apagadas automaticamente**.

✔ Renove o plano antes desse prazo se não quiser perder as aplicações.\
✔ Faça um **backup** dos arquivos se quiser guardá-los.
{% endhint %}

***

## 🛠️ **Depuração Passo a Passo**

📌 **Um erro comum que desenvolvedores cometem é dizer:** _"Funciona na minha máquina mas não na Discloud."_

Lembre-se, **a Discloud opera em um ambiente Linux**. Sua aplicação deve ser **adaptada para rodar no ambiente alvo**, não apenas na sua máquina local.

***

## ⚡ **Corrigindo Aplicações Que Encerram Imediatamente**

Se sua aplicação **inicia e imediatamente encerra**, geralmente é devido a:

{% stepper %}
{% step %}
RAM insuficiente.

* Se a aplicação usa mais memória do que alocada, a Discloud **encerra forçadamente**.
* Verifique seu **uso de RAM** e **otimize operações intensivas em memória**.
{% endstep %}

{% step %}
Erros durante a inicialização.

* Bugs na **sequência de inicialização** podem **impedir a app de rodar adequadamente**.
* Verifique **dependências ausentes**, **configurações incorretas** ou **erros não capturados** na lógica de inicialização.
{% endstep %}
{% endstepper %}

***

## ❗ **Corrigindo Aplicações Que Encerram Durante uma Ação Específica**

Se sua aplicação **para de rodar quando um evento ou ação específica é acionada**, siga estes passos de depuração:

{% stepper %}
{% step %}
Verifique os logs.

* Logs fornecem insights valiosos sobre o que causou o travamento.
* Procure **mensagens de erro** relacionadas a essa ação.
{% endstep %}

{% step %}
Revise o código que trata essa ação.

* Verifique **exceções não tratadas**, **respostas de API inválidas** ou **erros de banco de dados**.
* Garanta que o **tratamento de erro** adequado esteja em vigor.
{% endstep %}

{% step %}
Monitore o uso de recursos.

* Algumas ações **requerem mais RAM** (ex. tocar música, processar imagens).
* Se a ação for intensiva em recursos, **considere aumentar a alocação de RAM**.
{% endstep %}
{% endstepper %}

***

## 🎵 **Exemplos Comuns (Aplicações Discord)**

{% hint style="info" %}
#### **Bots de Música**

Se o bot **encerra ao tocar música**, pode ser devido a:\
✔ **Uso alto de RAM** → Otimize processamento de áudio.\
✔ **`ffmpeg` ausente** → Adicione `ffmpeg` nas dependências [`APT`](../../configurations/discloud.config/apt.md).\
✔ **Limites de taxa de API** → Verifique se está atingindo limites com o provedor de música.
{% endhint %}

{% hint style="info" %}
#### **Bots de Geração de Imagens**

* **Gerar imagens consome memória**.
* Garanta que seu bot tenha **RAM suficiente** e otimize o código de processamento de imagens.
{% endhint %}

***

## 🛰️ **Verifique o Status da Discloud**

Se nenhuma das soluções acima resolver o problema, verifique a página de status da Discloud ou o canal Discord para quaisquer problemas relatados em todo o sistema. Problemas temporários de infraestrutura podem impactar a disponibilidade da sua aplicação.

* [**Página de Status da Discloud**](https://status.discloud.app/)
* [**Canal Discord da Discloud**](https://discord.com/channels/584490943034425391/694744729731989605)
