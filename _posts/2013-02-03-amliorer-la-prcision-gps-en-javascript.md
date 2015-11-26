---
layout: post
title: Améliorer la précision GPS en JavaScript
created: 1359926517
---
<div style="float:right">
<img src="/sites/xavierraffin.com/files/geolocalistion-javascript-html5_0.png" style="border:1px solid" alt="géolocalisation JavaScript HTML5 depuis un mobile" />
<center><b>Géolocalisation JavaScript</b>
<i>sources CC : <a href="http://www.b2bweb.fr/molokoloco/javascript-community-agnostic-logo-proposal/" target="_blank">b2bweb.fr</a>, <a href="http://commons.wikimedia.org/wiki/File:Geolocalisation_GPS_SAT.png" target="_blank">wikimedia</a>, <a href="https://commons.wikimedia.org/wiki/File:Multimedia-player-iphone.svg?uselang=fr" target="_blank">wikimedia</a></i></center>
</div>
L'arrivée d'HTML5 a été accompagné de l'apparition de nouvelles API JavaScript, permettant notamment d'accéder aux éléments hardware des terminaux : Webcam, Micro, Batterie, ... 

En particulier, il existe <a href="http://www.w3schools.com/html/html5_geolocation.asp" target="_blank">une API JavaScript de géolocalisation</a> permettant de récupérer ou de suivre, la position GPS d'un téléphone mobile depuis une page Web.

Malheureusement, la position récupérée n'est pas toujours de bonne qualité.

Cet article présente <b>une <u>méthode pur JavaScript</u> pour améliorer la précision des coordonnées récupérées</b>.

<div style="clear:right">
<br />
Si l'API JavaScript est assez basique (nous le verrons plus loin) elle a le mérite d'être supporté par la plupart des navigateurs mobile (et desktop) modernes :</div>

<center><img src="/sites/xavierraffin.com/files/api-geolocalisation-support.png" alt="tableau des navigateurs supportant la géolocalisation"/>
<i>Support de l'API par les navigateurs (<a href="http://caniuse.com/#feat=geolocation">source caniuse.com</a>)</i>
</center>
<br />

Comme je le disais en préambule, l'écart entre la position de l'utilisateur et celle renvoyée par le navigateur peut être très grand.
Cela rend inutilisable cette API dans beaucoup de contextes où la précision a de l'importance : comme la recherche d'objets autour de soi.

<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:32px; margin: 20px"><b>4km !</b></div>
<i>L’écart entre la position réelle et celle renvoyée par un <b>IPhone4</b> peut parfois dépasser <b>4000 mètres.</b>
</i>
<br />
</div>
<br />

<h1>Le Contexte : mobi.tisseo.fr</h1>

J'ai mis au point cette méthode pour la WebApp <a href="http://mobi.tisseo.fr/?nomobile=false">mobi.tisseo.fr</a> dont je suis responsable technique chez <a href="http://www.tisseo.fr" target="_blank">Tisséo</a>.

Cette application (site mobile) permet entre autre, la récupération de la liste des arrêts de bus et tramways autour de la position du téléphone mobile :
<center><img src="/sites/xavierraffin.com/files/geoloc690.png" alt="géolocalisation sur mobi.tisseo.fr"/></center>

Pour cette fonctionnalité, il est primordial que la précision de géolocalisation soit de 150 mètres ou moins.
Notre parti pris est même de ne donner aucun résultat si on ne parvient pas à descendre en dessous de 166 mètres. (ce qui sera le cas sur un Android avec le GPS désactivé) :
<blockquote>Votre position n'a pu être déterminée avec une précision suffisante.</blockquote>

Nous avons éprouvé notre code de géolocalisation sur un large panel de téléphone de test : IPhone3/4/5, IPad, XPeria X10, Galaxy Note, HTC Desire HD, Samsung Bada, Nokia WindowsPhone 7, ...

<h1>Les défauts de l'API JavaScript</h1>

Pour que vous puissiez comprendre, je vous présente l'API JavaScript et vous explique les problèmes rencontrés.

Seulement deux fonctions sont disponibles :
<ul>
<li><u>getCurrentPosition</u> : permet de récupérer la position GPS une seule fois</li>
<li><u>WatchPosition</u> : permet de suivre la position GPS à intervalle régulier</li>
</ul>

<h2>getCurrentPosition</h2>

C'est cette fonction qui donne les plus mauvais résultats.

Elle dispose de seulement 3 paramètres :
<ul>
<li><u>enableHighAccuracy</u> : true/false, indique si l'on souhaite obtenir une position précise.
Malheureusement, cela ne garanti pas un appel GPS sur tous les téléphones</li>
<li><u>maximumAge</u> : fraicheur maximale de la position en cache
Ce critère n'est pas respecté par certains téléphones (IPhone en particulier)</li>
<li><u>timeout</u> : durée après laquelle la callback d'erreur est appelé si aucune position n'a été trouvé</li>
</ul>

S'il n'y a pas d'erreur une fonction callback de votre choix est appellée avec un paramètre contenant les informations suivantes :
<ul>
<li><u>latitude, longitude</u> : les coordonnées GPS en WGS84</li>
<li><u>altitude (optionnel)</u> : pour les alpinistes et aviateurs</li>
<li><u>accuracy</u> : <b>très important</b>, donne la précision estimée de la mesure.
Heureusement cette valeur est "en général" assez honnête (comprenez proche de la vérité).</li>
</ul>

<javascript title="Code d'exemple">
var options = {
    timeout : 30000,
    enableHighAccuracy : true,
    maximumAge : 1000
};
navigator.geolocation.getCurrentPosition(showPosition, showError, options);

function showPosition(position)
 {
    alert( "Latitude: "   + position.coords.latitude +
           "Longitude: "  + position.coords.longitude +
           "Accuracy: "   + position.coords.accuracy );
}
function showError(err)
{
    alert("Error no : " + err.code);
}
</javascript>

Avec cette fonction, vous ne pouvez donc <b><u>pas être certain</u></b> que la position obtenue soit précise, ni récente sur tous les terminaux.
La position renvoyée peut être ancienne de plusieurs minutes et peut donc être très éloignée de votre position actuelle si vous venez de prendre un bus par exemple.

Vous pouvez peut-être vous en sortir avec plusieurs appels successifs à getCurrentPosition, mais c'est <b>sans garantie</b> et cela peut prendre du temps :
<blockquote>Un timeout trop court ne vous donnera pas de résultat, trop long, vous prenez le risque de faire attendre l'utilisateur</blockquote>

<h2>WatchPosition</h2>

L'autre fonction de l'API permet de suivre la position de l'internaute à intervalle régulier.

Les options sont les mêmes. La différence est le fait que la callback est appellé <s>au bon vouloir de l'OS</s> à chaque changement de position détecté par l'OS.

L'autre différence et avantage de taille c'est que vous pouvez interrompre le suivi de position par un appel à la fonction <i>"clearwatch"</i>.

<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:16px; margin: 20px"><b>La confiance
règne</b></div>
<i>Intuitivement, pour suivre une position on se dit que le navigateur ne pourra plus tricher : il doit appeler le GPS.
Et pourtant ...
</i>
<br />
</div>
<br />

Mes tests ont montrés que la première position obtenue (lors du premier appel à la fonction callback) était souvent mauvaise.
Cette première réponse est obtenue très rapidement (ce qui renforce ma conviction que l'appareil sort ça du cache) alors que les suivantes prennent du temps à venir.

Pire, j'ai même constaté que parfois sur iOS la première position était mauvaise, mais l'accuracy bonne (65m sur un IPhone) : dans ce cas <b><u>le téléphone vous ment</u></b>.

Inversement les Android semblent plus honnêtes, mais ils ne donnent jamais une précision de moins de 500m si le GPS est désactivé (et vous n'avez aucun moyen de le savoir en JavaScript).

Pour comprendre ces comportements, j'ai construit une <a href="/sites/xavierraffin.com/files/test-geoloc.html" target="_blank">page de test</a> et je me suis baladé dans Toulouse :

<center><img src="/sites/xavierraffin.com/files/test-geoloc.png" style="border:1px solid" alt="Résultat d'un test sur le terrain"/>
<i>Résultat d'un test sur le terrain</i>
</center>
<br />

Lors du test ci dessus, j'ai récupéré successivement les positions 1, 2, 3 et 4.
L'accuracy a diminué au fur et à mesure des résultats.
On voit que la première position obtenue est très éloignée de ma position réelle : <b>si j'avais donné les arrêts autour de moi avec cette position, le résultat aurait été très mauvais !</b>

<h1>Construction de la méthode</h1>

Après ce qu'on a vu précédemment, on peut déduire les éléments suivants:
<ul>
<li>il faut utiliser watchposition</li>
<li>il ne faut pas faire confiance à la première position sauf si elle est inférieur à 65m (cas des desktop)</li>
<li>dans tout les cas on doit abandonner après X secondes (disons 30 secondes) : si aucune position n'est donnée (timeout à X secondes) ou si les accuracy dépassent un certain seuil (166m dans mon cas)</li>
</ul>

Voici donc la stratégie que j'ai mis au point :

<center><img src="/sites/xavierraffin.com/files/algo-geoloc.png" style="border:1px solid" alt="Graphique d'acceptation de l'erreur de géolocalisation"/>
<i>Critère d'arrêt ou d'abandon de l'algorithme</i>
</center>
<br />

Le critère d'abandon de l'algorithme est donc représenté par <span style="color:blue"><b>la courbe bleue</b></span> (limite temporelle).
<b>La courbe pointillée</b> (limite de qualité), représente les valeurs de précision insuffisantes pour être prises en compte.

En résumé :
<blockquote>Après 30 secondes, si on a pas récupéré de position ou si on a récupéré des positions trop imprécises on abandonne.</blockquote>

Si à l'inverse on trouve une position en dessous du seuil limite rapidement, <u>il peut être intéressant d'attendre encore un peu afin de voir si on peut faire encore mieux</u>.

C'est l'idée de <span style="color:red"><b>la courbe rouge</b></span> : <b>on diminue nos exigences au fur et à mesure que le temps passe</b>.

<u>Exemple :</u> on a trouvé une position précise à 100 mètres au bout d'une seconde, alors :
<ul>
<li><u>Cas 1 :</u><b>on trouve une position précise à 50 mètres au bout de 2 secondes</b> : ca valait le coup d'attendre, on s'arrete la et on affiche le résultat</li>
<li><u>Cas 2 :</u><b>on ne trouve pas de position plus précise au bout de 5 secondes </b> : ce n'est pas la peine de faire attendre l'utilisateur plus longtemps, 100 mètres ce n'est pas si mal</li>
</ul>

Sur le graphique précédent, j'ai représenté un seuil d'acceptation linéaire, mais vous pouvez très bien choisir quelque chose de différent :

<center><img src="/sites/xavierraffin.com/files/autre-politique-geoloc.png" style="border:1px solid" alt="Graphique d'acceptation de l'erreur de géolocalisation"/>
<i>Autres choix possibles de seuil d'acceptation</i>
</center>
<ul>
<li><u>par palier :</u> très facile à coder : <b>c'est ce que j'ai choisi</b></li>
<li><u>fonction continue deux fois dérivable :</u> pour les joueurs</li>
<li>... etc ...</li>
</ul>
<br />

La subtilité du code JavaScript est que comme vous ne pouvez pas savoir quand (et même si) watchPosition vous retournera une valeur.
Donc vous devez lancer une tache de supervision à part avec un "<i>setInterval</i>".

Pour voir la mise en pratique et le code rendez-vous sur la <a href="/sites/xavierraffin.com/files/test-geoloc.html">page de test</a>.
<i>(Je commenterais plus le code d'ici quelques temps, promis :-)</i>

<h1>Conclusion</h1>

La mise au point de cette méthode a pris beaucoup de temps, car si elle n'est pas complexe elle se base sur des observations de terrains longues et fastidieuses.
Une voie d'amélioration serait peut-être la prise en compte des user-agent pour une adaptation au terminal détecté.
<i>Peut-être le ferais-je si j'en ai le temps et si je veux <s>devenir célèbre</s> remplir mon Github.</i>

Maintenant les observations faites lors des tests m'amènent à penser que certains fournisseurs d'OS mobile dégradent volontairement l'expérience de la WebApp pour pousser l'utilisateur à préférer une application native.
C'est particulièrement le cas pour l'une de ces compagnies (dont je tairais le nom, mais dont le logo est une pomme) qui dégrade un peu plus la qualité et la précision des coordonnées XY <b>à chaque sortie de nouveau modèle</b>.

Dans la bataille HTML5 vs application native, la précision JavaScript de géolocalisation pourrait être un bon indicateur de tendance.
