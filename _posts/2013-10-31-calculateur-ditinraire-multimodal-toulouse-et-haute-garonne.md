---
layout: post
title: Calculateur d'itinéraire multimodal Toulouse et Haute-Garonne
created: 1383258714
comments: true
redirect_from: "/content/calculateur-itineraire-multimodal-toulouse-haute-garonne/"
---
<link rel="stylesheet" href="http://cimm.tisseo.fr/direct-mb-cimm-1.0/cimm.css" type="text/css" media="all" />
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" ></script>
<script type="text/javascript" src="http://openlayers.org/api/OpenLayers.js" ></script>

Après <a href="/content/plan-interatif-javascript-tisseo">le plan interactif Tisséo</a>, j'ai le plaisir de vous présenter un autre projet réalisé avec <a href="http://xavierraffin.com/content/pr%C3%A9sentation-de-synthese">SYNTHESE</a> en préparation depuis plusieurs mois à Tisséo : le <b>Calculateur d'Itinéraire Multi-Modal</b> (CIMM).<br><br>

excerpt_separator

Ce projet, entièrement réalisé par nos équipes Tisséo est le fruit d'un partenariat entre plusieurs organisations publiques : l'état, la région Midi-Pyrennées, le département de la Haute-Garonne, Toulouse-Métropôle, et Tisséo.<br><br>
<div style="float:right">
<center>
<img src="/sites/xavierraffin.com/files/emprise-cimm.png" /><br>
<i>Le périmètre du calculateur est plus grand que le département</i></center>
</div>
Ce calculateur permet d'effectuer des itinéraires en mixant:<ul>
<li>Train SNCF</li>
<li>Transport Tisséo</li>
<li>Cars Arcs en Ciel</li>
<li>Cars du Conseil Régional</li>
<li>Bus de Colomiers et de Muret</li>
<li>VélôToulouse</li>
<li>Vélo personnel</li>
<li>Voiture personnelle</li>
</ul>
<div style="clear:both" /><br>
Pour voir en détail comment tout ceçi peut être combiné, je vous invite à essayer :
<img src="/sites/xavierraffin.com/files/essayezle.png" />
<table style="margin:0;padding:0;border:0;border-collapse:separate;background:#FFF"><tr><td style="margin:0;padding:0;border:0;background:#FFF;vertical-align: top"><img src="/sites/xavierraffin.com/files/allezy_0.png" /></td>
<td style="margin:0;padding:0;border:0;background:#FFF"><div id="div_load_calculateur"></div></td></tr></table>
<script src="http://cimm.tisseo.fr/ci-multimodal-v2.0" type="text/javascript" ></script>
<center><i>Le formulaire de calcul d'itinéraire multimodal</i></center><br><br>

Comme vous pouvez le voir, ce calculateur est directement intégrable dans n'importe quel site via un widget JavaScript : c'est <i>une marque blanche</i><br>
<i><b>ATTENTION : </b>L'intégration du widget est aujourd'hui réservée à des sites explicitement autorisés, qui sont aujourd'hui exlusivement des sites d'organismes publics (je dispose d'un petit passe droit ;-)</i><br><br>

En plus de l'incontournable <a href="http://xavierraffin.com">xavierraffin.com</a>, le calculateur est disponible sur les sites suivants :<ul>
<li><a href="http://www.tisseo.fr/calculateur-multimodal" target="_blank">tisseo.fr</a></i>
<li><a href="http://www.toulouse-metropole.fr/calculateur_itineraire" target="_blank">toulouse-metropole.fr</a></li>
<li><a href="http://www.haute-garonne.fr/itineraire" target="_blank">haute-garonne.fr</a></li>
<li><a href="http://www.sicoval.fr/outils/transports.html " target="_blank">sicoval.fr</a></li>
<li><a href="http://www.mairie-balma.fr/trajet.html" target="_blank">Mairie de Balma</a></li>
<li><a href="http://www.ville-colomiers.fr/index.php/Se-d%C3%A9placer?idpage=113" target="_blank">Mairie de Colomiers</a></li>
<li><a href="http://www.cornebarrieu.com/cimm.html" target="_blank">Mairie de Cornebarieu</a></li>
<li><a href="http://www.plaisancedutouch.fr/articles_calc.asp?idrubrique=112&idpage=363" target="_blank">Mairie de Plaisance du Touch</a></li>
<li><a href="http://www.ville-aucamville.fr/fr/vie-pratique/transports/calculateur-tisseo.html" target="_blank">Mairie d'Aucamville</a></li>
<li><a href="http://www.labarthesurleze.com/se_deplacer_autrement.vdom" target="_blank">Mairie de Labarthe sur Lèze</a></li>
<li><a href="http://www.saint-genies-bellevue.fr/web/147-tisseo.php" target="_blank">Mairie de Saint Genies Bellevue</a></li>
<li><a href="http://www.escalquens.fr/escalquens-ma-ville/transports/" target="_blank">Mairie d'Escalquens</a></li>
<li><a href="http://www.mairie-seilh.fr/pages/page.php?page=579" target="_blank">Mairie de Seilh</a></li>
<li><a href="http://www.fonsorbes.fr/Calculateur-d-itineraires-Tisseo.html" target="_blank">Mairie de Fonsorbe</a></li>
<li><a href="http://www.mairie-launaguet.fr/fr/cadre-vie/transports/calculateur-tisseo.html" target="_blank">Mairie de Launaguet</a></li>
<li><a href="http://www.villeneuve-tolosane.fr/web/117-calculateur-d-itineraire.php" target="_blank">Mairie de Villeneuve-Tolosane</a></li>
<li><a href="http://www.gratentour.fr/transport.vdom" target="_blank">Mairie de Gratentour</a></li>
<li>et la liste s'allonge toutes les semaines...</li>
</ul>

<h1>Explications techniques</h1>

<h2>Intégration dans un site web</h2>
Techniquement, le calculateur est hébergé et administré chez Tisséo, et la technique d'intégration retenue pour ce widget s'appelle le <b>JSONP</b> :

<center><img src="/sites/xavierraffin.com/files/integ-cimm-small.png" />
<i>Intégration du calculateur dans une page web</i>
</center>
<br>
Sur la page du "site hôte", il suffit d'ajouter le code HTML suivant :

<pre>
<script type="text/javascript" src=".../jquery.min.js" ></script>
<script type="text/javascript" src=".../OpenLayers.js" ></script>
<link rel="stylesheet" href="http://cimm.tisseo.fr/direct-mb-cimm-1.0/cimm.css" type="text/css"/>
<script src="http://cimm.tisseo.fr/ci-multimodal-v2.0" type="text/javascript"></script>
<div id="div_load_calculateur"></div>
</pre>

<u>Les éléments importants sont :</u><br>

La balise d'accroche du widget : c'est à cet endroit de la page que va s'insérer le formulaire :

<pre>
<div id="div_load_calculateur"></div>
</pre>

Le script de chargement du formulaire : il charge les données depuis les serveurs Tisséo et remplace la balise précédente par le formulaire
<pre>
<script src="http://cimm.tisseo.fr/ci-multimodal-v2.0" type="text/javascript"></script>
</pre>
Vous remarquerez que le domaine utilisé içi est <b><i>cimm.tisseo.fr</i></b> : ce n'est pas le domaine du site hôte.<br><br>
C'est cela qui permet de contourner les restrictions de sécurité "Cross Domain" des navigateurs.<br><br>
En effet, une fois le formulaire chargé, celui-ci dialogue avec le serveur Tisséo (pour l'autocomplétion, et l'affichage des résultats) sans rechargement de la page.<br><br>

Or le JavaScript interdit toujours la communication Ajax avec un autre domaine <u>sauf</u> dans le cas d'un chargement d'un script de ce domaine par le HTML.
C'est cette technique qu'on appelle le <a href="http://en.wikipedia.org/wiki/JSONP" target="_blank">JSONP</a>.<br><br>

<i><u><b>Note:</b></u> Il existe une nouvelle technique normalisé par le W3C qui permet de faire la même chose plus simplement : le <a href="http://en.wikipedia.org/wiki/Cross-origin_resource_sharing" target="_blank">CORS</a>.<br>
Cependant, cette technique n'est <a href="http://caniuse.com/cors" target="_blank">pas supportée par les plus vieux navigateurs</a> (notament IE)</i>
<br><br>
Enfin, concernant l'apparence du widget, le site hôte peut :
<ul>
<li>soit utiliser la CSS prédéfinie par Tisséo (comme c'est le cas sur cette page)</li>
<li>soit modifier cette CSS et la charger localement : cela permet par exemple de changer les couleurs et les dimensions</li>
</ul>
<br>
<h2>Spécificités du calcul mixte</h2>
<br>
Une des grosses nouveautés fonctionnelle introduite par ce calculateur est la possibilité d'effectuer des calculs mixtes <i>"Voiture + Piéton"</i> (ou <i>"Vélo + Piéton"</i>) de manière automatique.
<br /><br />
Il faut comprendre içi que <u>c'est le calculateur qui choisi le point de rupture entre les modes</u>.<br /><br />


<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:30px; margin: 15px"><b>Trop de voiture !</b></div>
<i><br />Quand on compare les temps de trajets <i>"Routier"</i> et <i>"Transport en Commun"</i>, il sera presque toujours plus rapide de prendre la voiture.
</i>
<br /><br />
<i>C'est généralement faux en pratique car <b>les bouchons pénalisent le temps de trajet voiture</b></i>
</div><br /><br />

Pour éviter d'encourager l'utilisation de la voiture individuelle, nous avons introduit des notions "politiques" :
<ul>
<li><u>un ratio</u> : on limite la proportion de trajet effectuée en voiture</li>
<li><u>une mesure de densité d'offre</u> : à 4 heures du matin, ou dans un village de montagne, les trajets "Transport en commun" sont souvent <s>assez ridicules</s> peu performants.<br>
Dans ces cas là, il faut donc autoriser un plus grand nombre de kilomètres en voiture pour obtenir un temps de trajet acceptable.</li>
</ul><br />
Voici ce que ça donne en pratique :<br>

<center>
<img src="/sites/xavierraffin.com/files/influence-offre.png" /><br>
<i>Influence de la densité d'offre sur le trajet en voiture (en noir)</i>
</center>
<br>
Sur la figure précédente, on voit que lorsque l'offre de Transport public est plus forte le calculateur propose un trajet en voiture plus court.
<br><br>
Voyons maintenant plus en détail comment nous avons mis cela en musique :<br>
<h2>Architecture hybride</h2>
<br>
Les choix fonctionnels effectués pour ce calculateur, étant parfois éloigné de la roadmap <a href="http://xavierraffin.com/content/pr%C3%A9sentation-de-synthese">SYNTHESE</a> et du cap fixé par ça communauté, il nous a fallu introduire certaines fonctionnalités dans une surcouche.<br><br>

Concrètement, cela signifie que les requêtes adressées au serveur Tisséo transitent par un <i>"proxy applicatif"</i> qui enchaine les appels à SYNTHESE et les enrichit de données tierces :<br><br>

<center>
<img src="/sites/xavierraffin.com/files/cimm-symfony_0.png" /><br>
<i>Symfony compose avec "intelligence" les réponses aux requêtes utilisateurs</i>
</center><br>

Pour le mode <i>"Transport en Commun"</i>, le Symfony se contente de transmettre la requête à SYNTHESE et de renvoyer la réponse à l'internaute.<br><br>

Pour les trajets mixtes <i>"Routier"</i> + <i>"Transport en Commun"</i> Symfony interroge plusieurs services SYNTHESE, prend des décisions et compose une réponse à l'internaute: 
<ol>
<li><u>Requête de densité d'offre:</u> dans quel rayon autour du point de départ et dans un intervalle d'une heure après l'heure de départ demandée y a-t-il 50 services au départ ?</li>
<li><u><b>Si rayon > 1km :</b> Requête de trajet mixte <i>"Transport en Commun"</i> + <i>"Routier"</i> :</u> calcul d'itinéraire en limitant la distance parcourue en voiture à la distance obtenue précédement (avec application d'un ratio et en s'assurant que le rapport distance en voiture / distance total reste inférieur à 1/3)<br>
<li><u><b>Si rayon < 1km :</b> Requête de trajet <i>"Transport en Commun"</i> </i> :</u> calcul d'itinéraire en Transport en Commun seulement : <u>en effet, on ne prend pas sa voiture pour faire 500 mètres</u><br>
</li>
</ol>
<br>
<center>
<img src="/sites/xavierraffin.com/files/density-service-principle.png" /><br>
<i>Principe de fonctionnement du service de "Densité de Service"<br>
que j'ai codé <a href="https://extranet.rcsmobility.com/projects/synthese/wiki/Density_Service" target="_blank">directement dans le code de SYNTHESE</a></i>
</center>
<br>
<br>
Autre exemple mixte <i>"Routier"</i> + <i>"Transport en Commun"</i>  mais avec un rabattement sur les parcs relais
<ol>
<li><u>Requête spatiale postGIS :</u> pour trouver les 5 parcs relais les plus proches à vol d'oiseau</li>
<li><u>5 Requetes de calcul routier vers les XY obtenus:</u> pour trier dans l'ordre les parcs relais les plus proches <b>par la route</b> (ce qui peut être très différent du résultat à vol d'oiseau suivant la topologie (peu de ponts sur la garonne par exemple))</li><li>
<u>1 Requete "Transport en Commun":</u> depuis le parcs relais le plus proche jusqu'au lieu d'arrivée</li>
</ol>
La réponse renvoyée à l'internaute sera l'agrégation du trajet routier jusqu'au parc relais suivi du trajet TC.<br><br>

Enfin pour d'autres requêtes comme la recherche spatiale de station VélôToulouse Symfony fait le travail sans SYNTHESE en utilisant simplement une base PostGIS.<br>

<h1>Conclusion</h1>
<br>
Ce premier projet "multi-réseaux" sur lequel j'ai été amené à travailler a été une expérience éprouvante mais finalement passionante.<br>
En effet, les délais impartis pour la réalisation étaient particulièrement serrés, et le résultat soumis au jugement de nombreux acteurs professionels du transport.<br>
Il nous a aussi fallu progresser de façon très importante sur notre système de gestion de données : l'intégration quotidienne des données de plusieurs réseaux au sein d'un même système nécessite des processus très industrialisés.<br>
<br>
<u>Sur le résultat :</u><br><br>
Nous sommes assez fiers des possibilités puissantes du calcul mixte "Routier" + "Transport en commun" qui offre une alternative crédible au tout voiture pour les zones péri-urbaines : ces concepts seront peut-être généralisés aux autres services Tisséo (c'est en réflexion).<br><br>
L'outil semble trouver son public : la fréquentation du premier mois ayant été très encourageante pour une plateforme multimodale (plus de 500 calculs par jour pour le premier mois tout sites confondus)<br><br>


