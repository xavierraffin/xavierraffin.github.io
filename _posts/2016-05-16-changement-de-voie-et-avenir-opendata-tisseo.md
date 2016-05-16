---
layout: post
title: Changement de voie et avenir OpenData Tisséo avec Navitia
comments: true
redirect_from: "/content/avenir-opendata-tisseo-navitia/"
excerpt_separator: <!--more-->
---

Je quitte aujourd'hui Tisséo après 6 ans d'OpenSource et 4 ans d'OpenData transport public (d'où le subtil jeu de mot du titre).

C'est l'occasion de faire un petit bilan, et de décrire de quoi l'avenir de l'OpenData Toulousain sera fait.

Et je vais même me risquer à un pronostic sur l'avenir de l'opensource dans le domaine du transport public au niveau mondial.

<img src="/public/images/aiguillage.jpg">
<center><u>Par Arne Hückelheim — Travail personnel, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=23003609</u></center>

<!--more-->
<br>

L'idée de se billet vient d'une question qui est venue plusieurs fois de la part des utilisateurs de api.tisseo.fr : 

>
> Les API Navitia et Tisséo se ressemblent, est-ce que Tisséo travaille sur un fork de Navitia ?

En effet, les développeurs curieux et perspicaces auront remarqués des similitudes troublantes entre les deux API.

_Ce billet est aussi un complément de [ma conférence à Mozilla en 2016](http://xavierraffin.com/2016/04/25/conference-API-opensource-opendata-mozilla) et de [ma conférence au Paris Open Source Summit 2015](http://xavierraffin.com/2015/11/19/conference-collaboration-opensource-ParisOpenSourceSummit)_

# Réponse courte

En fait c'est plutôt le contraire d'un fork, c'est une fusion :-)

# Réponse longue

* depuis 2001 Tisséo utilise un logiciel libre nommé **SYNTHESE** pour le calcul d'itinéraire et les systèmes IV temps réel
* en 2012 Tisséo a ouvert une API basé sur ce logiciel (et que j'ai créé pour l'occasion -voir [conf mozila](http://xavierraffin.com/2016/04/25/conference-API-opensource-opendata-mozilla)-)
* en 2013 **Kisio Digital** (ex CanalTP) filliale de la SNCF à ouvert une API OpenData : http://api.navitia.io
  Cette API est alimentée par les GTFS OpenData de nombreux réseaux dans le monde et mis à disposition par Kisio.
  Le réseau Tisséo est notamment disponible dans navitia.io (dans l'instance fr-sw), mais la qualité des données n'est pas aussi bonne que sur l'API Tisséo (limitation du GTFS et fréquence de MAJ trop faible) et il n'y a pas de temps réel
* à partir de là, je m'inspire un peu de leur syntaxe pour préparer la v1 actuelle dans l'objectif de rendre les deux API plus proches pour les développeurs
* en avril 2014, Kisio Digital open source son calculateur "Navitia" qui est derrière l'API navitia.io (ils sont balaises pour les noms chez Kisio)
* en juin 2014, les acteurs du libre dans le milieu du calcul d'itinéraire transport en commun libre se rencontrent et discutent des API :
  * **OpenTripPlanner** (Conveyal) 
  * **RRRR** (Bliksemlabs financé par ministère des transports hollandais)
  * **Navitia** (Kisio)
  * **SYNTHESE** (représenté par Tisséo) 

A ce moment là, on se rend bien compte que c'est compliqué et du gachis de ressource de travailler sur des logiciels différents et d'essayer de générer une API commune (tous ces cerveaux pour faire une telle découverte, c'est fascinant).

_Les deux premiers projets sont un peu à part : Conveyal destine plutôt OpenTripPlanner à de l'analyse de donnée qu'à servir le public en production, et RRRR veut offrir du calcul d'itinéraire embarqué sur mobile._

<center>
<blockquote class="twitter-tweet" data-lang="fr"><p lang="und" dir="ltr">Wow <a href="https://t.co/Mcdtjd2IdO">https://t.co/Mcdtjd2IdO</a> <a href="https://twitter.com/hashtag/otp?src=hash">#otp</a> <a href="https://twitter.com/hashtag/opentripplanner?src=hash">#opentripplanner</a> <a href="https://twitter.com/hashtag/opensource?src=hash">#opensource</a></p>&mdash; Stephan Simart (@stifoon) <a href="https://twitter.com/stifoon/status/659372239473778688">28 octobre 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
<u>Stifoon (Kisio) prend note du virage "analyste" OpenTripPlanner</u>
</center>
<br>

De plus au sein de la communauté SYNTHESE il y a des divergences sur la direction que dois suivre le projet (voir [ma conférence à Mozilla](http://xavierraffin.com/2016/04/25/conference-API-opensource-opendata-mozilla)) et des problèmes techniques (la bête accuse le poids des ans : 320000 lignes de C++ bouré de template de template)

Chez Tisséo après avoir évalué les options qui s'offrent à nous, mêmes les plus complexes à base de forks de patchs et d'aspirine, on décide de partir sur Navitia et de contribuer pour ajouter ce qui nous manque dans le projet.

Sur nos outils en production, on décide d'intégrer Navitia au fur et à mesure que les fonctions manquantes seront prêtes.

* en septembre 2015, toutes les fiches horaires Tisséo sont générés à partir de Navitia (et d'un autre logiciel libre : [TimeTable](https://github.com/CanalTP/MttBundle))
* en octobre 2015, sur http://api.tisseo.fr on bascule sur un mode hybride Navitia/SYNTHESE : c'est Navitia qui prend maintenant en charge l'authentification, la stack http, le parsing et formatage des requête (mais c'est encore SYNTHESE qui fait le gros des calculs)
* en octobre 2015 la sncf ouvre son api basée sur Navitia (http://api.sncf.com) et en décembre y met le temps réel des trains
* en janvier 2017 (si tout se passe bien), on ouvrira de nouveaux services directement servi par Navitia (service véhicule)
* en septembre 2017 (on espère) l'API sera servie intégralement par Navitia

# L'avenir

L'objectif maintenant est de créer une API v2 commune (Tisséo/Navitia) basée sur Navitia et qui offrira toutes les fonctions de l'API Tisséo en plus de celles de Navitia (pagination, filtre, isochrone et un tas de trucs).

_Je souhaite d'ailleurs bonne chance à tous mes collègues qui vont s'atteler à cette tâche ardue, en particulier ET, OG, VP, et JL_

A partir de là, pour les developeurs, les API SNCF, navitia.io et Tisséo auront une syntaxe identique.
On imagine que cela devrait démultipliser les possibilités, et même devenir un standard "de facto".

Je suis même prêt à prendre le pari que Navitia va devenir <u>la</u> solution IV de tous les opérateurs de transport public et de mobilité dans le monde.

Je base ce pari sur les faits suivants :

* Navitia est opensource
* le code est de grande qualité
* le projet est adossé à de grands industriels
* le projet est adossé à une naissante mais solide communauté
* il n'y a pas d'alternative OpenSource pour la production
* il n'y a pas de solutions propriétaire qui soit au niveau (troll inside)

Si vous ne partagez pas mon point de vue n'hésitez pas à me laisser un commentaire.

# Cliffhanger

Où est ce que je vais après Tisséo ?

Ca fera l'objet d'un futur article ...



