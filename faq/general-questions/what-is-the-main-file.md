---
description: Learn what the main file is and how to identify it in your project.
---

# What is the main file?

## 📂 General Main Files

The **main file** is the fundamental code of your application. It is the entry point that makes your bot go online or your website start running. Depending on the language and how you named it, common examples include:

* `index.js`
* `bot.js`
* `main.py`
* `index.py`
* `app.js`

***

## ⚠️ Exceptions (Defaults)

Some bot-making software, such as **Discord Bot Maker (DBM)** and **Discord Bot Controls**, have a default main file already set up, which is usually:

* `bot.js`

***

## 🔍 How do I know my main file?

The main file is the one you use to start your application locally. If you are unsure, check the common methods for each language below:

{% tabs %}
{% tab title="JavaScript" %}
The main file is the one you use to start your bot:

* When running the `node MainFile.js` command.
* It is usually defined in your `package.json` under the `"main"` field.

```json
{
  "name": "my-bot",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  }
}
```
{% endtab %}

{% tab title="Python" %}
The main file is the one you use to start your bot:

* When running the `python MainFile.py` command.
* By right-clicking the file and selecting **RUN** in PyCharm or VS Code.
{% endtab %}

{% tab title="Java" %}
The main file is the one you use to start your bot:

* When running the `java -jar MainFile.jar` command.
* By double-clicking the `.jar` file.
{% endtab %}

{% tab title="Ruby" %}
The main file is the one you use to start your bot:

* When running the `ruby MainFile.rb` command.
{% endtab %}

{% tab title="Go" %}
The main file is the one you use to start your bot:

* When running the `go run MainFile.go` command.
{% endtab %}

{% tab title="PHP" %}
The main file is the one you use to start your bot:

* When running the `php MainFile.php` command.
{% endtab %}

{% tab title="Rust" %}
In Rust projects, the main file is typically located at:

* `src/main.rs`
{% endtab %}
{% endtabs %}

***

## 🛠️ Defining it on Discloud

Once you have identified your main file, you must specify it in your [**`discloud.config`**](../../configurations/discloud.config/) file using the `MAIN` property.

```ini
MAIN=index.js
```

{% hint style="info" %}
The name `MainFile.*` used in the examples above is just a placeholder. Your file can have any name you choose, as long as it is the entry point of your application.
{% endhint %}
