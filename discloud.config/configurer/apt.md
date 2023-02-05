# 📦 APT (Installez de packages)

**APT (Advanced package tool**), fait référence à l'installeur de packages utilisant les distributions Lixnus basées en Debien et Ubuntu.\
\
sur **DisCloud**, vous pouvez additionner quelques packages listés ci-dessous dans le container de votre application en cas de nécessité.

## :gear: Comment utiliser

Consultez le package[^1] nécessaire pour votre projet e insérez-le dans `APT=`

{% hint style="info" %}
Si vous avez besoin de plus que **1 package**, séparez-les par des `virgules et espaces`, comme dans l'exemple ci-dessous:
{% endhint %}

```typescript
...
APT=tools, ffmpeg
...
```

### Packages disponibles

<table><thead><tr><th>Nom du package</th><th data-type="select" data-multiple>Dépendances</th></tr></thead><tbody><tr><td>canvas</td><td></td></tr><tr><td>puppeteer</td><td></td></tr><tr><td>java</td><td></td></tr><tr><td>ffmpeg</td><td></td></tr><tr><td>libgl</td><td></td></tr><tr><td>tools</td><td></td></tr><tr><td>openssl</td><td></td></tr></tbody></table>

[^1]: Insérez uniquement les packages sous "Nom Du Package" dans votre "APT=".&#x20;

    Les dépendances sont juste ce qui sera installé par DisCloud