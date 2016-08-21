---
layout: post
title: Application mobile Tisséo v2
comments: true
excerpt_separator: <!--more-->
---

Aujourd'hui est sortie l'application mobile Tisséo V2 sur iOS et Android.

Cette version majeure a demandé des mois de travail et apporte beaucoup de nouveautés et de nombreuses améliorations.

Comme vous le savez peut-être, [j'ai quitté Tisséo au mois de mai](http://xavierraffin.com/2016/05/16/changement-de-voie-et-avenir-opendata-tisseo/) et ce projet sera ma dernière réalisation pour les usagers des transports toulousains.

# Listes des nouveautés

* un widget !
* plans de lignes
* fond de plan plus lisible, plus joli et plus rapide
* horaires "en temps réel" sur 15 jours
* disponibilité des fiches horaires hors ligne
* de nombreuses améliorations esthétiques et de performance

<!--more-->

<style  type="text/css">
.thumbnail {
  float:left;
  padding-right: 0.7em;
}
.screenshot, .thumbnail {
  text-align:center;
}
.thumbnail img, .screenshot img {
    width:340px;
    margin-bottom:0;
}
.screenshot img {
    margin-left: auto;
    margin-right: auto
}
.thumbnail .click, .screenshot .click {
    color:#000 !important;
    text-decoration:italic;
}
.thumbnail .title, .screenshot .click {
    font-weight:bold;
}
.clearfix:after {
  content:'';
  display:block;
  clear:both;
  padding-bottom:1em;
}
</style>

# Nouveau fond de plan

C'est peut-être la nouveauté la plus visible, le fond de plan a été totalement renouvelé.

Toujours basé sur OpenStreetMap, la définition du plan a été augmentée pour améliorer la lisibilité des polices de caractères sur les terminaux de résolution élevé.

Ensuite, le style de la carte a été revu pour augmenter le contraste et pour plus d'élégance.

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/plan-avant.png"><img src="/public/images/appli-tisseo-v2/plan-avant.png"></a>
<span class="title">Plan avant</span><br>
<a href="/public/images/appli-tisseo-v2/plan-avant.png" class="click">(Cliquez pour agrandir)</a>
</div>
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/plan-apres.png"><img src="/public/images/appli-tisseo-v2/plan-apres.png"></a>
<span class="title">Plan après</span><br>
<a href="/public/images/appli-tisseo-v2/plan-apres.png" class="click">(Cliquez pour agrandir)</a>
</div>
</div>

Vous pouvez constater la lisibilité des noms de rues _(cela ne "bave" plus en limite de niveau de zoom)_ :
<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/centre-avant.png"><img src="/public/images/appli-tisseo-v2/centre-avant.png"></a>
<span class="title">Plan centre avant</span><br>
<a href="/public/images/appli-tisseo-v2/centre-avant.png" class="click">(Cliquez pour agrandir)</a>
</div>
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/centre-apres.png"><img src="/public/images/appli-tisseo-v2/centre-apres.png"></a>
<span class="title">Plan centre après</span><br>
<a href="/public/images/appli-tisseo-v2/centre-apres.png" class="click">(Cliquez pour agrandir)</a>
</div>
</div>

Toutes ces améliorations augmentent le poids de la carte et augmente la bande passante utilisée. C'est pourquoi deux mécanismes ont été mis en places :
* trois niveau de définition différents sont utilisés en fonction de la densité de pixel de votre appareil.
* un cache hors ligne a été implémenté pour économiser la bande passante de l'utilisateur. La taille de ce cache est de 50 mo par défaut mais peut-être modifié dans les paramètres. Le cache est très intelligent et s'adaptera aux zones visités les plus fréquemment par l'utilisateur.

Pour ceux que les aspects techniques intéresse sachez que le cache serveur renseigne des headers Etags et que si l'image n'a pas changé un simple code http 304 sera renvoyé. On se base de plus sur la date du fichier local et une durée d'expiration pour savoir si on doit requêter le serveur : si oui et qu'un 304 est obtenu on met à jour la date du fichier.

La stack cartographique est principalement basée sur PostgreSQL, Geoserver et Mapproxy (j'en ai parlé plus en détail [ici](http://xavierraffin.com/2013/10/09/innovation-tisso-un-plan-interactif/#socle-technique))

# Plans de lignes

Dans le menu principal, vous constaterez un nouvel item "Plans de lignes" :

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/nouveau-menu.pngg"><img src="/public/images/appli-tisseo-v2/nouveau-menu.png"></a>
<span class="title">Menu principal</span><br>
<a href="/public/images/appli-tisseo-v2/nouveau-menu.png" class="click">(Cliquez pour agrandir)</a>
</div>
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/plan-des-lignes.png"><img src="/public/images/appli-tisseo-v2/plan-des-lignes.png"></a>
<span class="title">Menu plan des lignes</span><br>
<a href="/public/images/appli-tisseo-v2/plan-des-lignes.png" class="click">(Cliquez pour agrandir)</a>
</div>
</div>

Vous pourrez remarquez en haut de ce menu un bouton "Télécharger le plan détaillé du réseau" qui permet d'obtenir le plan PDF du réseau complet.
Ce n'est pas forcément très adapté à un affichage sur mobile, mais cela a été demandé par de nombreux utilisateurs.

Si vous sélectionner une ligne dans la liste, alors vous arriverez sur une page comme celle-ci :

<div class="screenshot">
<a href="/public/images/appli-tisseo-v2/trace-de-ligne.png">
<img src="/public/images/appli-tisseo-v2/trace-de-ligne.png">
</a>
<span class="title">Tracé d'une ligne</span><br>
<a href="/public/images/appli-tisseo-v2/trace-de-ligne.png" class="click">(Cliquez pour agrandir)</a>
</div>

Vous pouvez afficher la ligne pour chaque terminus en cliquant sur le bouton en haut de l'écran.

_Notez que comme l'affichage des arrêts, l'affichage des tracés de ligne est instantané car les tracés sont sauvegardés hors ligne sur votre mobile et synchronisés de manière transparente lorsqu'ils changent._

Un nouveau bouton donne accès à la fiche horaire PDF :

<div class="screenshot">
<a href="/public/images/appli-tisseo-v2/fh-pdf.pngg">
<img src="/public/images/appli-tisseo-v2/fh-pdf.png">
</a>
<span class="title">Menu "plans de ligne"</span><br>
<a href="/public/images/appli-tisseo-v2/fh-pdf.png" class="click">(Cliquez pour agrandir)</a>
</div>

Encore une fois ces PDF ne sont pas optimisés pour le mobile, mais la demande des utilisateurs a été très forte.

Les plans de lignes PDF, et les tracés de lignes sont accessibles depuis d'autres écrans de l'application (voir section suivante).

# Nouveau écrans de prochains passages

La page la plus consulté de l'application (65% des vues) est la page de prochains passage.

Les nouveaux écrans présentent le mode de transport, de nouveaux pictogrammes, et un menu intercalaire se développe si on clique sur une ligne :

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/prochainspassages-avant.png"><img src="/public/images/appli-tisseo-v2/prochainspassages-avant.png"></a>
<span class="title">Prochains passages avant</span><br>
<a href="/public/images/appli-tisseo-v2/prochainspassages-avant.png" class="click">(Cliquez pour agrandir)</a>
</div>
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/prochainspassages-apres.png"><img src="/public/images/appli-tisseo-v2/prochainspassages-apres.png"></a>
<span class="title">Prochains passages après</span><br>
<span style="text-decoration:italic">C'est quand même plus joli hein ?</span><br>
<a href="/public/images/appli-tisseo-v2/prochainspassages-apres.png" class="click">(Cliquez pour agrandir)</a>
</div>
</div>

Le menu permet de :
* mettre en favori l'élément
* consulter les horaires temps réel des 15 prochains jours à cet arrêt (voir section suivante)
* afficher le tracé de la ligne
* voir les alertes de cette ligne (s'il y en a)

# Horaires des 15 prochains jours

Une des demandes régulière des utilisateurs était de pouvoir voir plus de deux prochains passages, comme cela était possible sur le site tisseo.fr

Nous avons donc ajouté un nouvel écran accessible depuis la vue prochains passage (voir section précédente) :

<div class="screenshot">
<a href="/public/images/appli-tisseo-v2/horaire-journee.png">
<img src="/public/images/appli-tisseo-v2/horaire-journee.png">
</a>
<span class="title">Horaires des 15 prochains jours</span><br>
<a href="/public/images/appli-tisseo-v2/horaire-journee.png" class="click">(Cliquez pour agrandir)</a>
</div>

Les prochains horaires sont en temps réel (si l'information est disponible) et deviennent théoriques lorsqu'on s'éloigne dans le futur.

Comme pour le calcul d'itinéraire, il est possible de consulter les informations jusqu'à 15 jours maximum dans le futur.

# Widget

Demandé par de nombreux utilisateurs, l'application se dote d'un widget :

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/widget.png"><img src="/public/images/appli-tisseo-v2/widget.png"></a>
<span class="title">Widget Android</span><br>
<a href="/public/images/appli-tisseo-v2/widget.png" class="click">(Cliquez pour agrandir)</a>
</div>
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/widget-ios.png"><img src="/public/images/appli-tisseo-v2/widget-ios.png"></a>
<span class="title">Widget iOS</span><br>
<a href="/public/images/appli-tisseo-v2/widget-ios" class="click">(Cliquez pour agrandir)</a>
</div>
</div>

Ce widget présente les prochains passages favoris triés par distance (si l'utilisateur accepte de donner sa position).
Afin d'économiser la batterie, ce widget ne se rafraîchit qu'au clic sur les flèches.

Ce widget peut être redimensionné verticalement.

Pour le moment, il n'y a qu'un seul widget mais s'il y a de la demande il sera possible d'en créer de nouveaux (n'hésitez pas à soliciter l'équipe).

Par exemple on pourrait imaginer des widget de calcul d'itinéraire ou des prochains passages à un unique arrêt plus compact.

# Autres améliorations

Globalement, une refonte esthétique générale a été apportée :
* polices de caractères
* pictogrammes et icônes
* mise en page des écrans optimisés
* effets d'animations et de transition

<div class="clearfix">
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/jaures-avant.png"><img src="/public/images/appli-tisseo-v2/jaures-avant.png"></a>
<span class="title">Popup avant</span><br>
<a href="/public/images/appli-tisseo-v2/jaures-avant.png" class="click">(Cliquez pour agrandir)</a>
</div>
<div class="thumbnail">
<a href="/public/images/appli-tisseo-v2/jaures-apres.png"><img src="/public/images/appli-tisseo-v2/jaures-apres.png"></a>
<span class="title">Popup après</span><br>
<a href="/public/images/appli-tisseo-v2/jaures-apres.png" class="click">(Cliquez pour agrandir)</a>
</div>
</div>

Sur cet exemple, vous constaterez les nouveaux pictogrammes et polices de caractère des cartouches de ligne (A, 16, NOCT, ...).
Vous pouvez également remarquer que nous avons changé le bouton "Y aller" pour le rendre plus visible.

Des amélioration techniques non visibles ont étés apportés comme une meilleure prise en compte des arrêts non desservis en cas de déviation.

Enfin le support Android 6 et iOS 9 a été amélioré.

# Conclusion

__5 étoiles :__
L'application vous plaît ? Si vous voulez la voir continuer à évoluer mettez cinq étoiles sur Apple Store ou Google Play.
En plus de faire plaisir à l'équipe de développement, cela aide vraiment en interne à vendre le projet et à convaincre les décideurs de l'importance de ce projet et des médias d'informations voyageur en général.

Grâce à une équipe interne de passionnés, à l'utilisation (et la contribution) massive de l'opensource et de l'opendata la qualité des outils d'une ville comme Toulouse pour le transport public est vraiment excellente pour un investissement très réduit.

D'un autre côté la fréquentation de l'application mobile et des autres applications OpenData explose véritablement (avec la 4G dans le métro cela ne va pas s'arrêter). Signe que cela rend service à de plus en plus de monde.
Je suis convaincu que cela encourage à prendre les transports publics et à rendre notre ville plus "verte".

Il est donc vraiment important que vous manifestiez votre soutient pour que l'équipe puisse rester indépendante sur la technique et sur les choix d'expérience utilisateur.

Dans une grande structure publique avec un fort lien à la politique, __il y a toujours un risque que tout soit remis en cause__.

_Vous pouvez aussi écrire directement à digital@tisseo.fr si vous avez des remarques, des idées ou que vous voulez les encourager ;-)_

## Le mot de la fin

Cet article sera très probablement mon dernier sur les outils de Tisséo.

Je redis à toute l'équipe mon plaisir d'avoir travaillé avec eux et au plaisir de prendre une bière à la méca ;-)
