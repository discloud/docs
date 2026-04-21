---
description: >-
  Aprenda tudo sobre o arquivo de configuração para hospedar aplicações na
  Discloud.
icon: gear
---

# discloud.config

## 📄 O que é `discloud.config` e para que serve?

É um arquivo de configuração que simplifica o processo de upload das suas aplicações na Discloud. Com este arquivo, você pode configurar facilmente as informações para cada aplicação que você faz upload no serviço de hospedagem.

***

## 📂 **Localização do Arquivo `discloud.config`**

**✅ Localização Correta**

O arquivo `discloud.config` <mark style="color:yellow;">**deve estar na**</mark> [<mark style="color:yellow;">**raiz**</mark> <mark style="color:yellow;">do seu projeto</mark>](../../faq/general-questions/what-is-the-root-of-the-project.md).

```bash
your-project/           # ← DIRETÓRIO RAIZ
├── discloud.config     # ✅ OBRIGATÓRIO AQUI
├── package.json        # Arquivo raiz de exemplo
├── src/                # Pasta do código fonte
│   └── index.js        # Arquivo principal da aplicação
├── .gitignore          # Arquivos de configuração
└── README.md           # Documentação
```

**❌ Localizações Inválidas**

Essas localizações causarão falhas no upload:

```bash
your-project/
├── src/
│   └── discloud.config   # ❌ ERRO DE SUBPASTA
├── config/
│   └── discloud.config   # ❌ ERRO DE SUBPASTA
└── .github/
    └── discloud.config   # ❌ ERRO DE PASTA OCULTA
```

***

## 🛠️ Opções de configuração

Veja abaixo todas as opções de configuração para o arquivo `discloud.config`. [Clique aqui para ver alguns exemplos de diferentes aplicações](./#exemplos-de-arquivos-discloud.config).

{% tabs %}
{% tab title="📑 Informações" %}
Defina informações para sua aplicação na plataforma de hospedagem, como `NAME` e `AVATAR`. Isso permite que você identifique facilmente sua aplicação no painel ou na extensão do Visual Studio Code. Veja:

<pre class="language-properties" data-title="discloud.config"><code class="lang-properties">NAME=MyApp
AVATAR=https://i.imgur.com/bWhx7OT.png
<a data-footnote-ref href="#user-content-fn-1"># ...</a>
</code></pre>

* `NAME` - determina o nome da sua aplicação na plataforma de hospedagem.
* `AVATAR` - usa a URL da imagem como avatar para sua aplicação na plataforma de hospedagem.
{% endtab %}

{% tab title="🖥️ Aplicações" %}
Para que sua aplicação inicie corretamente na hospedagem, você precisa definir seu tipo usando a opção `TYPE`, definir o ponto de entrada com a opção `MAIN`, especificar a `RAM` máxima que pode usar com a opção `RAM`, e indicar a [versão da linguagem](versions.md) com a opção `VERSION`. Veja abaixo:

<pre class="language-properties" data-title="discloud.config"><code class="lang-properties"><a data-footnote-ref href="#user-content-fn-1"># ...</a>
TYPE=bot
MAIN=index.js
RAM=100
VERSION=latest
</code></pre>

* `TYPE` - pode ter dois valores: **bot** ou **site**.
* `MAIN` - deve conter o caminho para o [arquivo principal](../../faq/general-questions/what-is-the-main-file.md) da sua aplicação.
* `RAM` - determina a quantidade máxima de RAM disponível para a aplicação.
* `VERSION` - especifica a [versão da linguagem](versions.md) do seu projeto.

{% hint style="info" %}
Se o `TYPE` estiver definido como **site**, você também deve definir a opção `ID` com seu subdomínio. [Veja mais aqui.](../../faq/general-questions/how-to-create-a-subdomain.md)
{% endhint %}

<pre class="language-properties" data-title="discloud.config"><code class="lang-properties"><strong>TYPE=site
</strong><strong>ID=your-subdomain
</strong>MAIN=index.js
RAM=100
VERSION=latest
<a data-footnote-ref href="#user-content-fn-1"># ...</a>
</code></pre>

{% hint style="warning" %}
Para hospedar um **site**, é necessário um mínimo de **512MB de RAM**, junto com um [**Plano Platinum**](https://discloud.com/plans).
{% endhint %}
{% endtab %}

{% tab title="🧩 Recursos" %}
Dependendo da linguagem de programação do seu projeto, você pode definir quais comandos serão executados para o processo de build e o comando para iniciar a aplicação usando as propriedades `BUILD` e `START`.

Para habilitar o reinício automático em caso de falhas, defina a opção `AUTORESTART` como **true** (disponível apenas para [**Plano Platinum**](https://discloud.com/plans) ou superior).

Você pode instalar [pacotes](apt.md) usando a opção `APT`.

<pre class="language-properties" data-title="discloud.config"><code class="lang-properties"><a data-footnote-ref href="#user-content-fn-1"># ...</a>
BUILD=npm run build
START=npm run start
AUTORESTART=true
APT=tools
</code></pre>

* `BUILD` - define o comando ou script para compilar o projeto.
* `START` - define o comando ou script para iniciar o projeto.
* `AUTORESTART` - garante que a aplicação reinicie automaticamente em caso de falha.
* `APT` - permite especificar uma lista de [pacotes](apt.md) a serem instalados.
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
#### **Opções obrigatórias no seu `discloud.config`**

**Apenas um campo é obrigatório**:

```ini
MAIN=index.js
```

**Todos os outros campos são opcionais** e usarão padrões inteligentes se omitidos:

* `TYPE` padrão é `bot`
* `RAM` padrão é `100` (MB)
* `VERSION` padrão é `latest`
{% endhint %}

***

## 🪅 Exemplos de arquivos **`discloud.config`**

> Veja abaixo exemplos de arquivos **discloud.config** para [🤖 Bots Discord](./#bots-discord) e [🌐 Sites e APIs](./#sites-e-apis).

{% tabs %}
{% tab title="🤖 Bots Discord" %}
{% tabs %}
{% tab title="🟨Bot JS Simples" %}
Bot Discord feito em JavaScript onde o ponto de entrada é o arquivo **index.js** na raiz do projeto.

{% code title="discloud.config" %}
```properties
NAME=Lorito
TYPE=bot
MAIN=index.js
RAM=100
VERSION=latest
```
{% endcode %}
{% endtab %}

{% tab title="🟦 Bot com TS" %}
Bot feito em TypeScript onde o ponto de entrada é o arquivo **index** dentro da pasta **build**. A aplicação iniciará executando o script **start** do arquivo **package.json**.

{% code title="discloud.config" %}
```properties
NAME=Mee8
TYPE=bot
MAIN=build/index.ts
START=npm run start
BUILD=npm run build
RAM=200
VERSION=latest
```
{% endcode %}
{% endtab %}

{% tab title="🐍 Bot com PY" %}
Bot Discord feito em Python onde o ponto de entrada é o arquivo **main.py** na raiz do projeto.

{% code title="discloud.config" %}
```properties
NAME=Dyna
TYPE=bot
MAIN=main.py
RAM=300
VERSION=latest
```
{% endcode %}
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🌐 Sites e APIs" %}
{% tabs %}
{% tab title="📄 Site HTML simples" %}
Site simples com HTML puro, usando o subdomínio **"friendbook"** da conta do usuário.

{% code title="discloud.config" %}
```properties
NAME=Friendbook
TYPE=site
MAIN=index.html
RAM=512
VERSION=latest
ID=friendbook
```
{% endcode %}
{% endtab %}

{% tab title="🟢 API Web com Express" %}
API Web construída com **Express.js**, onde o arquivo de entrada é **index.js** dentro da pasta **server**. A aplicação iniciará executando o script **start** do arquivo **package.json**.

{% code title="discloud.config" %}
```properties
NAME=Crud cinema
TYPE=site
MAIN=server/index.js
START=npm run start
RAM=512
VERSION=latest
ID=moviemark
```
{% endcode %}
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## ⚙️ **Opções de configuração**

O arquivo `discloud.config` contém configurações essenciais para sua aplicação Discloud. Abaixo estão as **opções de configuração disponíveis** junto com seus respectivos limites e descrições.

<table><thead><tr><th width="147" align="center">Opção</th><th width="258" align="center">Limite / Valores</th><th align="center">Descrição</th></tr></thead><tbody><tr><td align="center"><strong>NAME</strong></td><td align="center"><code>1 - 30 caracteres</code></td><td align="center">O nome da sua aplicação (usado para fins de exibição).</td></tr><tr><td align="center"><strong>AVATAR</strong></td><td align="center"><code>URL da imagem (.gif, .jpeg, .jpg, .png)</code></td><td align="center">Uma URL para o avatar da aplicação. Formatos suportados: <strong>GIF, JPEG, JPG, PNG</strong>.</td></tr><tr><td align="center"><strong>TYPE</strong></td><td align="center"><code>bot / site</code></td><td align="center">Define se a aplicação é um <strong>bot</strong> ou um <strong>site</strong>.</td></tr><tr><td align="center"><strong>MAIN</strong></td><td align="center"><code>Caminho relativo do arquivo</code></td><td align="center">Especifica o <strong>arquivo principal</strong> que deve ser executado na pasta do projeto.</td></tr><tr><td align="center"><strong>RAM</strong></td><td align="center"><code>100 - 32000 MB</code></td><td align="center">A <strong>quantidade de RAM</strong> alocada para a aplicação (<strong>varia por</strong> <a href="https://discloud.com/plans"><strong>plano</strong></a>).</td></tr><tr><td align="center"><strong>VERSION</strong></td><td align="center"><code>latest / current / suja / specific</code></td><td align="center">Define as opções de <a href="versions.md"><strong>versionamento</strong></a> para o ambiente e dependências.</td></tr><tr><td align="center"><strong>ID</strong></td><td align="center"><code>Subdomínios definidos pelo usuário</code></td><td align="center">Subdomínio personalizado para sua aplicação (<a href="/broken/pages/RRMHVrAsVQMAN5Hsmrz8">apenas para sites</a>).</td></tr><tr><td align="center"><strong>BUILD</strong></td><td align="center"><em>(Comandos de build personalizados)</em></td><td align="center">Se especificado, define <strong>comandos para executar antes do início da aplicação</strong> (ex.: instalar dependências).</td></tr><tr><td align="center"><strong>START</strong></td><td align="center"><em>(Comando de início personalizado)</em></td><td align="center">Substitui o comando de início padrão para lançar a aplicação.</td></tr><tr><td align="center"><strong>AUTORESTART</strong></td><td align="center"><code>true / false</code></td><td align="center">Determina se o app deve <strong>reiniciar automaticamente</strong> se travar.</td></tr><tr><td align="center"><strong>VLAN</strong></td><td align="center"><code>true / false</code></td><td align="center">Habilita <strong>Virtual LAN (VLAN)</strong> para rede interna entre aplicações.</td></tr><tr><td align="center"><strong>HOSTNAME</strong></td><td align="center"><em>(Hostname personalizado)</em></td><td align="center">Especifica um hostname personalizado para a aplicação.</td></tr><tr><td align="center"><strong>APT</strong></td><td align="center"><em>(Lista de pacotes)</em></td><td align="center">Instala <strong>dependências Linux adicionais</strong> necessárias pelo seu app. <a href="apt.md"><strong>Veja pacotes disponíveis</strong></a>.</td></tr></tbody></table>

[^1]: **Nota:** Os **`...`** apenas indicam a continuação de outras opções anteriores ou subsequentes que não são relevantes para mencionar nesta página.
