---
description: >-
  Quando o seu bot do Discord precisa de sharding e como isso afeta a RAM na
  Discloud.
---

# Como fazer sharding do meu bot?

**Sharding** divide o seu bot do Discord em várias conexões (shards), e cada uma cuida de uma parte dos servidores. O Discord **exige** sharding quando o bot passa de **2.500 servidores**.

***

## 🧠 Sharding e RAM

Cada shard mantém a própria conexão e o próprio cache. Por isso, mais shards usam mais memória.

* Antes de ativar o sharding, veja o uso atual na página [Como funciona a RAM?](how-does-ram-work.md).
* Depois de ativar, acompanhe o uso por algumas horas e ajuste a RAM alocada no [`discloud.config`](../../configurations/discloud.config/).
* Limitar o cache da biblioteca reduz o uso de memória de cada shard.

***

## 🛠️ Exemplos

{% tabs %}
{% tab title="discord.js" %}
Com o `ShardingManager`, um arquivo inicia os shards e cada shard roda o arquivo do bot.

{% code title="index.js" %}
```javascript
const { ShardingManager } = require("discord.js");

const manager = new ShardingManager("./bot.js", {
  token: process.env.TOKEN,
  totalShards: "auto",
});

manager.on("shardCreate", (shard) => console.log(`Shard ${shard.id} iniciado`));
manager.spawn();
```
{% endcode %}

No `discloud.config`, aponte o `MAIN` para o arquivo que inicia os shards (no exemplo, `index.js`).
{% endtab %}

{% tab title="discord.py" %}
O `AutoShardedClient` decide quantos shards usar e roda todos no mesmo processo.

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
O `ShardingManager` do discord.js cria um processo para cada shard por padrão. Isso usa mais RAM do que rodar todos os shards no mesmo processo.
{% endhint %}

***

## ❓ Ainda precisa de ajuda?

Veja as [**Perguntas Gerais**](./) ou junte-se ao nosso [**Servidor Discord**](https://discord.discloudbot.com/) para suporte.
