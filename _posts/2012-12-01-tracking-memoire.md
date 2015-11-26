---
layout: post
title: Tracking mémoire et profiling sur les gros projets 
---

J'ai récemment fait l'acquisition d'un superbe T-shirt qui arbore fièrement un logo que vous reconnaîtrez tous :

![placeholder](/public/img/2012/valgrind-man.png "Large example image")

_Il parait que j'étais le premier client en deux ans. Allez comprendre ?_

C'était donc pour moi une occasion unique de rendre hommage à ce superbe projet et d'y consacrer cet article.

Pour ceux qui n'ont pas reconnu le logo, il s'agit de celui de __Valgrind__ (pourtant c'était écrit gros).

Valgrind est un tracker d'erreur mémoire libre créé par Julian Seward qui a évolué en outil de débogage et de profiling (profilage en français moche) très complet.
Le principe de ce logiciel est d'exécuter des programmes dans un environnement virtuel où le processeur est simulé.
Ainsi, aucune allocation, affectation, lecture ou libération de mémoire ou même appel de fonction ne lui échappe

Grace à cette architecture Valgrind peut faire les deux choses suivantes de manière redoutablement efficace :

-    détecter les erreurs mémoires : il peut vous fournir un rapport complet des dépassements de tableau, des fuites mémoires (perte de pointeur sur une structure non libérée), etc ...
-    Faire du profiling : analyse du temps CPU passé dans chaque fonction et le nombre d'appel.

