# git

Synchronisez un répertoire git avec votre application pour des mises à jour automatiques _(commits)_.

Chaque fois qu'un commit est envoyé dans le répertoire de votre application, DisCloud mettra automatiquement à jour vos fichiers d'application.

<figure><img src="../../.gitbook/assets/git-logs_example.png" alt=""><figcaption><p>Exemple de git logs sur DisCloud lors d'un déploiement</p></figcaption></figure>

{% hint style="info" %}
Cette fonctionnalité n'est disponible que pour les forfaits payants.
{% endhint %}

## :pencil: Exigences

Votre application doit déjà être hébergée sur DisCloud.

## **Comment utiliser?**

#### Allez dans le canal de texte `#🔌・commands` et tapez `.git`

<figure><img src="../../.gitbook/assets/git_cmd.png" alt=""><figcaption><p>Commande .git dans le canal de commande</p></figcaption></figure>

{% tabs %}
{% tab title="Github" %}

## URL du répertoire

Allez dans les MP du bot DisCloud et collez l'URL du répertoire git pour votre application.

<figure><img src="../../.gitbook/assets/git_url.png" alt=""><figcaption><p>Coller l'URL du répertoire</p></figcaption></figure>

### Configurer le token d'accès ([Abrir Github](https://github.com/settings/personal-access-tokens/new))

Il est important que l'accès soit disponible pour tous les répertoires _(surtout si vous souhaitez activer la synchronisation pour plus d'une application)_

<figure><img src="../../.gitbook/assets/github_token.png" alt=""><figcaption></figcaption></figure>

#### Configuration des permissions

Définissez `Webhooks` en lecture seule et générez votre jeton.

<figure><img src="../../.gitbook/assets/github_token_permissions.png" alt=""><figcaption></figcaption></figure>

### Webhook

Ouvrez le répertoire de votre application et créez un `webhook`

<figure><img src="../../.gitbook/assets/github_add-webhook.png" alt=""><figcaption></figcaption></figure>

#### Configurer le Webhook

Assurez-vous de changer le `type de contenu` en `application/json`

<figure><img src="../../.gitbook/assets/github_webhook-config.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
