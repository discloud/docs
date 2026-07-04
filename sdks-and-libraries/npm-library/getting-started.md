---
description: >-
  Learn how to install, configure, and start using the discloud.app NPM library
  to manager your Discloud application.
icon: flag-checkered
---

# Getting Started

## 📦 Installation

You can install the **discloud.app** library using your preferred package manager:

{% tabs %}
{% tab title="NPM" %}
```bash
npm install discloud.app
```
{% endtab %}

{% tab title="Yarn" %}
```bash
yarn add discloud.app
```
{% endtab %}

{% tab title="PNPM" %}
```bash
pnpm add discloud.app
```
{% endtab %}

{% tab title="Bun" %}
```bash
bun add discloud.app
```
{% endtab %}
{% endtabs %}

## 🔑 Obtaining Your API Token

Before using the library, you need to obtain your **Discloud API Token**.

For detailed instructions on how to get your API token, please visit [here](../../faq/general-questions/how-can-i-get-my-discloud-api-token.md).

{% hint style="danger" %}
**Keep your token secure!** Never share it publicly or commit it to version control. Store it in environment variables or secure configuration files.
{% endhint %}

## 🚀 Basic Setup

### Environment Variables Configuration

{% stepper %}
{% step %}
Create a `.env` file in your project root to store your API token securely:

{% code title=".env" %}
```bash
DISCLOUD_TOKEN=your_api_token_here
```
{% endcode %}
{% endstep %}

{% step %}
Install the **dotenv** package to load environment variables:

```bash
npm install dotenv
```
{% endstep %}

{% step %}
Then use it in your application:

{% code title="index.js" %}
```javascript
require("dotenv").config(); // Load environment variables
const { discloud } = require("discloud.app");

async function main() {
  try {
    // Authenticate using environment variable
    await discloud.login(process.env.DISCLOUD_TOKEN);
    console.log("Successfully authenticated with Discloud!");

    // Your application logic here...
  } catch (error) {
    console.error("Authentication failed:", error.message);
  }
}

main();
```
{% endcode %}
{% endstep %}
{% endstepper %}

## 🎯 Your First API Call

Let's test the connection by fetching information about your applications:

{% code title="test-connection.js" %}
```javascript
require("dotenv").config(); // Load environment variables
const { discloud } = require("discloud.app");

async function testConnection() {
  try {
    // Authenticate
    await discloud.login(process.env.DISCLOUD_TOKEN);

    // Fetch all your applications
    const apps = await discloud.apps.fetch("all");

    console.log(`Found ${apps.size} applications:`);
    apps.forEach((app, id) => {
      console.log(`- ${app.name} (ID: ${id})`);
    });
  } catch (error) {
    console.error("Error:", error.message);
  }
}

testConnection();
```
{% endcode %}

## 📁 TypeScript Support

The library includes full **TypeScript** support with type definitions:

{% code title="index.ts" %}
```typescript
import "dotenv/config"; // Load environment variables
import { discloud, App } from "discloud.app";

async function main(): Promise<void> {
  try {
    await discloud.login(process.env.DISCLOUD_TOKEN!);

    // Fetch a specific application with full type support
    const app: App = await discloud.apps.fetch("your_app_id");

    console.log(`App: ${app.name}`);
    console.log(`Status: ${app.online ? "Online" : "Offline"}`);
    console.log(`RAM: ${app.ram}MB`);
  } catch (error) {
    console.error("Error:", error);
  }
}

main();
```
{% endcode %}

***

{% hint style="success" %}
**Ready to go!** You've successfully set up the discloud.app library. Check out [Usage Examples](usage-examples.md) to see what you can build!
{% endhint %}
