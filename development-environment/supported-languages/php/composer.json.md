---
description: >-
  Entenda e configure composer.json para que a Discloud possa instalar suas
  dependências PHP automaticamente.
---

# composer.json

## 🗂 O que é `composer.json`?

`composer.json` declara os metadados do seu projeto, pacotes necessários, regras de autoload e scripts opcionais. Quando presente na raiz do arquivo que você faz upload, a Discloud instala as dependências definidas dentro usando o Composer.

***

## 🛠 Criando `composer.json`

{% stepper %}
{% step %}
Gere interativamente:

```bash
composer init
```
{% endstep %}

{% step %}
Ou crie um arquivo mínimo manualmente:

```json
{
  "name": "example/app",
  "type": "project",
  "require": {
    "guzzlehttp/guzzle": "^7.9"
  },
  "autoload": {
    "psr-4": { "App\\": "src/" }
  }
}
```
{% endstep %}

{% step %}
Então instale:

```bash
composer install
```
{% endstep %}
{% endstepper %}

***

## 📦 Adicionando / Atualizando Dependências

Instale novo pacote:

```bash
composer require ramsey/uuid
```

Atualize um pacote:

```bash
composer update ramsey/uuid
```

Atualize todos (pode alterar versões amplamente):

```bash
composer update
```

***

## 📄 Arquivo de Lock (`composer.lock`)

Commite `composer.lock` para que os deploys reproduzam as versões exatas das dependências. Se ausente, as versões mais recentes correspondentes são resolvidas durante a instalação.

***

## 🧰 Referência de Comandos Comuns

```bash
# Inicializar projeto
composer init

# Instalar deps
composer install

# Remover pacote
composer remove vendor/pkg

# Otimizar autoload
composer dump-autoload --optimize

# Executar script
composer run-script <name>

# Mostrar desatualizados
composer outdated
```
