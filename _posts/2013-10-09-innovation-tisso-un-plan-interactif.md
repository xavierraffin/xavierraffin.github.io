---
layout: post
title: 'Innovation Tisséo : un plan interactif'
created: 1381349144
---
Tisséo ouvre aujourd'hui un plan interactif de son réseau sur son site web :

<center><a href="http://www.tisseo.fr/plan-interactif/" target="_blank" style="font-size:25px;font-weight: bold">http://www.tisseo.fr/plan-interactif</a></center>

Cet outil inaugure un nouveau fond de plan qui se généralisera sur les autres support numériques Tisséo.

excerpt_separator

C'est avec un immense plaisir que je vous présente le résultat de longs mois de travail intensif :

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-11.png" />
<i>Au démarrage le plan interactif ressemble à ça</i></center>

<i>Pour les amateurs de technique, vous pouvez directement vous rendre <a href="#socle-technique">à la fin de l'article</a> pour comprendre comment nous avons réalisé cette merveille.</i>

<h1>Les fonctionnalités</h1>

Voici les grandes fonctionnalités de la carte :
<ul>
<li><a href="#exploration-carte">Exploration de la carte</a></li>
<li><a href="#prochains-passages">Prochains passages en temps réel</a></li>
<li><a href="#google-street">Google Street View</a></li>
<li><a href="#calcul-itineraire">Calcul d'itinéraire</a></li>
<li><a href="#exploration-lignes">Exploration des lignes</a></li>
<li><a href="#poi">Points d'intérêt</a></li>
<li><a href="#disponibilite-velotoulouse">Disponibilité des VélôToulouse en temps réel</a></li>
<li><a href="#i18n">Internationalisation</a></li>
<li><a href="#autres-outils">Autre Outils</a></li>
</ul>

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-12.png" />
<i>Les différents éléments de l'IHM</i></center>

<h2 id="exploration-carte">Exploration de la carte</h2>

Une des plus simples actions possibles, est de rechercher un lieu à l'aide de la barre de recherche :

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-3.png" />
<i>recherche d'arrêt, d'adresse ou de rue</i></center>

Après validation dans cette barre de recherche, le plan se centrera sur l'objet demandé, une rue, un arrêt, ...

Dans le cas d'un arrêt, une fenêtre s'ourvrira indiquant les lignes qui y passent, et vous permet de zommer sur les poteau d'arrêt ou d'utiliser cette zone d'arrêt comme point de départ ou d'arrivée :

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-13.png" />
<i>Fenêtre sur zone d'arret</i></center>

Vous remarquerez les pictogrammes <img src="/sites/xavierraffin.com/files/Icone_Alerte.png" /> sur les lignes perturbées : le clic sur ce picto renvoi vers l'information réseau associée.

Le clic sur un numéro de ligne permet <a href="#exploration-lignes">l'affichage de la ligne</a>.

<h2 id="prochains-passages">Prochains passages en temps réel</h2>

Si vous zoomez fortement, vous verrez, non plus les "zones d'arrêts" mais les "poteaux d'arrets" sur la carte.

Si vous cliquez sur un poteau d'arrêt, vous pourrez voir les prochains passages des bus et tram :

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-5.png" />
<i>Prochains passages en temps réel</i></center>

<h2 id="google-street">Google Street View</h2>

Aussi bien sur une "zone d'arrêt" que sur un "poteau d'arrêt", vous pouvez accéder à une visualisation Google Street View :

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-6.png" />
<i>Google Street View : vous pouvez visualiser en plein écran</i></center>

<h2 id="calcul-itineraire">Calcul d'itinéraire</h2>

Vous pouvez lancer un calcul d'itinéraire depuis le formulaire à gauche, depuis une fenêtre d'arrêt, ou bien directement en par clic droit sur la carte (ma méthode préferée)

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-2_0.png" />
<i>Un calcul d'itinéraire sur le plan interactif</i></center>

<h2 id="exploration-lignes">Exploration des lignes</h2>

Il est possible d'afficher une ou plusieurs lignes (sélection multiple avec <i>CTRL</i>)

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-4.png" />
<i>Affichage d'une ligne de bus</i></center>

<h2 id="poi">Points d'intérêt</h2>

Grâce au menu de gauche (dernier onglet), il vous est possible d'afficher des points d'intérêts sur la carte  (sélection multiple avec <i>CTRL</i>)

Les point d'intérêts sont des lieux publics (administrations, théatres, parcs, universités, ...) ou des lieux en lien avec le transport (Parkings, Parcs relais, Gare Routières, stations vélôToulouse).

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-7.png" />
<i>Au survol des points d'intérêts des informations complémentaires s'affichent</i></center>

<h2 id="disponibilite-velotoulouse">Disponibilité des VélôToulouse en temps réel</h2>

Les points d'intérêts "stations vélôToulouse" indiquent le nombre de places disponibles et de vélos disponibles en temps réel.

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-8.png" /></center>

<h2 id="i18n">Internationalisation</h2>

Le plan interactif, comme d'autres éléments transport de tisseo.fr a été traduit intégralement en anglais et espagnol.

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-10.png" />
<i>Aperçu de la version anglaise du plan interactif</i></center>

Ces versions sont disponibles aux URL suivantes :

<a href="http://www.tisseo.fr/en/interactive-map" target="_blank" style="font-size:18px;font-weight: bold">http://www.tisseo.fr/en/interactive-map</a>

<a href="http://www.tisseo.fr/es/mapa-interactivo" target="_blank" style="font-size:18px;font-weight: bold">http://www.tisseo.fr/es/mapa-interactivo</a>

<i>(aujourd'hui il n'existe pas encore de lien depuis tisseo.fr vers ces deux versions, mais cela va venir)</i>

<h2 id="autres-outils">Autres outils</h2>

<center><img src="/sites/xavierraffin.com/files/plan-interactif-tisseo-9.png" /></center>

Enfin, la barre d'outil supérieur permet dans l'ordre :
<ul>
<li>Remise à zéro de la carte</li>
<li>Mesure des distances</li>
<li>Impression : l'impression des calculs d'itinéraires bénéficie d'un traitement spécial (meilleur rendu sous chrome)</li>
<li>Lien persistant : permet de générer un lien vers l'état actuel de l'application<br />Idéal pour envoyer un itinéraire à un ami</li>
<li>Nous contacter</li>
<li>Aide</li>
</ul>

<h1 id="socle-technique">Le socle technique</h1>

<h2>Les données</h2>

<ul>
<li><u>OSM</u> : les données du fond de plan ainsi que les données de voirie du calculateur sont importées d'OpenStreetMap</li>
<li><u>OpenData JCDecaux</u> : le nombre de place de vélo disponible dans les stations vélÔToulouse</li>
<li><u>OpenData Toulouse Métropôle</u> : les numéros de rue, les stations de vélo (nous n'utilisons pas l'API JCDecaux içi, car elle ne permet pas les requêtes spatiales)</li>
<li><u>Google Maps API V3</u> : pour les fenêtres Google Street View</li>
<li><u>Tisséo</u> : tout le reste : arrêts, lignes, horaires, agences, parcs relais ...</li>
</ul>

<h2>Les composants logiciels</h2>

Sans entrer dans les détails (ce que je ferais dans de futurs articles) je résume içi les principaux composant de l'architecture logicielle.

<ul>
<li><u>SYNTHESE</u> : élément central de l'application, il centralise les données transport, effectue les calculs d'itinéraires, donne les horaires temps réel, ...</li>
<li><u>OpenLayers + ExtJS</u> : ces librairies JavaScript composent la colone vertébrale de l'application côté client</li>
<li><u>PostGIS</u> : cette extension spatiale à PostGreSQL nous sert à stoquer les données OSM du fond de carte, ainsi que les données des POI</li>
<li><u>Géoserver</u> : notre moteur de rendu cartographique : il transforme les données OSM et Tisséo en images png</li>
<li><u>Nginx + Mapproxy + Gunicorn + pngcrush </u> : notre arsenal de cache cartographique il assure la tenue à la charge</li>
<li><u>Apache</u> : sert les fichiers statiques, sert aussi de reverse proxy devant les autres systèmes (sauf fond de carte) pour éviter le cross domain</li>
<li><u>PHP</u> : il y a un petit bout de php qui permet d'enrichir l'API JCDecaux de fonctions spatiales (avec PostGIS en backend)</li>
</ul>

<h1>Remerciements</h1>

Je profite de cette inauguration pour remercier toute l'équipe qui a participé au projet :
<ul>
<li><u>Développeurs (ma team de winners)</u> : Julien, Erwan, Vincent, Romain, Pierre-Yves</li>
<li><u>Spécialistes SIG</u> : Laurie, Grégoire, Virginie</li>
<li><u>Données</u> : Cyrille</li>
<li><u>Design & UX</u> : Julien, Brigitte, Lee</li>
<li><u>Administrateurs Systèmes</u> : David, Emmanuel, Julien, Maxime</li>
<li><u>Les chefs</u> : (bah, ils y ont mis du leur aussi :-) Frédéric, Olivier</li>
<li><u>Pour ses conseils techniques précieux</u> :  Eric</li>
</ul>
