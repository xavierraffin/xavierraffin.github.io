---
layout: post
title: Google maps passe Toulouse à la 3D ! Bientôt dans OpenStreetMap ?
created: 1358546657
comments: true
redirect_from: "/content/google-maps-passe-toulouse-à-la-3d-bientôt-dans-openstreetmap/"
excerpt_separator: <!--more-->
---
J'ai constaté très récemment que la vue satellite de Google Maps étaient passée en 3D isométriques sur les niveaux de zoom les plus importants.

Et le moins qu'on puisse dire c'est que <b><u>ça en jette</u></b> :

<center><img src="/sites/xavierraffin.com/files/fabre1.png" />
<img src="/sites/xavierraffin.com/files/fabre2.png" />
<i>Vue 3D <s>du canéropôle</s> de l'oncopôle, les laboratoires Fabre (<a href="https://maps.google.fr" target="_blank" >source Google Maps</a>)</i></center>
<br />

<!--more-->

<center><img src="/sites/xavierraffin.com/files/a380s-gmap.png" />
<i>Les A380 à Blagnac (<a href="https://maps.google.fr" target="_blank" >source Google Maps</a>)</i></center>

Si cette nouveauté couvre l’agglomération de Toulouse cela n'est pas encore le cas partout et en particulier à Paris !
Je suppose que cela ne saurait tarder puisque Google annonce régulièrement <a href="http://google-latlong.blogspot.fr/2012/11/imagery-update-tour-sites-around-world.html" target="_blank">de nouvelles villes couvertes par cette technologie</a>.

4 projections sont disponibles : Nord (par défaut), Sud, Est, Ouest.
Vous pouvez passer de l'une à l'autre en déplaçant le curseur N sur la roue de positionnement :

<center><img src="/sites/xavierraffin.com/files/vue-de-l-est.png" />
Le curseur permet de tourner autour de la carte<i> (<a href="https://maps.google.fr" target="_blank" >source Google Maps</a>)</i></center>

Vous constaterez de plus que ces angles de vues ont été pris quasi-au même moment.

Cela est dû à la méthode utilisée pour cette représentation à 45°, <b>le balayage aérien</b> :

<center><img src="/sites/xavierraffin.com/files/balayage-aerien.jpg" />
<i>La vue 3D utilise le balayage aérien (<a href="https://maps.google.fr" target="_blank" >source Google Maps</a>)</i></center>

La ville est cartographiée en plusieurs passages, très généralement effectués le même jour.
Les images de chaque passage sont ensuite fusionnés grâce à un découplage très complexe qui suit les rues afin d'éviter les changements d'angles au milieu des bâtiments (<a href="http://blog.alexandrecazaux.fr/2012/06/07/google-fait-le-choix-de-la-photogrammetrie/" target="_blank">plus de détails sur la technique utilisée </a>) :

<center><img style="border:1px solid" src="/sites/xavierraffin.com/files/changement-angle-gmap.png" />
<i>Les changements d'angles sont faits au milieu des voiries (OK il faut avoir l'oeil)</i></center>

Il ne s'agit pas là de véritable 3D, mais seulement d'une vue <i>"quadri-isométrique"</i>.

Le grand avantage de cette technique par rapport à de la vraie 3D est la <b>très grande compatibilité des navigateurs</b>.
En effet, si <a href="http://google-latlong.blogspot.fr/2011/10/step-inside-map-with-google-mapsgl.html" target="_blank">la vraie 3D arrive</a> sur les navigateurs et OS récents et compatibles WebGL, cela ne sera pas possible sur tous les périphériques avant un long moment.

Cette nouvelle vue 3D, n'utilise rien de nouveau :
La carte est toujours composée d'images carrées PNG juxtaposées (technique du type <a href="http://fr.wikipedia.org/wiki/Web_Map_Service" target="_blank">WMS</a>), ce que tous les navigateurs savent afficher depuis 1995 :

<center><img src="/sites/xavierraffin.com/files/kh.jpg" />
<i>Un exemple d'image qui compose le fond de carte : ce n'est pas une impression d'écran mais bien <a href="https://khms1.google.com/kh?v=68&src=app&x=264247&y=212153&z=19&s=Galile&deg=0" target="_blank">une image donnée par Google</a> à votre navigateur
(<a href="https://maps.google.fr" target="_blank" >source Google Maps</a>)</i></center>
<br />

<center><img style="border:1px solid" src="/sites/xavierraffin.com/files/WMTStilematrix.png" />
<i>Principe de décomposition en images d'une carte Web suivant les niveaux de zoom (<a href="http://depot.ign.fr/geoportail/api/doc/fr/developpeur/wmts.htmlr" target="_blank" >source IGN</a>)</i></center>

Par contre on note que le graphe des rues est déformé pour respecter l'effet de perspective.
Mais cette subtilité est pré-calculée côté serveur et ne change rien côté client.

Cela risque cependant de rendre difficile la réalisation d'application cartographique "maison" qui ne soient pas totalement Google Maps.
Si vous affichez votre propre fond cartographique, et que vous proposez de basculer sur la vue satellite Google vous n'allez pas pouvoir retrouver exactement le même point de vue.

C'est donc une grosse avancée pour les utilisateurs de Google Maps, qui renforce (et referme un peu plus) l'écosystème Google Maps, et c'est un nouveau chalenge à relever pour les projets concurrents.
<br />

<h1>La 3D aussi chez OpenStreetMap</h1>

Justement, du côté de la communauté OpenStreetMap, une initiative a débutée l'an dernier : <b>la modélisation en 3D par les utilisateurs !</b>

<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:13px; margin: 20px"><b>INFO DEBUTANT:</b></div>
<i>Dans OpenStreetMap, toutes les données sont modélisées en XML.
Plusieurs logiciels permettent la saisie de donnée assistée (Potlatch, JOSM, ...)
</i>
</div>
<br />

En effet, plusieurs recommandations sur la modélisation des bâtiments en 3D <a href="http://wiki.openstreetmap.org/wiki/Simple_3D_Buildings">ont été publiées</a>.

Notamment la manière de représenter les toitures :

<center><img src="/sites/xavierraffin.com/files/modelisation-de-toits_0.png" />
<i>Modélisation de toit "type" à l'aide d'un attribut XML (<a href="http://wiki.openstreetmap.org/wiki/Simple_3D_Buildings" target="_blank" >source OpenStreetMap</a>)</i></center>

<center><img style="border:1px solid" src="/sites/xavierraffin.com/files/osm-maison.jpg" />
<i>Modélisation d'une toiture par définition manuelle des arrêtes (<a href="http://wiki.openstreetmap.org/wiki/User:Aschilli/ProposedRoofLines" target="_blank" >source OpenStreetMap</a>)</i></center>

Enfin, un attribut "height" (hauteur), a été ajouté <a href="http://wiki.openstreetmap.org/wiki/Proposed_features/Building_attributes">à l'élément "building"</a> qui peut être relevé approximativement par les utilisateurs en comptant le nombre d'étage.

Concernant le rendu, <a href="http://wiki.openstreetmap.org/wiki/3D_Development">plusieurs initiatives de visualiseurs 3D</a> ont débutés :

<center><img src="/sites/xavierraffin.com/files/OSM-3D-1.png" />
<img src="/sites/xavierraffin.com/files/OSM-3D-2.png" />
<i>Des vues 3D du projet OSM-3D.org (<a href="http://wiki.openstreetmap.org/wiki/OSM-3D_Screenshots" target="_blank" >source OpenStreetMap</a>)</i></center>

Aucun de ces projets ne fonctionne directement dans le navigateur de manière native (seul <a href=" http://www.osm-3d.org/map.htm">OSM-3D</a> propose une visualisation web, mais avec un plugin Java).

En effet, les moteurs de rendus phares : Mapnik et Geoserver ne disposent pas encore de la capacité à créer des vues isométriques depuis ces nouvelles données.

<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:13px; margin: 20px"><b>INFO DEBUTANT:</b></div>
<i>Les moteurs de rendu sont des logiciels qui génèrent des images PNG de fond de carte à partir d'une base de donnée.
<br />

De tels logiciels sont indispensables à la création de fond de carte pour le Web.
</i>
</div>
<br />

Seul geoserver permet la génération d'image isométrique de manière expérimentale :

<center><img src="/sites/xavierraffin.com/files/pseudo3d-geoserver.png" />
<i>Géoserver permet une représentation isométrique par extrusion
(<a href="http://mapping-malaysia.blogspot.fr/2010/07/pseudo-3d-buildings-in-geoserver.html" target="_blank" >source mapping-malaysia.blogspot.fr</a>)</i></center>

Comme vous pouvez le voir ci-dessus, tous <u>les bâtiments ont la même hauteur</u>.
Geoserver se limite en effet, à étirer tous les bâtiments sur une hauteur identique définie une fois pour toute.
Il est donc impossible de représenter une ville de façon réaliste sans même parler des nouvelles toitures sophistiquées d'OSM.

<h1>Conclusion</h1>

La vue 3D isométrique Google Maps représente à mes yeux une avancée indéniable du confort utilisateur.
C'est une innovation qui tire encore par le haut les applications cartographiques web.

Côté libre, ça démarre et j'ai hâte de voir en combien de temps la communauté OSM Toulousaine sera capable de modéliser Toulouse en 3D !

Côté moteur de rendu, on voit qu'il ne manque pas grand chose mais qu'il reste beaucoup de travail <b>:-)</b>.

Si comme moi, vous trouvez le domaine de la cartographie web passionnant, je vous recommande <a href="http://www.paris-web.fr/2012/conferences/les-nouveaux-horizons-de-la-cartographie-sur-le-web.php" target="_blank">cette vidéo de la conférence de Benjamin Becquet à paris web 2012</a>.

Il y parle des grandes innovations à venir sur la cartographie web :
<ul>
<li>la 3D</li>
<li>le vectoriel : disposer d'un zoom fluide, de possibilité de rotation et perspective</li>
<li>l'indoor : la cartographie à l'intérieur des bâtiments</li>
</ul>
