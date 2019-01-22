---
title: Conditionner l'affichage d'un plugin sur Wordpress en fonction du device
date: '2019-01-22T11:41:00+01:00'
---
<img src="https://raw.githubusercontent.com/napka4/strata-cms-template/master/site/static/img/blog/luca-braco-217276-unsplash.jpg" width="400px" alt="du code php !">

Ouais ouais j'ai un titre de 2km, mais je suis fière !

Et puis j'ai réussi un petit exploi personnel : Conditionner l'affichage d'un plugin Wordpress en fonction du device utilisé.

Pour faire simple, j'avais un plugin de multiscroll en marche pour faire un jôooooli site qui voit son écran splitter en deux et un jôooli effet de scroll.\
Problème sur mobile c'était hideux! Vraiment !

Alors je cherche comme un chinois et finis par trouver le graal !!!\
Oh joie !

Un petit plugin d'abord ==> Conditional Display for Mobile by WonderPlugin\
Qui permet d'utiliser un shortcode qui va décider ou non de ce que verra l'utilisateur en fonction de son device.\
Dans mon problème je voulais lui dire que si c'était un mobile, d'afficher ma page avec mon contenu en colonnes.\
Ca donne ça :

```
[wonderplugin_cond deviceinclude="Mobile"]

This content only shows on mobile and tablet devices.

[/wonderplugin_cond]
```

Ensuite j'ai eu un autre problème. C'est que mon pluggin qui fait du double scroll splitter s'affiche toujours, et que c'est très laid!

Là intervient le MU Plugin!

En gros c'est toi qui créer le plugin qui va décider pour tout les autres!\
Pourquoi? Parce qu'il va être chargé le premier et va dire aux autres les instructions que tu veux !\
Pratique !!

Donc voici la marche à suivre :\
D'abord tu vas dans ton dossier wp-content, ensuite tu créer un dossier mu-plugins\
Et dedans tu vas créer un fichier php, peu importe le nom que tu lui donne.\
Mais si comme moi tu veux faire une focntion qui gère les devices, bah tu l'appelle, device_conditionnal_plugin.php par exemple

\
Bon, et dedans qu'est-ce qu'on y met ?\
Tadaaaaaaa : Voilà mon code trouvé en farfouillant sur le oueb !

```
<?php 
function my_non_mobile_plugins() {
  return array(

    // ici tu mets le nom de tes plugins que tu veux pas voir sous mobile
    // avec nom-du-dossier/nom-du-fichier.php

    'csh-multiscroll/csh-multiscroll.php',

  );
}

function my_is_mobile() { 
  $is_mobile = false;
  if ( strpos($_SERVER['HTTP_USER_AGENT'], 'Mobile') !== false
    || strpos($_SERVER['HTTP_USER_AGENT'], 'Android') !== false
    || strpos($_SERVER['HTTP_USER_AGENT'], 'Silk/') !== false
    || strpos($_SERVER['HTTP_USER_AGENT'], 'Kindle') !== false
    || strpos($_SERVER['HTTP_USER_AGENT'], 'BlackBerry') !== false
    || strpos($_SERVER['HTTP_USER_AGENT'], 'Opera Mini') !== false
    || strpos($_SERVER['HTTP_USER_AGENT'], 'Opera Mobi') !== false
  ) {
    $is_mobile = true;
  }
  return $is_mobile;
}

add_filter( 'option_active_plugins', 'my_disable_plugins_for_mobiles' );

function my_disable_plugins_for_mobiles( $plugins ) {

  if ( ! my_is_mobile() ) {
    return $plugins; // for non-mobile device do nothing
  }

  $not_allowed = my_non_mobile_plugins(); // get non allowed plugins

  return array_values( array_diff( $plugins, $not_allowed ) );

}
?>
```

C'est beau hein ?!!\
Et du coup sur mobile ça marche trop bien maintenant, mon plugin vient plus foutre le bordel!!\
A savoir aussi : Le plugin ne s'affiche pas non plus dans le back office de wordpress sous mobile !

J'atais trop fière de mon truc, il fallait que je vous le partage !

Bisous aux lecteurs égarés
