---
description: >-
  Understand how to compile and package your Java project into a deployable JAR
  file using Maven or Gradle.
---

# How to build and package a Java application?

## 📌 **Why Do I Need to Build My Java Application?**

Discloud **does not compile Java projects** automatically.

You must:\
✔ **Compile your code** into `.class` files.\
✔ **Package everything into a single `.jar` file** (including dependencies).\
✔ **Ensure the `META-INF/MANIFEST.MF` file** correctly defines the **Main-Class**.

***

## 🔧 **Choosing a Build Tool**

<table><thead><tr><th width="112">Build Tool</th><th width="367">Best For</th><th>Required Files</th></tr></thead><tbody><tr><td><strong>Maven</strong></td><td>Large projects, dependency-heavy apps</td><td><code>pom.xml</code></td></tr><tr><td><strong>Gradle</strong></td><td>Modern projects with flexible build scripts</td><td><code>build.gradle</code> or <code>build.gradle.kts</code></td></tr></tbody></table>

***

## 📦 **Building Your Java Application**

{% tabs %}
{% tab title="Maven" %}
[Apache Maven](https://maven.apache.org/guides/index.html) is a widely used build automation tool that manages project builds, dependencies, and documentation using a Project Object Model (POM).​

{% stepper %}
{% step %}
Add the Maven Compiler Plugin.

Ensure your `pom.xml` includes the **Maven Compiler Plugin** to specify the Java version for compilation. This prevents compatibility issues when running the project.

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
* Set `<source>` and `<target>` to the **Java version** required for your project.
{% endhint %}
{% endstep %}

{% step %}
Specify the Main Class.

To make your application executable, you need to specify the entry point (`main` method). This is done using the **Maven Shade Plugin**, which also ensures that all dependencies are bundled inside a **single JAR file**.

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
                <!-- NOTE: Replace this with the fully qualified name of your project's main class -->
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
* Replace `com.project.example.Main` with the actual **fully qualified name** of your `Main` class.
* Ensure the `Main` class contains a valid `public static void main(String[] args)` method.
{% endhint %}
{% endstep %}

{% step %}
Build the Project.

Run the following command to **clean** old builds and generate the new JAR files:

```bash
mvn clean package
```

After running `mvn package`, Maven will create **two** different JAR files inside the `target/` directory:

{% stepper %}
{% step %}
Standard JAR (Original Project JAR).

📌 **Filename:** `original-<artifactId>-<version>.jar`\
📌 **Example:** `original-com.maven.discordbot-0.0.1-SNAPSHOT.jar`\
📌 **Contents:**

* Only **your project's compiled code**.
* **Does NOT include dependencies**.

{% hint style="danger" %}
**Do NOT use this file for execution** unless dependencies are handled separately.
{% endhint %}
{% endstep %}

{% step %}
Fat JAR (Shaded JAR with Dependencies).

📌 **Filename:** `<artifactId>-<version>.jar`\
📌 **Example:** `com.maven.discordbot-0.0.1-SNAPSHOT.jar`\
📌 **Contents:**

* Your **compiled application code**.
* **All dependencies included** (JDA, Apache Commons, etc.).
* **Manifest file (`MANIFEST.MF`) with the `Main-Class` entry**.

{% hint style="success" %}
**Use this file for execution and deployment.**
{% endhint %}
{% endstep %}
{% endstepper %}
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Gradle" %}
[Gradle](https://gradle.org/) is a flexible build automation tool that uses a Groovy or Kotlin-based DSL to define the build process.​

{% stepper %}
{% step %}
Apply the Java Plugin.

Ensure your `build.gradle` (Groovy) or `build.gradle.kts` (Kotlin) applies the **Java plugin**:

{% tabs %}
{% tab title="Groovy" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id 'java'
    id 'com.gradleup.shadow' version '8.3.6' // Shadow Plugin for Fat JAR
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
Specify the Main Class.

To make the application executable, define the **entry point (`main` method)** inside the **JAR manifest**.

{% tabs %}
{% tab title="Groovy" %}
{% code title="build.gradle" %}
```groovy
shadowJar {
    archiveClassifier.set('all')
    manifest {
        attributes(
            'Main-Class': 'com.project.Main' // Replace with your actual main class
        )
    }
}

tasks.build.dependsOn shadowJar // Ensure shadowJar runs when building
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
        attributes(mapOf("Main-Class" to "com.project.Main")) // Replace with your actual main class
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
* Replace `"com.project.Main"` with the **fully qualified name** of your `Main` class.
{% endhint %}
{% endstep %}

{% step %}
Build the Project.

To clean old builds and generate new JAR files, run:

```bash
gradle clean build
```

{% stepper %}
{% step %}
Standard JAR (Regular Project JAR).

📌 **Filename:** `<project-name>.jar`\
📌 **Example:** `discordbot.jar`\
📌 **Contents:**

* Only **your project's compiled code**.
* **Does NOT include dependencies**.

{% hint style="danger" %}
**Do NOT use this file for execution** unless dependencies are handled separately.
{% endhint %}
{% endstep %}

{% step %}
Fat JAR (Uber JAR with Dependencies).

📌 **Filename:** `<project-name>-all.jar`\
📌 **Example:** `discordbot-all.jar`\
📌 **Contents:**

* Your **compiled application code**.
* **All dependencies included** (JDA, Apache Commons, etc.).
* **Manifest file (`MANIFEST.MF`) with the `Main-Class` entry**.

{% hint style="success" %}
**Use this file for execution and deployment.**
{% endhint %}
{% endstep %}
{% endstepper %}
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### **Recommendation**

Rename your JAR file to a simple name like `app.jar` to avoid issues with special characters.​
{% endhint %}
