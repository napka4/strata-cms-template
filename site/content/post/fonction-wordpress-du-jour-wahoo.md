---
title: 'Fonction Wordpress du jour : Wahoo !'
date: '2018-03-14T18:21:38+01:00'
---
Il y a quelques semaines lors d'un de mes cours de formation sur Node.js, un de mes collègues de promo m'a parlé de ce qu'il faisait avec Wordpress. Et bien sur j'ai ouvert grands les oreilles car c'est mon activité principale !

Et là il m'annonce qu'il modifie et créer des thèmes perso (soit moi aussi je pourrais y arriver si je me penchais vraiment sur la question) avec l'élementor ! En gros il créer des widgets, ou fonctionnalités qu'il intègre à son page builder pour répondre à la demande du client !

Mais TOP !!!! Je dis oui je veux savoir faire ça !

Alors ni une ni deux, on part d'un de mes projets pour un clients perso.

**La base : créer un forum sur Wordpress (again !!), se logguer,poster, et en fonction de si on est loggué ou pas on voit la fonction se logguer ou déco ou s'inscrire !**

Facile? Bah pas avec bbpress, il affiche tout d'un coup et c'est très moche ! Moi je veux un truc qui fasse sérieux quand même ! (You know, I'm a real Developper !)

Donc la solution : créer une classe Auth dans mon thème dans le dossier inc pour créer une condition d'affichage de mon widget.

Je crée donc un dossier "registerTest" dans mon dossier "inc" de mon theme. Puis je crée une classe "Auth". Celle-ci va avoir un : namespace "ForumAlex\RegisterTest"; puis j'utilise Elementor donc une jolie collection de Use :
<script src="https://gist.github.com/napka4/cda3b05d76877274c48b32651d41a397.js"></script>

Ensuite mon widget Auth va apparaître dans ma base de widget d'elementor :

![test du widget créer dans elementor](/img/blog/capture d’écran (2)_li.jpg)

Et voilà ce que ça donne : Quand je ne suis pas connecté ou enregistré 

![mon register en fonction de ma connexion](/img/blog/capture d’écran (3).png)

et si je le suis : 

![la fonction s'enregistrer disparaît](/img/blog/capture d’écran (4).png)
