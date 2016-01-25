---
layout: post
title: Nouvelle version du blog
comments: true
created: 1353881847
redirect_from: "/content/nouvelle-version-du-blog/"
---

Avec cette nouvelle année viennent les bonnes résolutions.

Alors voila, j'ai finalisé la refonte de mon site perso (enfin en tout cas je l'ai mis en ligne).

Plus sobre, j'ai choisi le thème <a href="https://github.com/poole/hyde">Hyde</a> de Mark Otto alias <a href="https://twitter.com/mdo">@mdo</a>.

## Un site statique ??

Techniquement quoi de neuf ?

Et bien une technologie très 1980 : __des pages statiques__ ! 

Cette technologie avancée revient à la mode car :
 - la montée en charge est très bonne :-o
 - elle est facile à mettre en cache :-o
 - le besoin en ressource serveur est faible :-O

Mais au delà de ces évidences, c'est surtout <strike>le ras le bol des CMS obèses</strike> __l'émergence de nouveaux générateurs de site__ qui a relancé l'intérêt de la pratique.

Car en effet, s'il est statique pour le visiteur, __il ne l'est pas pour l'auteur__.
Grace à <a href="http://jekyllrb.com">Jeckyll</a>, je rédige mes articles <strike>dans une interface en 3D vétu d'un exosquelette</strike> hors ligne en syntaxe markdown et je structure le site à l'aide de templates et de fichiers YAML de configuration.

Par exemple, si j'ajoute un article, je créé simplement un nouveau fichier texte, je relance Jeckyll et celui ci reconstruit les pages du site, avec la pagination, les tags, les liens internes ...

Cette technique c'est aussi beaucoup popularisé grace au service d'hébergement gratuit <a href="https://pages.github.com">Github pages</a>.
Github propose de transformer vos dépôts en site web sur votre propre nom de domaine !!

De plus Github exécute Jeckyll sur votre dépôt avant de le servir en ligne.
Vous pouvez donc ne mettre en conf que le code source de votre site et non pas le code généré : la classe.

Voici par exemple le dépôt du code de mon blog : https://github.com/xavierraffin/xavierraffin.github.io 

## Limitations

Alors effectivement, il est impossible de réaliser une page dynamique côté serveur avec un tel système.

Mais par contre, en combinant un peu de Javascript avec quelques services Web, on peut presque tout faire.

Par exemple les commentaires sont servi par <a href="https://disqus.com">Disqus</a>.

Autre exemple, en intégrant Viméo, j'ai pu réaliser le site de vidéos professionnel de mon frère : http://regisraffin.com

Certains comme <a href="http://makina-corpus.com">Makina Corpus</a> vont beaucoup plus loin avec des sites cartographiques avancés pour leurs clients : http://vuduciel.loire-atlantique.fr

Si j'ai pris un plaisir sadique à forcer mon frère à utiliser git pour mettre à jour son site cela n'est pas une obligation
Il est possible d'utiliser un éditeur de contenu pour Github comme <a href="http://prose.io/">prose.io</a>.

## Le contenu

Maintenant, il ne me reste plus qu'à poster des articles toujours plus passionnants et peut être un peu plus régulièrement ;-)





