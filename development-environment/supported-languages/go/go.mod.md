---
description: >-
  Aprenda como gerar e configurar o arquivo go.mod para gerenciar módulos e
  dependências para aplicações Go na Discloud.
---

# go.mod

## 🗂️ O que é `go.mod`?

`go.mod` define o caminho do seu módulo, a versão da toolchain Go (no formato `major.minor`), e as dependências diretas necessárias pelo seu projeto. A Discloud usa ele (e o `go.sum` acompanhante) para baixar e verificar módulos antes de construir sua aplicação.

***

## 🛠️ Criando um Novo Módulo

{% stepper %}
{% step %}
Inicialize um módulo no diretório atual:

```bash
go mod init github.com/you/yourapp
```
{% endstep %}

{% step %}
Adicione (ou atualize) dependências automaticamente referenciando-as no código e organizando:

```bash
go mod tidy
```

Isso cria `go.sum` (não deve estar vazio) com linhas de checksum.
{% endstep %}

{% step %}
Adicione uma dependência específica explicitamente:

```bash
go get github.com/go-chi/chi/v5
```

Então organize novamente se necessário:

```bash
go mod tidy
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Precisa do Go localmente? Veja o [guia do ambiente local](../../local-environment/golang.md).
{% endhint %}

***

## 🧩 Exemplo Mínimo

{% code title="go.mod" %}
```go
module github.com/you/yourapp

go 1.22
```
{% endcode %}

{% hint style="warning" %}
A versão do Go **DEVE** estar no formato `major.minor` (ex.: `1.22`). **NÃO** use patch: `1.22.3`.
{% endhint %}

***

## 📦 Adicionando Dependências

Para adicionar uma nova dependência, ou:

{% stepper %}
{% step %}
Importe-a no seu arquivo fonte e execute `go mod tidy`, ou
{% endstep %}

{% step %}
Execute `go get module/path@version` diretamente.

**Exemplo: adicionar Chi router**

```bash
go get github.com/go-chi/chi/v5
```

Snippet resultante do `go.mod`:

```go
require (
	github.com/go-chi/chi/v5 v5.0.12 // versão exemplo
)
```

> As versões são resolvidas semanticamente pelo sistema proxy/módulo.
{% endstep %}
{% endstepper %}

***

## 🔒 Integridade do `go.sum`

`go.sum` contém hashes criptográficos de cada versão de módulo necessária (direta & indireta) para garantir builds reprodutíveis. Ele **deve ser commitado** junto com `go.mod`.

Regenere / atualize-o a qualquer momento:

```bash
go mod tidy
```

***

## 🧪 Exemplos de Tipos de Aplicação

Exemplos em abas para cenários comuns:

{% tabs %}
{% tab title="🤖 Bot Discord" %}
{% code title="go.mod" %}
```go
module github.com/you/discordbot

go 1.22

require (
    github.com/bwmarrin/discordgo v0.27.1 // exemplo
)
```
{% endcode %}
{% endtab %}

{% tab title="🌐 Website / API" %}
{% code title="go.mod" %}
```go
module github.com/you/webapp

go 1.22

require (
    github.com/go-chi/chi/v5 v5.0.12
)
```
{% endcode %}

Requisitos:

* Seu servidor HTTP deve escutar na porta `8080`.
{% endtab %}

{% tab title="📦 Apenas Stdlib Mínimo" %}
{% code title="go.mod" %}
```go
module github.com/you/stdlibonly

go 1.22
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

## 🧰 Referência de Comandos Comuns

```bash
# Execute sua aplicação diretamente
go run .

# Construa um binário
go build -o app

# Liste todos os módulos (diretos+indiretos)
go list -m all

# Mostre o gráfico de dependências
go mod graph
```
