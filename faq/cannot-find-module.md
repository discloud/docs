## **__Comment résoudre l'erreur suivante?__** `` Error: cannot find module...``
 ### JavaScript
* Habituellement, dans les logs/terminaux est informé le fichier qui a géré l'erreur, et les lignes possibles que l'erreur peut être, vérifiez si dans ce fichier, il a vraiment besoin du module informé.

* Si vous n'en avez pas besoin, supprimez le module répertorié dans la commande.

* Si vous avez besoin, installez le module en exécutant la commande suivante dans votre VSC/IDE: ``npm i (nome_do_modulo) --save``.
  * **exemple:** ``npm i moment --save``.

* Assurez-vous que le module est listé dans le fichier ``package.json`` avant d'héberger l'application sur DisCloud.

* Ne mettez pas de noms avec des accents, des grosses lettres dans votre projet afin de ne pas provoquer de conflit dans le fichier `package.json`, dans la partie `"name"` s'il comporte des majuscules, des caractères spéciaux entre autres, informez des informations le plus simple possible.
  * **exemple:** `"name": "monbot",`

* L'erreur peut également être due au fait que vous avez défini un chemin de lecture incorrect (`./`, `../` , `../../`, etc.) lors de l'extraction des informations du fichier si vous avez spécifié le chemin de lecture à tort, il ne pourra pas être lu.
 
{% hint style="info" %}
 💻 Note: Pour vérifier les logs/terminal, allez simplement sur le chat de ``#🔌┃commands`` et exécutez la commande ``.t`` ou ``.t (ID_DU_BOT)``, certains modules peuvent entrer en conflit avec certaines versions de lib discord alors vérifiez s'il y en a qui ne sont pas compatibles, si l'erreur persiste, allez sur le chat ``#dev-help`` et demandez de l'aide.
{% endhint %}
