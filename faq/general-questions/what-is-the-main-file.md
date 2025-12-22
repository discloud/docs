---
description: Saiba o que é o arquivo principal e como identificá-lo em seu projeto.
---

# O que é o arquivo principal?

## 📂 Arquivos Principais Gerais

O **arquivo principal** (main file) é o código fundamental da sua aplicação. É o ponto de entrada que faz seu bot ficar online ou seu site começar a funcionar. Dependendo da linguagem e de como você o nomeou, exemplos comuns incluem:

- `index.js`
- `bot.js`
- `main.py`
- `index.py`
- `app.js`

---

## ⚠️ Exceções (Padrões)

Alguns softwares de criação de bots, como o **Discord Bot Maker (DBM)** e o **Discord Bot Controls**, já possuem um arquivo principal padrão configurado, que geralmente é:

- `bot.js`

---

## 🔍 Como eu sei qual é o meu arquivo principal?

O arquivo principal é aquele que você usa para iniciar sua aplicação localmente. Se você não tiver certeza, verifique os métodos comuns para cada linguagem abaixo:

{% tabs %}
{% tab title="JavaScript" %}
O arquivo principal é o que você usa para iniciar seu bot:

- Ao executar o comando `node ArquivoPrincipal.js`.
- Geralmente é definido no seu `package.json` sob o campo `"main"`.

```json
{
  "name": "meu-bot",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  }
}
```

{% endtab %}

{% tab title="Python" %}
O arquivo principal é o que você usa para iniciar seu bot:

- Ao executar o comando `python ArquivoPrincipal.py`.
- Clicando com o botão direito no arquivo e selecionando **RUN** no PyCharm ou VS Code.
  {% endtab %}

{% tab title="Java" %}
O arquivo principal é o que você usa para iniciar seu bot:

- Ao executar o comando `java -jar ArquivoPrincipal.jar`.
- Clicando duas vezes no arquivo `.jar`.
  {% endtab %}

{% tab title="Ruby" %}
O arquivo principal é o que você usa para iniciar seu bot:

- Ao executar o comando `ruby ArquivoPrincipal.rb`.
  {% endtab %}

{% tab title="Go" %}
O arquivo principal é o que você usa para iniciar seu bot:

- Ao executar o comando `go run ArquivoPrincipal.go`.
  {% endtab %}

{% tab title="PHP" %}
O arquivo principal é o que você usa para iniciar seu bot:

- Ao executar o comando `php ArquivoPrincipal.php`.
  {% endtab %}

{% tab title="Rust" %}
Em projetos Rust, o arquivo principal geralmente está localizado em:

- `src/main.rs`
  {% endtab %}
  {% endtabs %}

---

## 🛠️ Definindo na Discloud

Depois de identificar seu arquivo principal, você deve especificá-lo em seu arquivo [**`discloud.config`**](../../configurations/discloud.config/) usando a propriedade `MAIN`.

```ini
MAIN=index.js
```

{% hint style="info" %}
O nome `ArquivoPrincipal.*` usado nos exemplos acima é apenas um exemplo. Seu arquivo pode ter qualquer nome que você escolher, desde que seja o ponto de entrada da sua aplicação.
{% endhint %}
