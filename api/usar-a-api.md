---
cover: ../.gitbook/assets/api-banner.png
coverY: 683.9595959595961
---

# 📡 Utiliser l'API

## :pencil: Exigences

#### Obtenir le token

Pour obtenir votre token, utilisez la commande [api](../suporte/comandos/api.md).

<figure><img src="../.gitbook/assets/api-cmd.png" alt=""><figcaption></figcaption></figure>

## Commencer

[Accédez aux routes de l'API](https://discloud.github.io/apidoc/)\
Cliquez sur `Authorize` et collez votre jeton API

<figure><img src="../.gitbook/assets/api-login.png" alt=""><figcaption><p>Placer le token</p></figcaption></figure>

## Commencez à utiliser l'API

exemple avec la route `/user`

<figure><img src="../.gitbook/assets/api-getuser-example.png" alt=""><figcaption><p>Exemple de la réponse de la route /user</p></figcaption></figure>

Vous pouvez importer le code `curl` dans des applications telles que [Insomnia](https://insomnia.rest/download) ou [Postman](https://www.postman.com/downloads/), puis générer le code dans la langue de votre choix à partir de celles-ci

> Exemples:

{% tabs %}
{% tab title="Insomnia" %}
<div>

<figure><img src="../.gitbook/assets/insomnia-generate-code.png" alt=""><figcaption><p>1</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/insomnia-code.png" alt=""><figcaption><p>2</p></figcaption></figure>

</div>


{% endtab %}

{% tab title="Postman" %}
<div>

<figure><img src="../.gitbook/assets/postman-generate-code.png" alt=""><figcaption><p>1</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/postman-code.png" alt=""><figcaption><p>2</p></figcaption></figure>

</div>
{% endtab %}
{% endtabs %}

Exemple avec la route`/upload`

* Votre fichier `.zip` doit inclure [discloud.config](../discloud.config/configurar/)
* Votre fichier `.zip` doit avoir une taille `<=100MB`

<figure><img src="../.gitbook/assets/api-upload-example.png" alt=""><figcaption></figcaption></figure>
