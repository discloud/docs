# Quel est le fichier principal?

## :file\_folder: Fichiers de base généraux

Le fichier principal est le code principal de votre bot, ce qui permet à votre bot de se connecter et d'effectuer automatiquement d'autres actions. Exemples de noms pour le fichier principal possibles: `index.js`, `bot.js` et `index.py`, cela dépend du nom que vous mettez.

## :file\_folder: Exceptions (valeurs par défaut)

Certains logiciels de création de bot, comme **Discord Bot Maker** et **Discord Bot Controls**, ont un fichier principal par défaut déjà défini, à savoir `bot.js`.

## :thinking: Comment connaître mon fichier principal?

{% tabs %}
{% tab title="🟨 JavaScript" %}
### JavaScript

* Le fichier principal est celui que vous utilisez pour allumer votre bot:
  * lors de l'exécution de la commande `node FichierPrincipal.js`
  * qui est généralement dans package.json dans la valeur de: **main**


{% endtab %}

{% tab title="🐍 Python" %}
### Python

* Le fichier principal est celui que vous utilisez pour allumer votre bot:
  * lors de l'exécution de la commande `python FichierPrincipal.py`
  * en cliquant avec le bouton droit de la souris, puis **RUN** **dans PyCharm**.


{% endtab %}

{% tab title="☕ Java" %}
### Java

* Le fichier principal est celui que vous utilisez pour allumer votre bot:
  * lors de l'exécution de la commande `java -jar FichierPrincipal.jar`
  * en cliquant 2 (deux) fois sur le **FichierPrincipal.jar**;


{% endtab %}

{% tab title="💎 Ruby" %}
### Ruby

* Le fichier principal est celui que vous utilisez pour allumer votre bot:
  * lors de l'exécution de la commande `ruby FichierPrincipal.rb`
{% endtab %}

{% tab title="🐿️ Go" %}
### Go

* Le fichier principal est celui que vous utilisez pour allumer votre bot:
  * lors de l'exécution de la commande `go run FichierPrincipal.go`
{% endtab %}

{% tab title="🐘 Php" %}
### Php

* Le fichier principal est celui que vous utilisez pour allumer votre bot:
  * lors de l'exécution de la commande `php FichierPrincipal.php`
{% endtab %}

{% tab title="🦀 Rust" %}
### Rust

Généralment le fichier principal est `src/main.rs`
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Le nom **FichierPrincipal.\*** est le fichier dans la situation décrite, qui varie d'une personne à l'autre car ils peuvent mettre le nom qu'ils veulent, alors analysez votre méthode d'activation du bot en la comparant aux situations présentées à savoir lequel est le **fichier principal**.
{% endhint %}
