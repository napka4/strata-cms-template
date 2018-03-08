---
title: 'Fonction JS du Jour : Bonjour (2)'
date: '2018-03-08T09:33:21+01:00'
---
Sur un de mes projets Wordpress (encore et toujours !), je devais réaliser un système de recherche avec un filtre qui fasse apparaître les résultats de la recherche. 

En gros, lorsque l'utilisateur tape "truc", tout les mots ect contenant "truc" s'affichent mais pas les autres.

J'ai cherché un moment, et on m'a gentillement orientée vers "**list.js**". 

J'ai trouvé pile ce qu'il me fallait grâce à cette mini-lib et comme je suis pas radine je vous offre un bout de code pour vous montrer ce que j'en ai fait !

\-1 D'abord je _charge les scripts_ dont j'aurais besoin :

```
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.10.1/jquery.min.js"></script><script src="//cdnjs.cloudflare.com/ajax/libs/list.js/1.5.0/list.min.js"></script><script src="//cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script><!-- Latest compiled and minified CSS --><link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
```

\-2 Ensuite je mets en place ma _première div_ et le petit code _bootstrap_ pour que tout soit _responsive_ :

```
<div id="test-list" class="container py-3">
```

\-3 Et viens ensuite ma _zone de recherche_, mon champs de texte (input), et les cases à cocher pour faire une _recherche par spécialités_ (une des demandes du clients):

```
  <label>Recherche :      <input type="text" class="fuzzy-search" placeholder="Rechercher par nom"/></label><label>Rechercher par spécialité :</label><br><div class="row">    <label class="col-sm-6 col-lg-3">    <input type="checkbox" name="cartonnage" class="filter" data-value="Cartonnage"/>Cartonnage    </label>    <label class="col-sm-6 col-lg-3">    <input type="checkbox" name="comf" class="filter" data-value="Communication imprimé feuille"/> Communication imprimée feuille     </label>    <label class="col-sm-6 col-lg-3">    <input type="checkbox" name="comroto" class="filter" data-value="Communication imprimé roto"/> Communication imprimée roto    </label></div>
```

Dans cette div j'ajoute une classe"fuzy-search" qui va me servir pour ma fonction js pour filtrer et lister. De même j'ajoute à mes checkboxes un "name", une class "filter", et une data-value pour récupérer les données en js et les utiliser ensuite. 

Une class "row" pour l'affichage, et une class "col-sm-6 col-lg-3" pour un affichage responsive toujours et en colonne de 4 éléments.

\-4  Viens maintenant la liste des éléments que je veux afficher, et qui vont devoir s'éffacer pour laisser ceux de la recherche. La petite difficulté en plus : ce sont des images cliquables qui ont un hover avec une image.

```
<div class="list content row">
```

```
        <div class="one box col-sm-6 col-lg-3"><a href="monsuperlien.fr"><p class="name">trucmachin</p><p class="spec">Etiquettes</p><p class="spec">etuis</p></a></div>
```

```
        <div class="two box col-sm-6 col-lg-3"><a href="monlientropcool.com"><p class="name">abahoui</p><p class="spec">Cartonnage</p><p class="spec">etuis</p></a></div>
```

```
        <div class="three box col-sm-6 col-lg-3"><a href="wahocestcool.io"><p class="name">je suis un artiste</p><p class="spec">retouche</p><p class="spec">numerik</p><p class="spec">Communication imprimé feuille</p><p class="spec">façonnage</p></a></div>....</div>
```

Alors ici j'ai rajouté une class "list content row" à ma div, list sert à regler le padding et le margin, content est une classe de bootstrap de mise en form tout comme row.

Ensuite chaque image et lien sont insérer dans une "div" avec une classe décomposée comme ça : one (j'y mets l'image en background et les propriétés de size) box (ça gère l'affichage de ma div et rends les textes dedans invisibles, oui c'est pas très propre tout ça !), puis une classe de bootstrap "col-sm-6 col-lg-3" pour l'affichage responsive encore ^^

Ma class "name" permet de récupérer le nom de la recherche pour filtrer par nom, la class"spec" sera utilisé pour le filtre par checkboxes.

\-5 Et maintenant le script en js :

```
script>    var options =        {        valueNames: ['name', 'spec']         };    var userList = new List        ('test-list',options);    //filter    $('.filter').change(function() {        var bool = this.checked;        var value = $(this).data("value");        userList.filter(function (item) {            if (item.values().spec == value && bool == true) {        return true;                 } else if (userList.filtered && bool == false) {              return true;               } else {                return false;            }        });        return false;    });    $('.box').click(function(){        window.location.href = $("a",$(this)).attr("href");    });    $('.box').hover(function () {        $(this).css("cursor","pointer")    },function () {        $(this).css("cursor","default")    })</script>
```

Alors voilà un peu d'explications :

var option permet de définir sur quoi on va filtrer les résultats. var user-list est utilisé pour créer la liste de résultat. Ensuite on utilise JQuery pour récupérer les valeurs :

on vérifie si les checkboxes sont cochées, on récupère les valeurs de celles-ci. On  compare ensuite ces valeurs et on retourne un résultat ou pas.

Et voilà ! Alors oui ce code n'est pas très joli, joli, c'est un peu dégueu je le concède mais comme je suis une newbie, j'ai fait au mieux ! Alors si un "expert" passe par-là et à des conseils pour reformater ça un peu mieux je suis preneuse ! 

Sur-ce bonne journée les ptits amis du net et à la prochaine pour une autre péripétie !!
