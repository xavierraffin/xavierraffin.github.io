---
layout: post
title: Analyse du calcul d'itinéraire sur Google Maps
created: 1374602467
comments: true
redirect_from: "/content/analyse-du-calcul-ditinéraire-sur-google-maps/"
---
Un calculateur d'itinéraire ne pourra jamais prévoir votre temps de trajet exact avec une certitude de 100%.

excerpt_separator

Il est par exemple impossible de savoir si vous aurez les feux au vert ou non.
Votre vitesse estimée est donc une moyenne tenant compte d'un ou de plusieurs de ces éléments :
<ul>
<li><u>la vitesse maximum autorisée :</u> c'est la moindre des choses</li>
<li><u>le type de voirie :</u> en fonction de la voie : résidentiel, boulevard, autoroute ... un abattement de la vitesse maximal théorique est effectué (par exemple sur <a href="/content/pr%C3%A9sentation-de-synthese">SYNTHESE</a> nous considérons que sur autoroute, vous circulez à 95% de la vitesse maximum, alors que sur une zone résidentielle nous appliquons un 70 %)</li>
<li><u>le traffic :</u> pour un calcul sur un itinéraire court et avec un départ immédiat cela est très fiable, cela l'est moins sur un trajet dans 3 jours (il existe cependant des calculateurs qui tiennent compte de l'historique de traffic sur le type de jour et d'heure choisi)</li>
<li><u>Les feux :</u>si le nombre de feux est élevé sur une section de parcours, un nouvel abattement sera réalisé</li>
</ul>

En plus de ces éléments, deux nouvelles idées ont été retenues par les ingénieurs de Google Maps :

<h1>Pénalité à l'insertion sur un rond point</h1>

Ce petit exemple montre que Google Maps applique une pénalité de 12 secondes pour l'insertion sur un rond point :

<center><img src="/sites/xavierraffin.com/files/algorithme-google-maps-1.png" />
<i>Pénalité de 12 secondes lors de l'insertion (crédit E.T.)</i></center>

<h1>Pénalité sur traversée de ligne discontinue</h1> 

Quitter un axe principal pour prendre une route secondaire perpendiculaire oblige le conducteur à freiner :

<center><img src="/sites/xavierraffin.com/files/algorithme-google-maps-2.png" />
<i>Pénalité supplémentaire de 39 secondes pour couper la voie opposée (crédit E.T.)</i></center>

Encore plus fort, vous noterez que la pénalité pour un virage à droite est de 6 secondes contre 45 secondes pour un virage à gauche.

En effet, Google Maps considère que lorsqu'on coupe la ligne blanche centrale, on perd encore plus de temps car on doit attendre que les voitures qui viennent à contre sens nous laissent un espace.

<h1>Remerciement</h1>

Ces constatations sur le comportement de Google Maps m'ont étés signalées par Erwan Turck, mon apprenti à Tisséo que je remercie chaudement ;-)
