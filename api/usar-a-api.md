---
cover: https://i.imgur.com/e12vweQ.png
coverY: 683.9595959595961
---

# 📡 Utiliser l'API

## :pencil: Exigences

#### Obtenir le token

Pour obtenir votre token, utilisez la commande [api](../suporte/comandos/api.md).

<figure><img src="https://i.imgur.com/pHkihk7.png" alt=""><figcaption></figcaption></figure>

## Commencer

[Accédez aux chemins de l'API](https://discloud.github.io/apidoc/)\
Cliquez sur `Authorize` et collez votre token de l'API

<figure><img src="https://i.imgur.com/PwrTXl1.png" alt=""><figcaption><p>Placer le token dans le champ</p></figcaption></figure>

## Commencez à utiliser l'API

Exemple avec le chemin: `/user`

<figure><img src="https://i.imgur.com/zgeJUqY.png" alt=""><figcaption><p>Exemple de la réponse</p></figcaption></figure>

Vous pouvez importer le code `curl` dans des applications telles que [Insomnia](https://insomnia.rest/download) ou [Postman](https://www.postman.com/downloads/), puis générer dans la langue de votre choix à partir de celles-ci

> Exemples:

{% tabs %}
{% tab title="Insomnia" %}
<div>

<figure><img src="https://i.imgur.com/UKOSZix.png" alt=""><figcaption><p>1</p></figcaption></figure>


<figure><img src="https://i.imgur.com/eGWaaOg.png" alt=""><figcaption><p>2</p></figcaption></figure>

</div>


{% endtab %}

{% tab title="Postman" %}
<div>

<figure><img src="https://i.imgur.com/dxIuvp6.png" alt=""><figcaption><p>1</p></figcaption></figure>

 

<figure><img src="https://i.imgur.com/0lIwMyR.png" alt=""><figcaption><p>2</p></figcaption></figure>

</div>
{% endtab %}
{% endtabs %}

Exemple avec du chemin: `/upload`

* Votre fichier `.zip` doit inclure [discloud.config](../discloud.config/configurar/)
* Votre fichier `.zip` doit avoir une taille inférieure ou égale à `100MB`

<figure><img src="https://i.imgur.com/7y2xDx4.png" alt=""><figcaption></figcaption></figure>
