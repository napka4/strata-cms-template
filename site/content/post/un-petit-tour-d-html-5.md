---
title: Un petit tour d'HTML 5
date: '2018-04-03T14:47:21+02:00'
---
Je suis tombée sur un article qui présente les nouveau balisages HTML 5 qui sont très pratiques et pourtant peu utilisés ! 

Alors voici un petit tour d'horizon de ces nouvelles balises : 

1 La balise "details"

<script src="https://snipsave.com/embed/BsIFStX01FJYzq3gIZ.js"></script>

Elle permet de faire une petite liste cliquable pour l'utilisateur 

<details>

  <summary>Copyright 1999-2014.</summary>

  <p> - by SuperAlex. All Rights Reserved.</p>

  <p>All content and graphics on this web site are the property of SuperAlex.</p>

</details>

_pas supporté chez IE_

2 La balise "mark"

<script src="https://gist.github.com/napka4/203fa705453f371c3fcfeb805158e836.js"></script>

Pratique permet de surligné du texte :

<p>Do not forget to buy <mark>milk</mark> today.</p>

3 La balise "small"

<script src="https://gist.github.com/napka4/545be0563e244c587c8e9b721a4cf85b.js"></script>

Pratique pour écrire des trucs petits tels les copyrights: (exemple piqué sur le site de la W3School)

<p>W3Schools.com - the world's largest web development site.</p>

<p><small>Copyright 1999-2050 by Refsnes Data.</small></p>

_Note: Il est possible que vous ne voyez rien de différent (compatibilité des navigateurs ...)_

4 La balise "progress"

<script src="https://gist.github.com/napka4/d57738ded5c71c3d37d8f757194e4e5d.js"></script>

Permet de faire des barres de progression :

<progress value="80" max="100">

</progress>

5 La balise "abbr"

```
<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>
```

Avec celle là on peut utiliser une abbréviation et la définir comme une sorte de tooltip :

<p>The <abbr title="World Health Organization">WHO</abbr> was founded in 1948.</p>

6 La balise "area"

```
<p>Click on the sun or on one of the planets to watch it closer:</p><img src="planets.gif" width="145" height="126" alt="Planets" usemap="#planetmap"><map name="planetmap">   <area shape="rect" coords="0,0,82,126" alt="Sun" href="sun.htm">   <area shape="circle" coords="90,58,3" alt="Mercury" href="mercur.htm">   <area shape="circle" coords="124,58,8" alt="Venus" href="venus.htm"></map>
```

Cette balise est une balise géniale ! (hyper enthousiaste de l'avoir trouvée celle-là)

Elle permet de définir des zones cliquables sur une image et d'y attribuer du coup des actions (links,etc).

_Exemple de la W3School:_

<p>Click on the sun or on one of the planets to watch it closer:</p>

<img src="https://www.w3schools.com/TAGS/planets.gif" width="145" height="126" alt="Planets" usemap="#planetmap">

<map name="planetmap">

  <area shape="rect" coords="0,0,82,126" alt="Sun" href="sun.htm">

  <area shape="circle" coords="90,58,3" alt="Mercury" href="mercur.htm">

  <area shape="circle" coords="124,58,8" alt="Venus" href="venus.htm">

</map>

_Note: Il est possible que vous ne voyez rien de différent (compatibilité des navigateurs)_

Je vous en rajouterai d'autres à l'occasion ! 

Bisous bisous !
