---
description: >-
  Install and manage a Java JDK locally (Windows, macOS, Linux) using
  installers, package managers, or SDKMAN!; build a runnable JAR with Maven or
  Gradle.
icon: java
---

# Java

## 🧾 Overview

Java runs on the JVM and is used for Discord bots (JDA, Discord4J), APIs (Spring Boot, Javalin), and background services. A local JDK lets you:

* Compile and run your project before uploading it to Discloud
* Manage dependencies with Maven or Gradle
* Build the runnable `.jar` that you upload to Discloud

{% embed url="https://adoptium.net/" %}

{% hint style="info" %}
On Discloud, Java applications are uploaded as a **pre-built `.jar`**. See [Java](../supported-languages/java.md) for hosting details and [How to build and package a Java application?](../../faq/general-questions/how-to-build-and-package-a-java-application.md) for the full build walkthrough.
{% endhint %}

***

## 📥 Installation

Install a **JDK** (not just a JRE): the JDK includes the `javac` compiler. The examples below use [Eclipse Temurin](https://adoptium.net/), a free OpenJDK build. Pick an LTS version (e.g. 21).

{% tabs %}
{% tab title="🪟 Windows" %}
{% tabs %}
{% tab title="Installer" %}
{% stepper %}
{% step %}
Open [https://adoptium.net/](https://adoptium.net/) and download the LTS `.msi` installer
{% endstep %}

{% step %}
Run the installer and enable **Set JAVA\_HOME variable** and **Add to PATH**
{% endstep %}

{% step %}
Reopen the terminal and verify

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
{% tab title="Installer" %}
Download the LTS `.pkg` from [adoptium.net](https://adoptium.net/), install it, then:

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

## 🧰 Build Tools (Maven or Gradle)

Most Java projects use a build tool to download dependencies and produce the `.jar`. Use the one your project already has (`pom.xml` = Maven, `build.gradle` = Gradle).

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
If the project has a Gradle wrapper (`gradlew`), you don't need to install Gradle: use `./gradlew` (or `gradlew.bat` on Windows).

```bash
# macOS
brew install gradle
# SDKMAN! (any OS)
sdk install gradle

gradle -version
```
{% endtab %}
{% endtabs %}

***

## 🧪 Minimal Workflow

{% stepper %}
{% step %}
Build the project into a JAR

```bash
# Maven
mvn clean package
# Gradle
./gradlew build
```
{% endstep %}

{% step %}
Test the JAR locally before uploading

```bash
java -jar target/my-app.jar
```
{% endstep %}

{% step %}
Upload the `.jar` to Discloud, with `MAIN` in your `discloud.config` pointing to it.
{% endstep %}
{% endstepper %}

{% hint style="info" %}
The exact JAR name and folder (`target/` for Maven, `build/libs/` for Gradle) depend on your project. To include the dependencies in a single runnable JAR, see [How to build and package a Java application?](../../faq/general-questions/how-to-build-and-package-a-java-application.md).
{% endhint %}

***

## 🔄 Updating

| Task                             | Command                                         |
| -------------------------------- | ----------------------------------------------- |
| Update JDK (SDKMAN!)             | `sdk upgrade java`                              |
| Update JDK (Homebrew)            | `brew upgrade --cask temurin@21`                |
| Update JDK (winget)              | `winget upgrade EclipseAdoptium.Temurin.21.JDK` |
| Check dependency updates (Maven) | `mvn versions:display-dependency-updates`       |

***

## 🗃 Common Commands

```bash
java -version
mvn clean package
mvn dependency:tree
./gradlew build
./gradlew dependencies
java -jar app.jar
```
