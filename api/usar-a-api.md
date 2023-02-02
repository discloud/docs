---
cover: ../../.gitbook/assets/api_routes_bg.png
coverY: 683.9595959595961
---

# 📡 Utiliser l'API

## :pencil: Exigences

#### Obtenir le token

Pour obtenir votre token, utilisez la commande [api](../suporte/comandos/api.md).

<figure><img src="../.gitbook/assets/api_cmd.png" alt=""><figcaption></figcaption></figure>

## Commencer

[Accédez aux chemins de l'API](https://discloud.github.io/apidoc/)\
Cliquez sur `Authorize` et collez votre token de l'API

<figure><img src="../.gitbook/assets/api_login.png" alt=""><figcaption><p>Placer le token dans le champ</p></figcaption></figure>

## Commencez à utiliser l'API

Exemple avec le chemin: `/user`

<figure><img src="../.gitbook/assets/api_get-user_example.png" alt=""><figcaption><p>Exemple de la réponse</p></figcaption></figure>

Vous pouvez importer le code `curl` dans des applications telles que [Insomnia](https://insomnia.rest/download) ou [Postman](https://www.postman.com/downloads/), puis générer dans la langue de votre choix à partir de celles-ci

> Exemples:

{% tabs %}
{% tab title="Insomnia" %}
<div>

<figure><img src="../.gitbook/assets/insomnia_generate_code.png" alt=""><figcaption><p>1</p></figcaption></figure>


<figure><img src="../.gitbook/assets/insomnia_code.png" alt=""><figcaption><p>2</p></figcaption></figure>

</div>


{% endtab %}

{% tab title="Postman" %}
<div>

<figure><img src="../.gitbook/assets/postman_generate_code.png" alt=""><figcaption><p>1</p></figcaption></figure>

 

<figure><img src="../.gitbook/assets/postman_code.png" alt=""><figcaption><p>2</p></figcaption></figure>

</div>
{% endtab %}
{% endtabs %}

Exemple avec du chemin: `/upload`

* Votre fichier `.zip` doit inclure [discloud.config](../discloud.config/configurar/)
* Votre fichier `.zip` doit avoir une taille inférieure ou égale à `100MB`

<figure><img src="../.gitbook/assets/api_upload_example.png" alt=""><figcaption></figcaption></figure>
