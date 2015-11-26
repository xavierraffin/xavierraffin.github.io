---
layout: post
title: Nouveau site bêta transport public Montréal
created: 1373051836
---
La STM (organisme de transport public de Montréal) vient de sortir une bêta version de son nouveau site : <a href="http://beta.stm.info" target="_blank">http://beta.stm.info</a>

<h1>Les aspects fonctionnels</h1>

D'abord un concept de page d'accueil innovant et très réussi : une cartographie interactive plein écran.

<img src="/sites/xavierraffin.com/files/page-accueil-stm-beta.png" />

Ensuite une très bonne mise en avant des services transport par onglet (Itinéraire, horaires, plan, tarif) même si cela est déjà plus répandu.

<h1>Sur le plan technique</h1>

Reconnaissable par ces URL <i>"sites/default/files"</i>, le site est basé sur le CMS Drupal comme c'est le cas à Tisséo.
Ils ont sécurisé leurs pages d’administration sur https et filtrage IP (http://beta.stm.info/user renvoi vers https://beta.stm.info/fr/user qui est inaccessible), un choix prudent et intelligent.

Coté intégration, du très classique JQuery / JQuery UI / plugins JQuery pour la couche présentation.

Grosse déception sur le support navigateur, malgré la présente de la librairie modernizr <b>les navigateur IE < 8 sont purement et simplement exclus du service</b> :

<center>
<div style="border: solid 2px #CCC"><img src="/sites/xavierraffin.com/files/adieu-ie8.png" /></div>
<i>Les caribous ne sont pas cool avec les utilisateurs d'IE8 : (<b>si si c'est la page d'accueil !</b>)</i>
</center>

Autant vous dire que chez nous ce choix serait impensable <i>(d'autant plus qu'IE8 est notre navigateur par défaut, hum ...)</i>.

Côté cartographie, OpenLayers compose un fond en TMS ou WMTS servi par Apache.
Je reviendrais bientôt sur ces architectures (avec une grosse surprise !!!)

Je termine ce tour d'horizon par une grosse interrogation :

<blockquote>Quelle sera la tenue à la charge d'une telle page d'accueil ?</blockquote>

Avec 103 requêtes http, les serveurs risquent de souffrir les jours d'intempéries ou de grève.
Surtout qu'il y a un seul frontal qui sert le site et le fond cartographique.
<div style="margin: 5px 10px 10px;; font-size:0.8em;"><i>Peut-être suis-je médisant sur ce point car il y a peut-être un load balancer.
Mais tout sur le même domaine c'est quand même pas idéal pour monter en charge.</i>
</div>


Il sera donc intéressant de suivre l'évolution du site en version définitive et dans la durée.
