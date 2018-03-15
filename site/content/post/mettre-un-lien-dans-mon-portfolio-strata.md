---
title: Mettre un lien dans mon portfolio Strata
date: '2018-03-15T14:56:41+01:00'
---
Tu cherche à mettre un lien dans ton portfolio Strata pour Hugo, et tu ne sais pas comment faire? Pas de panique tu es au bon endroit. Super Alex te dit tout !

Tu as un thème Strata pour Hugo, et c'est top tout va bien ! Mais là tu veux montrer tes réalisations au monde entier mais tu ne sais pas comment mettre ton lien?

Alors voici comment faire :

Tu vas dans ton fichier config.toml (celui sui se trouve dans le dossier site), et là tu va rajouter une ligne en dessous de description de ton "params.portfolio.gallery" :

url = "mon.lien.com"

Facile et après tu vas chercher ton fichier portfolio.html (celui qui se trouve dans site/themes/hugo/layouts/partials):

pour changer la ligne :

```
<h3>{{ .title | markdownify }}</h3>
```

par :

```
<a href="{{ .url }}"><h3>{{ .title | markdownify }}</h3></a>
```

Là tu récupère tout simplement le contenu de ton "url" pour le mettre dans ta balise a qui entoure le h3, met tu peux le mettre où tu veux bien sur !

Après à toi de voir sur ce principe opur rajouter d'autres champs et toutes les autres fantaisie que tu veux car ce n'est finalement pas très compliqué !

Enjoy!
