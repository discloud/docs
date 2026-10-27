---
description: >-
  Learn how to generate and configure the requirements.txt file to define
  essential dependencies for hosting your Python project on Discloud.
---

# requirements.txt

## **🗂️ What is `requirements.txt`?**

The `requirements.txt` file is essential for Python projects. It lists all dependencies and their versions, ensuring consistent package installation during deployment on Discloud.

***

## **🛠️ How to Create `requirements.txt`**

You can create this file using two methods:

{% tabs %}
{% tab title="Manual Creation" %}
{% stepper %}
{% step %}
Create a new text file in your project directory.
{% endstep %}

{% step %}
Name it exactly `requirements.txt`.
{% endstep %}
{% endstepper %}
{% endtab %}

{% tab title="Automatic Generation" %}
{% stepper %}
{% step %}
Ensure Python and pip are installed ([installation guide](../../local-environment/python.md)).
{% endstep %}

{% step %}
Open your terminal in the project directory and run:

```bash
pip freeze > requirements.txt
```

This automatically generates a list of all installed packages with their exact versions.
{% endstep %}
{% endstepper %}
{% endtab %}
{% endtabs %}

***

## **📝** Structure of `requirements.txt`

Your file should follow these patterns:

*   **Basic Package (**[**Latest Version**](https://pypi.org/project/discord.py/#history)**)**

    ```
    discord.py
    ```
*   **Version-Specific Package**

    ```
    discord.py==2.0.0
    ```
*   **Version Range**

    ```
    discord.py>=2.0.0
    ```
*   **GitHub Repository (**[**Unstable Version**](https://github.com/Rapptz/discord.py)**)**

    ```
    git+https://github.com/Rapptz/discord.py
    ```

{% hint style="info" %}
#### **Best Practices**

* 🔒 Lock critical dependencies with `==` for specific versions
* 🔄 Use `>=` for packages expecting updates
* 💻 Always test with exact versions before deployment
{% endhint %}

***

## **📦 Adding Packages**

{% stepper %}
{% step %}
**Install packages using pip.**

```bash
pip install package-name
```
{% endstep %}

{% step %}
**Update your requirements file.**

```bash
pip freeze > requirements.txt
```
{% endstep %}
{% endstepper %}

***

## **⚠️ Important Notes**

* Only include packages you actively installed via pip – imported modules don't automatically equal required packages!
* For GitHub-based packages, include the full repository URL as shown in the examples.
* If encountering installation issues, verify all package versions are compatible with your Python version.
