---
description: Guia completo para hospedar aplicações Java na Discloud.
icon: java
---

# Java

## 📁 **Preparando os Arquivos do Seu Projeto**

Antes do deploy, **seu projeto deve ser** [**compilado em um arquivo JAR executável**](../../faq/general-questions/how-to-build-and-package-a-java-application.md). Ao comprimir seu projeto, certifique-se de que **o arquivo `.jar` seja colocado na** [**raiz**](../../faq/general-questions/what-is-the-root-of-the-project.md) **do** [**arquivo `.zip`**](../../faq/general-questions/em-andamento-como-comprimir.md)**.**

#### ❌ **Arquivos a Excluir**

Certifique-se de que os seguintes arquivos e diretórios **não** sejam incluídos no seu [`.zip`](../../faq/general-questions/em-andamento-como-comprimir.md):

```diff
- package-lock.json
- node_modules/
- .cache/
- .git/
```

📌 **Use um arquivo** [**`.discloudignore`**](../../configurations/.discloudignore.md) **para excluir automaticamente esses arquivos.**

🔗 **Precisa de ajuda com compilação?** Verifique a FAQ sobre [**Como Construir e Empacotar uma Aplicação Java?**](../../faq/general-questions/how-to-build-and-package-a-java-application.md)

***

## 📦 **Compilando Sua Aplicação Java**

Para **fazer deploy da sua aplicação Java**, ela deve ser compilada em um **arquivo JAR executável**.

{% tabs %}
{% tab title="Maven" %}
📄 **Documentação Oficial do Maven** → [https://maven.apache.org/guides/index.html](https://maven.apache.org/guides/index.html)

```bash
mvn clean package
```
{% endtab %}

{% tab title="Gradle" %}
📄 **Documentação Oficial do Gradle** → [https://docs.gradle.org/current/userguide/userguide.html](https://docs.gradle.org/current/userguide/userguide.html)

```bash
gradle clean build
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### **Recomendação**

Renomeie seu arquivo JAR para um nome simples como `app.jar` para evitar problemas com caracteres especiais.​
{% endhint %}

***

## 📝 **Configurando o Arquivo Principal**

O parâmetro `MAIN` no seu arquivo [`discloud.config`](https://github.com/discloud/docs/blob/portuguese/configurations/discloud.config) deve apontar para o seu arquivo JAR executável. Por exemplo:

```ini
MAIN=app.jar
```

Certifique-se de que `app.jar` corresponda ao nome do seu arquivo JAR compilado.​

**Nota:** Para informações detalhadas sobre configurar o arquivo principal, consulte a FAQ da Discloud sobre o arquivo principal.

***

## ✍️ **Fazendo Deploy da Sua Aplicação**

Uma vez que seu projeto esteja **configurado e comprimido**, você pode escolher um dos seguintes **métodos de deploy** na Discloud:

<table data-card-size="large" data-view="cards"><thead><tr><th data-card-target data-type="content-ref"></th><th align="center"></th><th data-hidden></th><th data-hidden></th><th data-hidden></th></tr></thead><tbody><tr><td><a href="../../how-to-host-using/dashboard.md">dashboard.md</a></td><td align="center">Faça upload e gerencie sua aplicação via interface web.</td><td></td><td></td><td></td></tr><tr><td><a href="../../how-to-host-using/discord-bot.md">discord-bot.md</a></td><td align="center">Faça deploy diretamente através dos comandos do bot Discord da Discloud.</td><td></td><td></td><td></td></tr><tr><td><a href="../../how-to-host-using/visual-studio-code.md">visual-studio-code.md</a></td><td align="center">Integre com VS Code para gerenciamento contínuo de projetos.</td><td></td><td></td><td></td></tr><tr><td><a href="../../how-to-host-using/cli.md">cli.md</a></td><td align="center">Use a interface de linha de comando para deploy rápido e eficiente.</td><td></td><td></td><td></td></tr></tbody></table>
