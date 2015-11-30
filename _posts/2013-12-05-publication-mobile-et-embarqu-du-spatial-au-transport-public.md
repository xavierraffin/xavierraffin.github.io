---
layout: post
title: 'Publication : Mobile et Embarqué, du spatial au transport public'
created: 1386278955
---
J'ai publié un article dans le dernier numéro du <b>magasine Interface</b> (le magasine des INSA).

Le thème de ce numéro est :

<b>"Les nouveaux sujets de l'ingénierie informatique: cloud, sécurité informatique, mobilité, protection de la vie privée"</b>.

excerpt_separator

<div style="float:right">
<center>
<img src="/sites/xavierraffin.com/files/couv-interfacte-118.PNG" />
<i>La couverture du numéro 118 d'interface</i>
</center>
</div>

Les articles devaient prendre la forme de témoignages d'ingénieurs INSA travaillant dans ce domaine à destination de nos collègues et élèves-ingénieurs.

Cela a été pour moi l'occasion d'écrire un article de vulgarisation sur l'informatique dans le transport avec une coloration un peu plus personnelle que ce que je fais habituellement sur le blog.
J'ai notament donné 3 conseils aux jeunes ingénieurs qui souhaitent s'orienter dans cette activité.

<div style="clear:both">

<center>
<img src="/sites/xavierraffin.com/files/article-interface-118-site.png" />
<b>Aperçu de mon article dans le magasine</b>
</center>

<br><u>Voici le contenu intégral de l'article : (avec l'aimable autorisation de l'INSA)</u><br>

<center><h1 style="font-size: 1.9em">Mobile et Embarqué : du spatial au transport public</h1></center><br>

<b>Issu de la filière Modélisation Numérique du département GMM, je me suis spécialisé dans le développement Informatique.
Après un cursus dans le spatial (Mecano ID) puis dans l’aéronautique (EADS), j’ai bifurqué depuis 2010 dans le domaine du transport public en entrant chez Tisséo.
Si les domaines applicatifs ont changés, mes activités sont toujours restées centrés autour des logiciels de calculs.</b>

« <i>Des logiciels de calcul dans le transport public ?</i> »
Est généralement la première remarque des élèves ingénieurs à qui j’apprends mon employeur actuel.

Dans cet article, je vais donc répondre à cette question en faisant un focus particulier sur les aspects mobiles.

<h2>Description du contexte</h2><br>

Chez Tisséo, je suis responsable de toutes les applications « grand public » et de l'infrastructure qui les sert :
<ul>
<li>site internet : www.tisseo.fr</li>
<li>site mobile : mobi.tisseo.fr</li>
<li>applications iOS & Android (en cours de développement)</li>
<li>écrans IV (Information Voyageur) dans certaines stations</li>
</ul>
Ces applications sont alimentés par un système serveur dit «<i>Système d'Aide à l’Exploitation et à l’Information Voyageur</i>» (<b>SAE-IV</b>).
Ce système délivre des services à trois catégories d’utilisateurs :
<ul>
<li>Les usagers</li>
<li>Les chauffeurs des bus et tram (à Toulouse le métro est automatique)</li>
<li>Les régulateurs de trafic</li>
</ul>

Aux usagers en situation de mobilité le système offre les services suivants :
<ul>
<li>Horaire de passage à l’arrêt en temps réel</li>
<li>Calcul d’itinéraire</li>
<li>Représentation cartographique du réseau</li>
<li>Information trafic (perturbation, déviation, état des ascenseurs, …)</li>
<li>Réservation des bus TAD (Transport A la Demande)</li>
</ul>

Aux chauffeurs de bus, il permet de
<ul>
<li>suivre le tracé de la ligne (même en cas de déviation temporaire)</li>
<li>réguler l’avance retard</li>
<li>pour les lignes TAD : prendre en compte les réservations</li>
</ul>

Aux régulateurs de la centrale de trafic, il permet :
<ul>
<li>de contrôler les écarts entre le théorique et le réel</li>
<li>d’agir sur le réseau en cas d’incident ou de saturation (par injection de véhicules supplémentaires par exemple)</li>
</ul>

L’architecture du système est composée d’un serveur central (généralement plusieurs) et d’une multitude de périphériques mobiles et fixes.

<center>
<img src="/sites/xavierraffin.com/files/archipt-site.png" />
<b>Figure 1 : Architecture d’un système temps réel de transport public</b>
</center>

Pour que le système fonctionne, il faut lui fournir préalablement les données suivantes : 
<ul>
<li>Les horaires théoriques des lignes</li>
<li>Les tracés de ligne</li>
<li>La position des arrêts</li>
<li>Le graphe des rues de la ville</li>
</ul>

Ces données sont chargées dans une phase d'initialisation (généralement en fin de service vers 3h30).
Puis lorsque les véhicules commencent à sortir des dépôts, un flux continu d'information temps réel doit se répercuter sur tous les affichages clients.
Dans le cas du mobile, la satisfaction de l'usager dépendra de deux qualités :
<ul>
<li>la précision / pertinence des informations (géolocalisation)</li>
<li>la vitesse de mise à jour des informations</li>
</ul>

Comment adresse-t-on ces problématiques ? C'est ce que je vais présenter maintenant.

<h2>Synchronisation des données : contraintes des réseaux mobiles</h2><br/>

Une plus grosses contraintes du développement mobile est l'accès réseau.

En effet, si le débit est généralement correct en 3G, la latence peut être catastrophique.
Il arrive parfois de mettre plusieurs secondes avant de recevoir le premier octet de la réponse !

Le développement sur mobile marque donc le retour du besoin d'optimisation.
Nombre de requêtes HTTP, poids des transactions, mise en cache : <u>tout compte</u>.

La mise en cache de nos arrêts est l'un des défis de nos applications mobile.
En effet, il y en a trop pour les transférer quotidiennement, et pourtant il y a des petites modifications tous les jours.

Nous mettons donc en place un système d'envoi de différences suivant la date de dernier démarrage de l'application.
Un tel mécanisme doit être sans faille, car sinon, des incohérences d'affichage surviennent très vite.

Par exemple, lorsque <u>la communauté urbaine inaugure une nouvelle ligne de tram</u>, il y a intérêt à ce <u>qu'elle apparaisse le jour J</u> sur tous les téléphones !

<h2>Qualité de l'information : fortes exigences sur mobile</h2><br/>

La précision de géolocalisation et de géocodage (le fait de remplacer un nom par des coordonnées ou inversement) croît avec les affichages suivants :
<ul>
<li>vue textuelle non mobile</li>
<li>vue textuelle non mobile avec carte partielle</li>
<li>un plan interactif</li>
<li>mobile géolocalisé</li>
<li>mobile en réalité augmenté</li>
</ul>

En effet, si vous ne remarquerez probablement pas une correspondance placée de manière approximative sur un résultat de calcul d'itinéraire, vous ne comprendriez pas pourquoi les deux abris de bus d'un arrêt semblent être sur le même côté du trottoir sur une carte détaillé.
 
<center>
<img src="/sites/xavierraffin.com/files/ipad-carto-integ-small.png" />
<b>Figure 2 : « <i>plan interactif</i> » sur tablette</b>
</center>

Pour notre « plan interactif » (<a href="http://www.tisseo.fr/plan-interactif" target="_blank">http://www.tisseo.fr/plan-interactif</a>) nous avons reconstruit entièrement le système de positionnement des arrêts ainsi que de construction des tracés de lignes.

De même nous avons tous constaté que parfois un calcul d'itinéraire sur un mobile ou un GPS nous indiquais un point de départ erroné.

Cela n'est pas forcément du à un mauvais positionnement GPS, mais cela peut être <b>un problème de géocodage</b> :
Lorsque votre téléphone communique votre position au calculateur, celui-ci projette votre position sur son modèle de voirie.
Si son modèle de voirie est incomplet, pas à jour ou mal positionné, il vous dira : « <i>Vous partez de XXX</i> » qui ne correspond pas à votre position.

Pour être réactif face à ce genre de problème, nous utilisons un modèle de voirie communautaire (OSM) que nous pouvons donc corriger et que nous réimportons quotidiennement.

Un cran plus loin, nous avons fait des essais de « <i>réalité augmenté</i> » sur smartphone, et il nous est apparu, que nous n'étions pas encore prêt car pas assez précis.

<center>
<img src="/sites/xavierraffin.com/files/realite-augmente-cc-site.png" />
<b>Figure 3 : Un arrêt de bus en « <i>augmenté</i> » d'informations transport</b>
</center>

En effet, une erreur de 2 mètres peut faire disparaître un arrêt parce que situé derrière vous.

L'information temps réel de positionnement des bus est aussi très sensible :

Sur de grand arrêts, le système doit détecter que le bus est parti avant qu'il ne quitte la zone d’arrêt.
Avant que nous corrigions cela, il y avait des bus affichés au départ qui était déjà parti.
<b>Et les gens qui courraient pour rien en sortant du métro n'était pas ravis !</b>


<h2>3 conseils:</h2><br/>

A ceux qui voudraient travailler dans le domaine de la mobilité, j'ai tout d'abord une bonne nouvelle : « <i>L'avenir sera de plus en plus mobile</i> ».

La question, qui se pose n'est donc pas « <i>Vais-je réussir à travailler dans la mobilité ?</i> » mais « <i>Comment décrocher les postes les plus intéressants ?</i> »

<ol>
<li><b>Restez dans la technique :</b>
L'expertise technique permet de vous distinguer.
Notre monde se complexifie, et le besoin en expertise va croissant : par contre vous devrez vous maintenir à niveau en permanence.<br/>
</li>
<li><b>Toute expérience est valorisable :</b>
Entre des domaines très différents il y a parfois besoin de compétences similaires.
Avant un entretien, vous devez les avoir identifiés dans vos expériences précédentes.
Pour moi, ça a été le calcul, mais vous devez trouver la(les) votre(s).<br/>
</li>
<li><b>Faites preuve de stratégie et de cohérence dans votre cursus :</b>
Vous ne parviendrez peut-être pas directement à intégrer le domaine qui vous attire. Vous devrez alors trouver un autre domaine qui fait appel aux mêmes types de compétences.
Vous pouvez même annoncer cette stratégie lors d'un entretien, cela soulignera votre recul et votre détermination.<br/>
</li>
</ol>

<h2>Conclusion:</h2><br/>

Je travaille sur des applications à très forte visibilité qui rendent des services très concrets.
C'est extrêmement gratifiant, mais cela génère aussi une forte pression.
Lorsque quelque chose ne marche pas, cela se voit beaucoup et cela pénalise beaucoup de monde.

On se sent investi d'une grande responsabilité, mais on expose aussi son travail à la critique.

Cela a aussi des répercutions sur le plan personnel : je ne passe plus une seule soirée à Toulouse sans que quelqu'un me dise : « <i>Ce serait bien de faire ça</i> » ou « <i>Je ne comprend pas pourquoi vous avez fait ça comme ça</i> »   :-)


