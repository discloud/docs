---
description: >-
  Instale e gerencie um JDK Java localmente (Windows, macOS, Linux) usando
  instaladores, gerenciadores de pacotes ou SDKMAN!; gere um JAR executável com
  Maven ou Gradle.
icon: java
---

# Java

## 🧾 Visão Geral

Java roda na JVM e é usado em bots do Discord (JDA, Discord4J), APIs (Spring Boot, Javalin) e serviços em segundo plano. Um JDK local permite:

* Compilar e executar seu projeto antes de fazer o upload na Discloud
* Gerenciar dependências com Maven ou Gradle
* Gerar o `.jar` executável que você envia para a Discloud

{% embed url="https://adoptium.net/" %}

{% hint style="info" %}
Na Discloud, aplicações Java são enviadas como um **`.jar` já compilado**. Veja [Java](../supported-languages/java.md) para os detalhes de hospedagem e [Como construir e empacotar uma aplicação Java?](../../faq/general-questions/how-to-build-and-package-a-java-application.md) para o passo a passo completo do build.
{% endhint %}

***

## 📥 Instalação

Instale um **JDK** (não apenas um JRE): o JDK inclui o compilador `javac`. Os exemplos abaixo usam o [Eclipse Temurin](https://adoptium.net/), um build gratuito do OpenJDK. Escolha uma versão LTS (ex.: 21).

{% tabs %}
{% tab title="🪟 Windows" %}
{% tabs %}
{% tab title="Instalador" %}
{% stepper %}
{% step %}
Abra [https://adoptium.net/](https://adoptium.net/) e baixe o instalador `.msi` LTS
{% endstep %}

{% step %}
Execute o instalador e ative **Set JAVA\_HOME variable** e **Add to PATH**
{% endstep %}

{% step %}
Reabra o terminal e verifique

```bash
java -version
javac -version
```
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="winget" %}
```bash
winget install EclipseAdoptium.Temurin.21.JDK
java -version
javac -version
```
{% endtab %}

{% tab title="Chocolatey" %}
```bash
choco install temurin21 -y
java -version
javac -version
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🐧 Linux" %}
{% tabs %}
{% tab title="Debian/Ubuntu" %}
```bash
sudo apt update
sudo apt install -y openjdk-21-jdk
java -version
javac -version
```
{% endtab %}

{% tab title="Fedora" %}
```bash
sudo dnf install -y java-21-openjdk-devel
java -version
javac -version
```
{% endtab %}

{% tab title="Arch" %}
```bash
sudo pacman -S --needed jdk21-openjdk
java -version
javac -version
```
{% endtab %}

{% tab title="SDKMAN!" %}
```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 21-tem
java -version
```
{% endtab %}
{% endtabs %}
{% endtab %}

{% tab title="🍎 macOS" %}
{% tabs %}
{% tab title="Instalador" %}
Baixe o `.pkg` LTS em [adoptium.net](https://adoptium.net/), instale e depois:

```bash
java -version
javac -version
```
{% endtab %}

{% tab title="Homebrew" %}
```bash
brew update
brew install --cask temurin@21
java -version
javac -version
```
{% endtab %}

{% tab title="SDKMAN!" %}
```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install java 21-tem
java -version
```
{% endtab %}
{% endtabs %}
{% endtab %}
{% endtabs %}

***

## 🧰 Ferramentas de Build (Maven ou Gradle)

A maioria dos projetos Java usa uma ferramenta de build para baixar as dependências e gerar o `.jar`. Use a que o seu projeto já tem (`pom.xml` = Maven, `build.gradle` = Gradle).

{% tabs %}
{% tab title="Maven" %}
```bash
# Windows (winget)
winget install Apache.Maven
# macOS
brew install maven
# Debian/Ubuntu
sudo apt install -y maven

mvn -version
```
{% endtab %}

{% tab title="Gradle" %}
Se o projeto tiver o Gradle wrapper (`gradlew`), você não precisa instalar o Gradle: use `./gradlew` (ou `gradlew.bat` no Windows).

```bash
# macOS
brew install gradle
# SDKMAN! (qualquer sistema)
sdk install gradle

gradle -version
```
{% endtab %}
{% endtabs %}

***

## 🧪 Fluxo Mínimo

{% stepper %}
{% step %}
Gere o JAR do projeto

```bash
# Maven
mvn clean package
# Gradle
./gradlew build
```
{% endstep %}

{% step %}
Teste o JAR localmente antes de enviar

```bash
java -jar target/my-app.jar
```
{% endstep %}

{% step %}
Envie o `.jar` para a Discloud, com o `MAIN` do seu `discloud.config` apontando para ele.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
O nome e a pasta do JAR (`target/` no Maven, `build/libs/` no Gradle) dependem do seu projeto. Para incluir as dependências em um único JAR executável, veja [Como construir e empacotar uma aplicação Java?](../../faq/general-questions/how-to-build-and-package-a-java-application.md).
{% endhint %}

***

## 🔄 Atualização

| Tarefa                                 | Comando                                         |
| -------------------------------------- | ----------------------------------------------- |
| Atualizar o JDK (SDKMAN!)              | `sdk upgrade java`                              |
| Atualizar o JDK (Homebrew)             | `brew upgrade --cask temurin@21`                |
| Atualizar o JDK (winget)               | `winget upgrade EclipseAdoptium.Temurin.21.JDK` |
| Verificar atualizações de deps (Maven) | `mvn versions:display-dependency-updates`       |

***

## 🗃 Comandos Comuns

```bash
java -version
mvn clean package
mvn dependency:tree
./gradlew build
./gradlew dependencies
java -jar app.jar
```
