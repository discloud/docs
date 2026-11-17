---
description: >-
  Learn how to generate and configure the 'package.json' file, defining the
  essential dependencies to host your JavaScript project on Discloud.
icon: file-code
---

# package.json

## 🗂️ What is `package.json`?

The `package.json` file is essential for managing metadata and dependencies of Node.js projects. It ensures that the necessary libraries are automatically installed when hosting your application on Discloud.

***

## 🛠️ How to Create `package.json`

To generate the `package.json` file for your project, follow the steps below:

{% stepper %}
{% step %}
**Open the terminal in your project directory**

On Windows, use **Shift + Right Click** and select "Open PowerShell".
{% endstep %}

{% step %}
**Run the following command to create the `package.json` automatically:**

```bash
npm init -y
```

This command will create a `package.json` file in your project directory.
{% endstep %}
{% endstepper %}

***

## 📝 Structure of `package.json`

After creation, the `package.json` file should look like this:

{% code title="package.json" %}
```json
{
  "name": "discloud",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {}
}
```
{% endcode %}

{% hint style="info" %}
If you want to host a **Discord.js** bot or any other framework, you'll need to add dependencies to the `package.json`. Check the next section to learn how to do that.
{% endhint %}

***

## 📦 Adding Dependencies

To add dependencies, use the `npm install` command, which will automatically add the necessary libraries to the `package.json`.

**Example: Install `discord.js`**

```bash
npm install discord.js
```

After installing, your `package.json` will be automatically updated to include `discord.js` in the dependencies:

{% code title="package.json" %}
```json
{
  "name": "discloud",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "discord.js": "^14.0.3"
  }
}
```
{% endcode %}
