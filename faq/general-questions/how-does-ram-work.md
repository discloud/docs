---
description: >-
  What RAM is, why its usage goes up and down, and what happens when your
  application reaches the limit.
icon: memory
---

# How does RAM work?

## ⚡ Quick answer

{% hint style="success" %}
**RAM is not a balance that runs out.** On Discloud, it works just like the RAM on your computer: usage goes up while the application is using memory and goes down when it releases it.

Seeing RAM usage go up does **not** mean your plan is running out. The free plan doesn't expire.
{% endhint %}

***

## 🧠 What RAM is

RAM is the application's **working memory**. It holds everything the application is using **right now**: variables, loaded data, open connections and cache.

Think of a desk and a cabinet:

* **RAM** is the **desk**. Everything you're using right now sits on it. It's fast, but it has a limited size and gets cleared when you stop.
* The **disk** (SSD) is the **cabinet**. It stores files permanently, even when everything is turned off.

The same thing happens on your computer. When you open a browser with many tabs, RAM usage goes up. When you close it, usage goes down. Memory isn't "spent", it's only occupied while something is using it.

| Feature                       | RAM                                        | Disk (SSD)                                    |
| ----------------------------- | ------------------------------------------ | --------------------------------------------- |
| What it holds                 | What the application is using right now    | The application's files (code, data, uploads) |
| When the application restarts | It's cleared and starts over               | It stays the same                             |
| Speed                         | Very fast                                  | Slower                                        |
| On Discloud                   | Limited by the application's allocated RAM | Shows up as `ssd` in the application's status |

***

## 🔄 Why usage goes up and down

RAM usage changes all the time, depending on what the application is doing:

* **When it starts**, it loads the code, dependencies and connections. Usage rises quickly.
* **With each action**, like a command, a request or a generated image, it uses more memory for a while.
* **After the action**, that memory is released and usage goes down.
* **Over time**, libraries like discord.js and discord.py keep data in cache (servers, members, messages) to respond faster. This takes up memory continuously.

{% hint style="info" %}
#### **Memory doesn't come back right away**

Node.js, Python and Java don't give memory back as soon as they're done with it. A **garbage collector** cleans up from time to time. That's why usage can stay high for a while and then drop all at once. This is normal.
{% endhint %}

What matters is the **trend**. If usage rises, oscillates and then stays in a similar range, everything is fine.

***

## 📏 Allocated RAM and RAM in use

These are two different numbers:

| Number            | What it is                                                                            |
| ----------------- | ------------------------------------------------------------------------------------- |
| **Allocated RAM** | The most the application can use. This amount is reserved from your plan's total RAM. |
| **RAM in use**    | How much the application is using right now. It changes all the time.                 |

In the application's status, both show up together. For example, `39.9MB/100MB` means the application is using 39.9 MB out of a 100 MB limit.

To see the current usage:

* In the [Discloud Dashboard](https://discloud.com/dashboard), on your application.
* In the bot, with the `/status (ID)` command. See the [Bot Commands](../../how-to-host-using/discord-bot/commands.md).
* In the [CLI](../../how-to-host-using/cli.md), with `discloud app status <ID>`.
* In the [API](../../api-and-integrations/api-overview/applications.md), in the `memory` field of the application's status.

***

## 🧮 How much RAM does the application need?

It depends on the language, the libraries and how much the application is used. Some things usually take a lot of memory:

* Playing music, especially with `ffmpeg`.
* Generating or editing images.
* Opening browsers with [Puppeteer](../../configurations/puppeteer.md).
* Bots in many servers, because of the cache.
* Loading large files or AI models into memory.

To choose the allocated RAM:

{% stepper %}
{% step %}
**Check the real usage**

Run the application for a while, using its heaviest features, and see how high usage goes.
{% endstep %}

{% step %}
**Leave some headroom**

Allocate a bit more than the highest usage you saw. That way a spike doesn't take the application down.
{% endstep %}

{% step %}
**Adjust the allocated RAM**

Use the `RAM` option in [`discloud.config`](../../configurations/discloud.config/), the bot's `/memoria` command or the [API](../../api-and-integrations/api-overview/applications.md). Allocated RAM counts toward your plan's total.
{% endstep %}
{% endstepper %}

***

## 🚫 What happens at the limit

If the application tries to use **more RAM than it has allocated**, Discloud **stops** the application. This has nothing to do with your plan running out: the application just went over its own limit.

To fix it, you can:

* **Increase the allocated RAM**, if the application really needs more memory.
* **Reduce usage**, by optimizing the part of the code that uses the most.

See also [Diagnosing Offline Applications](../troubleshooting-solutions/diagnosing-offline-applications.md).

***

## 🚨 What if usage never stops rising?

If usage **keeps rising**, never levels off and rises the same way again after a restart, it's probably a **memory leak**. The application holds on to memory and never releases it.

{% hint style="warning" %}
Increasing the RAM **doesn't fix** a leak. The application just takes longer to reach the new limit.
{% endhint %}

Common causes:

* Arrays, `Map`s or dictionaries that only grow and never have items removed.
* `client.on(...)` or `setInterval` created **inside** a command, which repeat on every use.
* Unlimited library cache. In discord.js, use `makeCache` and `sweepers`. In discord.py, adjust `max_messages` and `member_cache_flags`.
* Browsers or processes that are opened and never closed.

{% code title="Leak example and fix" %}
```javascript
// ❌ keeps every message forever
const history = [];
client.on("messageCreate", (message) => history.push(message));

// ✅ keeps only the last 100
const MAX_HISTORY = 100;
const recent = [];
client.on("messageCreate", (message) => {
  recent.push(message.content);
  if (recent.length > MAX_HISTORY) recent.shift();
});
```
{% endcode %}

To find the cause, write memory usage to the [logs](how-to-access-the-application-logs.md) from time to time and see which action makes it rise:

{% tabs %}
{% tab title="Node.js" %}
```javascript
setInterval(() => {
  const mb = process.memoryUsage().rss / 1024 / 1024;
  console.log(`RAM: ${mb.toFixed(1)} MB`);
}, 60_000);
```
{% endtab %}

{% tab title="Python" %}
```python
import tracemalloc

tracemalloc.start()

# after it has been running for a while:
for stat in tracemalloc.take_snapshot().statistics("lineno")[:10]:
    print(stat)  # the 10 lines that allocate the most memory
```
{% endtab %}
{% endtabs %}

***

## ❓ Still need help?

See the [**General Questions**](./) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
