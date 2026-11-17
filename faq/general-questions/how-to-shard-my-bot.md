---
description: When your Discord bot needs sharding and how it affects RAM on Discloud.
---

# How do I shard my bot?

**Sharding** splits your Discord bot into several connections (shards), each one handling part of the servers. Discord **requires** sharding once the bot passes **2,500 servers**.

***

## 🧠 Sharding and RAM

Each shard keeps its own connection and its own cache. That's why more shards use more memory.

* Before enabling sharding, check your current usage on the [How does RAM work?](how-does-ram-work.md) page.
* After enabling it, watch usage for a few hours and adjust the allocated RAM in [`discloud.config`](../../configurations/discloud.config/).
* Limiting the library's cache reduces each shard's memory usage.

***

## 🛠️ Examples

{% tabs %}
{% tab title="discord.js" %}
With the `ShardingManager`, one file starts the shards and each shard runs the bot file.

{% code title="index.js" %}
```javascript
const { ShardingManager } = require("discord.js");

const manager = new ShardingManager("./bot.js", {
  token: process.env.TOKEN,
  totalShards: "auto",
});

manager.on("shardCreate", (shard) => console.log(`Shard ${shard.id} started`));
manager.spawn();
```
{% endcode %}

In `discloud.config`, point `MAIN` at the file that starts the shards (`index.js` in the example).
{% endtab %}

{% tab title="discord.py" %}
`AutoShardedClient` decides how many shards to use and runs all of them in the same process.

{% code title="main.py" %}
```python
import os
import discord

intents = discord.Intents.default()
client = discord.AutoShardedClient(intents=intents)

client.run(os.getenv("TOKEN"))
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
discord.js's `ShardingManager` creates one process per shard by default. That uses more RAM than running every shard in the same process.
{% endhint %}

***

## ❓ Still need help?

See the [**General Questions**](./) or join our [**Discord Server**](https://discord.discloudbot.com/) for support.
