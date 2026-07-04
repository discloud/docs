---
description: >-
  Examples and use cases for the discloud.app NPM library, covering application
  management, monitoring, team operations, and more.
icon: vial
---

# Usage Examples

{% hint style="info" %}
**Important**: To obtain your API Token required in the examples below, see [here](../../faq/general-questions/how-can-i-get-my-discloud-api-token.md).

**Setup Required**: Make sure you've completed the [**Getting Started**](getting-started.md) guide before using these examples.
{% endhint %}

***

## 👤 User Management

### 📄 Fetching User Information

```javascript
const { discloud } = require("discloud.app");

try {
  const user = await discloud.user.fetch();

  console.log("User information:", user);
} catch (error) {
  console.error("Failed to fetch user:", error.message);
}
```

## 📱 Application Management

### 🚀 Uploading a New Application

{% tabs %}
{% tab title="From File Path" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.create({
    file: "./my-bot.zip", // Path to your ZIP file
  });

  console.log("Upload successful!");
} catch (error) {
  console.error("Upload failed:", error.message);
}
```
{% endtab %}

{% tab title="From Buffer/Blob" %}
```javascript
const fs = require("fs");
const { discloud } = require("discloud.app");

try {
  const fileData = fs.readFileSync("./my-bot.zip");

  await discloud.apps.create({
    file: {
      data: fileData, // Buffer or Blob
      name: "my-bot.zip", // Original filename
    },
  });

  console.log("Upload successful!");
} catch (error) {
  console.error("Upload failed:", error.message);
}
```
{% endtab %}

{% tab title="From Stream" %}
```javascript
const fs = require("fs");
const { discloud, streamToFile } = require("discloud.app");

try {
  const stream = fs.createReadStream("./my-bot.zip");
  const file = await streamToFile(stream, "my-bot.zip");

  await discloud.apps.create({ file });
  console.log("Upload successful!");
} catch (error) {
  console.error("Upload failed:", error.message);
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Before uploading:** Ensure your ZIP file contains the [`discloud.config`](https://github.com/discloud/docs/blob/english/configurations/discloud.config) file and follows the [**preparation guidelines**](../../development-environment/supported-languages/javascript/) for your language.
{% endhint %}

### 🔄 Updating (Committing) an Application

{% tabs %}
{% tab title="File path / URL" %}
```javascript
const { discloud } = require("discloud.app");

await discloud.apps.update("APP_ID", {
  file: "FILE_PATH/FILE_NAME.zip",
});
```
{% endtab %}

{% tab title="Blob | Buffer | File | RawFile | ReadableStream" %}
```javascript
const { discloud } = require("discloud.app");
const fs = require("fs");

await discloud.apps.update("APP_ID", {
  file: {
    data: fs.readFileSync("FILE_PATH/FILE_NAME.zip"),
    name: "FILE_NAME.zip",
  },
});
```
{% endtab %}
{% endtabs %}

### 📱 Fetching Application Information

{% tabs %}
{% tab title="Single Application" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const app = await discloud.apps.fetch("your_app_id");
  console.log("Application info:", app);
} catch (error) {
  console.error("Failed to fetch app:", error.message);
}
```
{% endtab %}

{% tab title="All Applications" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const apps = await discloud.apps.fetch("all");
  console.log("Applications:", apps);
} catch (error) {
  console.error("Failed to fetch apps:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 🗑️ Deleting Applications

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.delete("your_app_id");
  console.log("App deleted successfully!");
} catch (error) {
  console.error("Failed to delete app:", error.message);
}
```

{% hint style="danger" %}
**Warning:** Deleting an application is **permanent** and cannot be undone. Make sure to backup your data before deletion.
{% endhint %}

***

## ⚡ Application Control

### 🟢 Starting Applications

{% tabs %}
{% tab title="Single App" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.start("your_app_id");
  console.log("App started successfully!");
} catch (error) {
  console.error("Failed to start app:", error.message);
}
```
{% endtab %}

{% tab title="All Apps" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.start("all");
  console.log("All apps started!");
} catch (error) {
  console.error("Failed to start apps:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 🔴 Stopping Applications

{% tabs %}
{% tab title="Single App" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.stop("your_app_id");
  console.log("App stopped successfully!");
} catch (error) {
  console.error("Failed to stop app:", error.message);
}
```
{% endtab %}

{% tab title="All Apps" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.stop("all");
  console.log("All apps stopped!");
} catch (error) {
  console.error("Failed to stop apps:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 🔄 Restarting Applications

{% tabs %}
{% tab title="Single App" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.restart("your_app_id");
  console.log("App restarted successfully!");
} catch (error) {
  console.error("Failed to restart app:", error.message);
}
```
{% endtab %}

{% tab title="All Apps" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.restart("all");
  console.log("All apps restarted successfully!");
} catch (error) {
  console.error("Failed to restart apps:", error.message);
}
```
{% endtab %}
{% endtabs %}

***

## 📊 Monitoring & Diagnostics

### 📈 Checking Application Status

{% tabs %}
{% tab title="Single App Status" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const status = await discloud.apps.status("your_app_id");
  console.log("Status fetched successfully!");
} catch (error) {
  console.error("Failed to get status:", error.message);
}
```
{% endtab %}

{% tab title="All Apps Status" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const statusMap = await discloud.apps.status("all");
  console.log("All status fetched successfully!");
} catch (error) {
  console.error("Failed to get status:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 📋 Viewing Application Logs

{% tabs %}
{% tab title="Single App Logs" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const logs = await discloud.apps.terminal("your_app_id");
  console.log("Logs fetched successfully!");
} catch (error) {
  console.error("Failed to get logs:", error.message);
}
```
{% endtab %}

{% tab title="All Apps Logs" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const logsMap = await discloud.apps.terminal("all");
  console.log("All logs fetched successfully!");
} catch (error) {
  console.error("Failed to get logs:", error.message);
}
```
{% endtab %}
{% endtabs %}

### 💻 Sending Terminal Commands

```javascript
const { discloud } = require("discloud.app");

try {
  const result = await discloud.apps.console("your_app_id", "ls -la");
  console.log("Command result:", result);
} catch (error) {
  console.error("Command failed:", error.message);
}
```

### 💾 Backup Operations

#### 📦 Creating Backups

{% tabs %}
{% tab title="Single App Backup" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const backup = await discloud.apps.backup("your_app_id");
  console.log("Backup created successfully!");
} catch (error) {
  console.error("Backup failed:", error.message);
}
```
{% endtab %}

{% tab title="All Apps Backup" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const backups = await discloud.apps.backup("all");
  console.log("All backups created successfully!");
} catch (error) {
  console.error("Backup failed:", error.message);
}
```
{% endtab %}
{% endtabs %}

***

## 👥 Team Management

### 👨‍💼 Managing Application Moderators

{% tabs %}
{% tab title="Fetch Team Members" %}
```javascript
const { discloud } = require("discloud.app");

try {
  const team = await discloud.appTeam.fetch("your_app_id");
  console.log("Team members fetched successfully!");
} catch (error) {
  console.error("Failed to fetch team:", error.message);
}
```
{% endtab %}

{% tab title="Add Team Member" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appTeam.create("your_app_id", "user_id", [
    "backup_app", // Can create backups
    "commit_app", // Can update the app
    "edit_ram", // Can modify RAM allocation
    "logs_app", // Can view application logs
    "restart_app", // Can restart the application
    "start_app", // Can start the application
    "status_app", // Can view app status
    "stop_app", // Can stop the application
  ]);

  console.log("Moderator added successfully!");
} catch (error) {
  console.error("Failed to add moderator:", error.message);
}
```
{% endtab %}

{% tab title="Edit Permissions" %}
```javascript
const { discloud, ModPermissions } = require("discloud.app");

try {
  await discloud.appTeam.edit("your_app_id", "user_id", [
    ModPermissions.backup_app, // Can create backups
    ModPermissions.commit_app, // Can update the app
    ModPermissions.edit_ram, // Can modify RAM allocation
    ModPermissions.logs_app, // Can view application logs
    ModPermissions.restart_app, // Can restart the application
    ModPermissions.start_app, // Can start the application
    ModPermissions.status_app, // Can view app status
    ModPermissions.stop_app, // Can stop the application
  ]);

  console.log("Permissions updated successfully!");
} catch (error) {
  console.error("Failed to edit permissions:", error.message);
}
```
{% endtab %}

{% tab title="Remove Team Member" %}
```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appTeam.delete("your_app_id", "user_id");
  console.log("Moderator removed successfully!");
} catch (error) {
  console.error("Failed to remove moderator:", error.message);
}
```
{% endtab %}
{% endtabs %}

***

## ⚙️ System Management

### 🔧 Managing RAM Allocation

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.ram("your_app_id", 512);
  console.log("RAM updated successfully!");
} catch (error) {
  console.error("RAM update failed:", error.message);
}
```

{% hint style="warning" %}
#### **RAM Requirements**

* Bot applications: minimum 100MB
* Website applications: minimum 512MB
* Check your plan limits before increasing RAM
{% endhint %}

### 🎨 Updating Application Profile

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.apps.profile("your_app_id", {
    name: "My Awesome Bot",
    avatarURL: "https://example.com/avatar.png",
  });

  console.log("Profile updated successfully!");
} catch (error) {
  console.error("Profile update failed:", error.message);
}
```

{% hint style="info" %}
#### **Profile Update Details**

* `name`: Optional. New name for your application (maximum 30 characters).
* `avatarURL`: Optional. URL of the new avatar image. Supported formats: GIF, JPG, JPEG, PNG.
{% endhint %}

### 📦 APT Package Management

#### 📥 Installing APT Packages

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appApt.install("your_app_id", [
    "tools",
    "canvas",
    "tesseract",
    "puppeteer",
    "selenium",
    "java",
    "ffmpeg",
    "libgl",
    "openssl",
    "mysql",
    "unixodbc",
  ]);

  console.log("Packages installed successfully!");
} catch (error) {
  console.error("Installation failed:", error.message);
}
```

#### 🗑️ Uninstalling APT Packages

```javascript
const { discloud } = require("discloud.app");

try {
  await discloud.appApt.uninstall("your_app_id", ["canvas", "ffmpeg"]);
  console.log("Packages uninstalled successfully!");
} catch (error) {
  console.error("Uninstallation failed:", error.message);
}
```
