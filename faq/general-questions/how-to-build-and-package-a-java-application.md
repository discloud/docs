---
description: >-
  Entenda como compilar e empacotar seu projeto Java em um arquivo JAR pronto
  para hospedar usando Maven ou Gradle.
---

# Como construir e empacotar uma aplicação Java?

## 📌 **Por Que Preciso Construir Minha Aplicação Java?**

Discloud **não compila projetos Java** automaticamente.

Você deve:\
✔ **Compilar seu código** em arquivos `.class`.\
✔ **Empacotar tudo em um único arquivo `.jar`** (incluindo dependências).\
✔ **Garantir que o arquivo `META-INF/MANIFEST.MF`** defina corretamente a **Main-Class**.

***

## 🔧 **Escolhendo uma Ferramenta de Construção**

<table><thead><tr><th width="112">Ferramenta de Construção</th><th width="367">Melhor Para</th><th>Arquivos Necessários</th></tr></thead><tbody><tr><td><strong>Maven</strong></td><td>Grandes projetos, aplicativos com muitas dependências</td><td><code>pom.xml</code></td></tr><tr><td><strong>Gradle</strong></td><td>Projetos modernos com scripts de construção flexíveis</td><td><code>build.gradle</code> ou <code>build.gradle.kts</code></td></tr></tbody></table>

***

## 📦 **Construindo Sua Aplicação Java**

{% tabs %}
{% tab title="Maven" %}
[Apache Maven](https://maven.apache.org/guides/index.html) é uma ferramenta de automação de construção amplamente usada que gerencia construções de projetos, dependências e documentação usando um Modelo de Objeto de Projeto (POM).​

{% stepper %}
{% step %}
Adicione o Plugin do Compilador Maven.

Garanta que seu `pom.xml` inclua o **Plugin do Compilador Maven** para especificar a versão do Java para compilação. Isso evita problemas de compatibilidade ao executar o projeto.

{% code title="pom.xml" %}
```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <version>3.13.0</version>
  <configuration>
    <source>17</source>
    <target>17</target>
  </configuration>
</plugin>
```
{% endcode %}

{% hint style="info" %}
* Defina `<source>` e `<target>` para a **versão do Java** necessária para seu projeto.
{% endhint %}
{% endstep %}

{% step %}
Especifique a Classe Principal.

Para tornar sua aplicação executável, você precisa especificar o ponto de entrada (método `main`). Isso é feito usando o **Plugin Maven Shade**, que também garante que todas as dependências sejam agrupadas dentro de um **único arquivo JAR**.

{% code title="pom.xml" %}
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-shade-plugin</artifactId>
      <version>3.2.4</version>
      <executions>
        <execution>
          <phase>package</phase>
          <goals>
            <goal>shade</goal>
          </goals>
          <configuration>
            <transformers>
              <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                <!-- NOTA: Substitua pelo nome totalmente qualificado da classe principal do seu projeto -->
                <mainClass>com.project.example.Main</mainClass>
              </transformer>
            </transformers>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```
{% endcode %}

{% hint style="info" %}
* Substitua `com.project.example.Main` pelo nome **totalmente qualificado** real da sua classe `Main`.
* Garanta que a classe `Main` contenha um método `public static void main(String[] args)` válido.
{% endhint %}
{% endstep %}

{% step %}
Construa o Projeto.

Execute o seguinte comando para **limpar** construções antigas e gerar os novos arquivos JAR:

```bash
mvn clean package
```

Após executar `mvn package`, o Maven criará **dois** arquivos JAR diferentes dentro do diretório `target/`:

{% stepper %}
{% step %}
JAR Padrão (JAR Original do Projeto).

📌 **Nome do arquivo:** `original-<artifactId>-<version>.jar`\
📌 **Exemplo:** `original-com.maven.discordbot-0.0.1-SNAPSHOT.jar`\
📌 **Conteúdo:**

* Apenas **o código compilado do seu projeto**.
* **NÃO inclui dependências**.

{% hint style="danger" %}
**NÃO use este arquivo para execução** a menos que as dependências sejam tratadas separadamente.
{% endhint %}
{% endstep %}

{% step %}
JAR Gordo (JAR Sombreado com Dependências).

📌 **Nome do arquivo:** `<artifactId>-<version>.jar`\
📌 **Exemplo:** `com.maven.discordbot-0.0.1-SNAPSHOT.jar`\
📌 **Conteúdo:**

* Seu **código de aplicação compilado**.
* **Todas as dependências incluídas** (JDA, Apache Commons, etc.).
* **Arquivo de manifesto (`MANIFEST.MF`) com a entrada `Main-Class`**.

{% hint style="success" %}
**Use este arquivo para execução e upload.**
{% endhint %}
{% endstep %}
{% endstepper %}
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Gradle" %}
[Gradle](https://gradle.org/) é uma ferramenta flexível de automação de construção que usa uma DSL baseada em Groovy ou Kotlin para definir o processo de construção.​

{% stepper %}
{% step %}
Aplique o Plugin Java.

Garanta que seu `build.gradle` (Groovy) ou `build.gradle.kts` (Kotlin) aplique o **plugin Java**:

{% tabs %}
{% tab title="Groovy" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id 'java'
    id 'com.gradleup.shadow' version '8.3.6' // Plugin Shadow para Fat JAR
}
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code title="build.gradle.kts" %}
```kotlin
plugins {
    java
    id("com.gradleup.shadow") version "8.3.6"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
{% endstep %}

{% step %}
Especifique a Classe Principal.

Para tornar a aplicação executável, defina o **ponto de entrada (método `main`)** dentro do **manifesto JAR**.

{% tabs %}
{% tab title="Groovy" %}
{% code title="build.gradle" %}
```groovy
shadowJar {
    archiveClassifier.set('all')
    manifest {
        attributes(
            'Main-Class': 'com.project.Main' // Substitua pela sua classe principal real
        )
    }
}

tasks.build.dependsOn shadowJar // Garantir que o shadowJar seja executado ao compilar
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code title="build.gradle.kts" %}
```kotlin
import com.github.jengelman.gradle.plugins.shadow.tasks.ShadowJar

tasks.withType<ShadowJar> {
    archiveClassifier.set("all")
    manifest {
        attributes(mapOf("Main-Class" to "com.project.Main")) // Substitua pela sua classe main real
    }
}

tasks.named("build") {
    dependsOn("shadowJar")
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
* Substitua `"com.project.Main"` pelo nome **totalmente qualificado** da sua classe `Main`.
{% endhint %}
{% endstep %}

{% step %}
Construa o Projeto.

Para limpar construções antigas e gerar novos arquivos JAR, execute:

```bash
gradle clean build
```

{% stepper %}
{% step %}
JAR Padrão (JAR Regular do Projeto).

📌 **Nome do arquivo:** `<project-name>.jar`\
📌 **Exemplo:** `discordbot.jar`\
📌 **Conteúdo:**

* Apenas **o código compilado do seu projeto**.
* **NÃO inclui dependências**.

{% hint style="danger" %}
**NÃO use este arquivo para execução** a menos que as dependências sejam tratadas separadamente.
{% endhint %}
{% endstep %}

{% step %}
JAR Gordo (Uber JAR com Dependências).

📌 **Nome do arquivo:** `<project-name>-all.jar`\
📌 **Exemplo:** `discordbot-all.jar`\
📌 **Conteúdo:**

* Seu **código de aplicação compilado**.
* **Todas as dependências incluídas** (JDA, Apache Commons, etc.).
* **Arquivo de manifesto (`MANIFEST.MF`) com a entrada `Main-Class`**.

{% hint style="success" %}
**Use este arquivo para execução e upload.**
{% endhint %}
{% endstep %}
{% endstepper %}
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### **Recomendação**

Renomeie seu arquivo JAR para um nome simples como `app.jar` para evitar problemas com caracteres especiais.​
{% endhint %}
