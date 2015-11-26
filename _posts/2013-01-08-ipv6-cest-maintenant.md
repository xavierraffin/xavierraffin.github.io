---
layout: post
title: IPv6 c'est maintenant !
created: 1357681891
---
<div style="float:right">
<img src="/sites/xavierraffin.com/files/IPv6_logo_256.png" />
<center>Le logo du lancement mondial d'IPv6</center>
</div>
Si vous suivez les actualités du monde d'internet, vous avez entendu parler d'IPv6.
Pour les autres, il s'agit d'une nouvelle version du protocole IP qui vient prendre la relève du vénérable IPv4, le système d'adressage internet.

IPv6 a fait l'objet d'un <a href="http://www.worldipv6launch.org" target="_blank">lancement mondial</a> le 6/6/2012.
A cette occasion, de nombreux FAI ont inaugurés leur offres IPv6 et des sites majeurs sont passés en IPv6 (ou venaient de le faire) :
<ul>
<li>www.google.com</li>
<li>www.facebook.com</li>
<li>www.youtube.com</li>
<li>www.wikipedia.org</li>
<li>www.yahoo.com</li>
<li>www.bing.com</li>
<li>...</li>
</ul>
Cette liste tombe certes un peu à plat sans le fabuleux <b>xavierraffin.com</b>.

L'explication de ce raté est simple : mon blog n'existait pas à cette date.
Mais c'est maintenant chose faite et l'IPv6 de mon blog est : <b>2a01:e0b:1:127:ca0a:a9ff:fec8:e84f</b>, et c'est ce qui m'a inspiré cet article.

<div style="float:right; background-color:#ECECEC">
<h4 style="background-color:#DDD;margin:0"><b>En détail</b></h4>
<a style="color:#191970" href="#ipv6-decolle">L'IPv6 décolle</a>
<a style="color:#191970" href="#consequences">Des conséquences techniques majeures</a>
<a style="color:#191970" href="#transition">Comment se passe la transition ?</a>
<a style="color:#191970" href="#comment-participer">Comment participer ?</a>
<a style="color:#191970;margin-left:15px" href="#ipv6-internaute">1) en tant qu'internaute</a>
<a style="color:#191970;margin-left:15px" href="#ipv6-webmaster">2) en tant que webmaster</a>
<a style="color:#191970;margin-left:15px" href="#ipv6-lan">3) en tant qu'admin réseau en entreprise</a>
<a style="color:#191970" href="#conclusion">Conclusion : IPv6 pour tisseo.fr ?</a>
</div>

<h1 id="ipv6-decolle">L'IPv6 décolle</h1>
Avant d'entrer dans des considérations techniques, quelques chiffres qui montrent que l'IPv6 devient une réalité :
<center><img src="/sites/xavierraffin.com/files/IPv6-progression.png" />
<i>Le traffic mondial IPv6 dépasse les 1% en 2012 (<a href="http://www.google.com/ipv6/statistics.html">source Google</a>)</i>
</center>
On peut même être fiers car la France est largement devant les états-unis sur ce point grâce à un FAI qui a tout compris :
 <center>
<img src="/sites/xavierraffin.com/files/IPv6-world-progression.png" style="border:1px #444 solid"/>
<i>Progression de l'IPv6 dans le monde (<a href="http://www.google.com/ipv6/statistics.html#tab=per-country-ipv6-adoption">source Google</a>)</i>
</center>

<h1 id="consequences">Des conséquences techniques majeures</h1>

IPv6 avec des adresses de 128 bits apporte une solution à la pénurie d'adresse IPv4 et ces 32 bit d'adresse.
Un adressage 128 bit c'est <a href="http://fr.wikipedia.org/wiki/Adresse_IPv6" target="_blank">667 millions de milliards d'adresses par millimètre carré de surface terrestre</a>, c'est tellement incommensurable que cela marque <b>la fin du NAT</b> <i>(tadaam !)</i>.

La disparition du NAT ou IP masquerade, est une révolution dans la conception des réseaux LAN qui va transformer l'administration réseau.
En effet, chaque appareil connecté au net pourra avoir une adresse IP unique ainsi un FAI ne fournit plus à ses abonnés une unique IPv4 mais une plage d'adresse IPv6 largement suffisante pour tous les équipements connectés de la maison.

<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:42px; margin: 5px 30px"><b>?</b></div>
<i>Vous êtes un geek hyper connecté avec 15 PC, 10 serveurs et 20 smartphones,et vous craignez que cela ne suffise pas ?

Pas d'inquiétude, typiquement un FAI vous donnera 2<sup>64</sup> adresses (soit 18 446 744 073 709 551 616) ce qui laisse de la marge pour vos futurs projets.</i></div>
<br />

L'avantage de cette nouvelle technique, est la simplification du routage vers les appareils (la redirection de port devient inutile) ce qui ouvre bien des possibilités mais laisse craindre des problématiques de sécurité nouvelles.

<div style="float:right">
<img src="/sites/xavierraffin.com/files/ours-polaire.jpg" />
<center><i>IPv6 sauve des ours</i></center>
</div>

L'IPv6 <s>sauve des ours</s> simplifie aussi le travail des routeurs internet grâce à d'autres changements d'architecture majeurs :
<ul>
<li><u>des entêtes beaucoup plus simples  :</u>l'entête des datagrammes IPv6 ne contient plus que 7 champs contre 14 pour l'IPv4</li>
<li><u>plus de calcul de checksum  :</u> la vérification de l’intégrité des paquets est laissée aux couches transport TCP et UDP (c'est donc fait en bout de chaine et pas par les routeurs)</li>
<li><u>des paquets beaucoup plus gros :</u> grâce à la fiabilité des réseaux actuels, il a été décidé que les limites de taille de paquet IPv6 pouvaient être bien plus élevées. La norme indique que tous les routeurs doivent supporter au minimum des paquets jusqu'à 1280 octets (contre 68 pour IPv4).</li>
<li><u>des paquets indivisibles :</u> les contenus ne subissent aucune opération de subdivision/reconstitution sur les routeurs. Si un datagramme est trop gros alors le routeur renvoie une erreur à la source lui indiquant que cette destination n'est pas atteignable avec des paquets aussi gros. C'est donc l'ordinateur source qui a la charge de s'adapter et de subdiviser ce qui est bien plus efficace.</li>
</ul>
L'avantage : diminue les traitements sur les routeurs internet donc: améliore le débit et économise du CPU !
Ce qui représente une avancée écologique importante et contribue à sauver des ours.

Enfin, je n'entre pas dans les détails mais IPv6 apporte bien d'autres améliorations en terme de sécurité (IPsec intégré, ...)

<h1 id="transition">Comment se passe la transition ?</h1>

Bien vu, vous vous demandez comment se passe la période de transition.

Car si un réseau IPv6 est assez différent d'IPv4, bien des choses ne changent pas ou peu :
<ul>
<li><u>DNS :</u> ça existe toujours : les enregistrements de domaines deviennent <b>AAAA</b> et les reverses PTR <a href="http://fr.wikipedia.org/wiki/IPv6#DNS" target="_blank">changent de look</a></i>
<li><u>DHCP :</u> ça change de nom : <b>DHCPv6</b> mais dans les grandes lignes c'est le même principe</i>
<li><u>ICMP, ARP, IGMP :</u> les trois sont remplacés par l'unique : <b>NDP (Neighbor Discovery Protocol)</b> qui offre en plus la découverte automatique des routes !</i>
<li><u>Routage des paquets :</u> se fait toujours d'une IPv6 vers une IPv6 (exclusivement)</li>
</ul>

Ce dernier point est très important : on ne peut pas construire de route d'une IPv4 vers une IPv6 (et inversement).
Autrement dit seuls les internautes en IPv6 contacteront xavierraffin.com (et accessoirement www.google.com) en IPv6.

<div style="float:right">
<img src="/sites/xavierraffin.com/files/tunnel-ipv6.svg_.png" />
<center><i>Tunneling IPv6 vers IPv4 (<a href="http://fr.wikipedia.org/wiki/Transition_d%27IPv4_vers_IPv6">source Wikipédia</a>)</i></center>
</div>

C'est pour ça que les services Web sont toujours accessibles en IPv4 et que l'IPv4 de mon blog (88.191.127.234) existe encore.

Et comme il faut que les internautes qui passent à l'IPv6 puissent toujours avoir accès aux sites web IPv4 (par exemple à des blogs de concurrents bien moins modernes) les FAI mettent en place des solutions de conversion IPv4 vers IPv6 (avec du tunneling et des trucs compliqués).

<h1 id="comment-participer">Comment participer ?</h1>

<h3 id="ipv6-internaute">1) en tant qu'internaute</h3>

Si vous voulez sauvez des ours vous aussi, vous pouvez passer à IPv6.

Plusieurs FAI proposent déjà l'IPv6 :
<ul>
<li>Free</li>
<li>SFR</li>
<li>Numéricable sur une de ces box</li>
<li>Orange : non, mais en 2014</li>
</ul>
Généralement vous pouvez basculer à IPv6 par un simple paramétrage de votre box.

<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:42px; margin: 5px 30px"><b>!</b></div>
<i>Paramétrez votre box (je vous laisse 5 minutes)

Puis reprenez votre lecture.</i></div>
<br />

Pour vérifier la qualité de votre connexion IPv6 depuis votre navigateur (qui implique votre navigateur, votre OS, le type de tunneling pratiqué par votre opérateur, ...) je vous conseille cet excellent service : <a href="http://test-ipv6.com">http://test-ipv6.com/</a>.

Vous avez 10/10 ? Il est temps de passer à l'étape suivante :

<h3 id="ipv6-webmaster">2) en tant que webmaster</h3>

Vous avez un ou plusieurs site web à titre pro ou perso ? 
Je vous encourage à sauter le pas.

Si vous souhaitez y passer rapidement sans modifier votre configuration réseau, ou que vous êtes inquiet d'utiliser un protocole encore peu éprouvé sachez qu'il existe des solutions.
Par exemple Akamai, le célèbre CDN propose par exemple <a href="http://www.akamai.com/html/solutions/ipv6_adaptation.html" target="_blank">un service de reverse tunneling</a> et prend en charge pour vous les problématiques techniques.

Si vous ne mangez pas de se pain là <s>et que vous ne souhaitez pas vivre comme un assisté</s>, vous avez de la chance : <u>j'ai défriché le terrain pour vous</u> (et c'était pas de la tarte) !

Mon blog est hébergé sur un serveur dédié dedibox que je loue chez Online.net.
Je vais donc détailler la procédure chez eux, mais comme leur mode de fonctionnement IPv6 est plutôt exotique, je vais aussi expliquer le cas standard.

Comme votre FAI, un hébergeur vous donnera un bloc IPv6 (un bloc /64 par machine chez OVH et /48 par client chez Online par exemple) à utiliser comme bon vous semble sur vos serveurs physiques et virtuels.

Ensuite suivant l'hébergeur, les IP de votre bloc seront soit très classiquement administrées par vos soins comme c'est le cas chez OVH soit de façon plus originale distribuées en dhcp(v6) (comme chez Online) !


Dans l'interface d'administration du serveur vous pouvez demander un bloc IPv6 /48.
<u>Cas particulier chez Online</u> : vous obtenez aussi un <b>Duid</b> qui permettra au DHCPv6 d'Online de vous reconnaitre et de vous attribuer les bonnes adresses (celles de votre bloc).

Bon, maintenant il faut configurer votre serveur (une ubuntu 10.04 dans mon cas).

De base une IPv6 est déclarée :
<code>
root@xxxxxx# ifconfig
eth0      Link encap:Ethernet  HWaddr c8:0a:a9:c8:e8:4f
          inet adr:88.191.127.234  Bcast:88.191.127.255  Masque:255.255.255.0
          adr inet6: fe80::ca0a:a9ff:fec8:e84f/64 Scope:Lien
          ...
</code>

Pas de fausse joie, il s'agit de l'IPv6 dédiée a un réseau LAN.
En IPv6 il existe des <a href="http://fr.wikipedia.org/wiki/Adresse_IPv6#Cat.C3.A9gories_d.27adresses">adresses réservées LAN (scope:lien)</a> (qui commencent toujours par <b>fe80</b>) et nous avons besoin d'adresse de type <b>scope:Global</b>. 

<div style="margin: 0 20px; padding: 10px;background-color:#ddd;">
<div style="float:left; font-size:42px; margin: 20px"><b>PING</b></div>
<i><br />Une adresse très utile pour les tests de paramétrage IPv6 <b>ipv6.google.com</b></i>
<br />
On ping avec "<b>ping6</b>" en IPv6.
</div>
<code>
root@xxxx# ping6 ipv6.google.com
connect: Network is unreachable
</code>

Donc là il va falloir dire à l'OS l'IP choisie (une au choix à l'intérieur de votre bloc) ainsi que la gateway (via le fichier /etc/network/interfaces):
<code>
...
#Mon parametrage IPv4
iface eth0 inet static
        address 88.191.127.234
        ...
#Mon parametrage IPv6
iface eth0 inet6 static
        address 2a01:e0b:1:127:ca0a:a9ff:fec8:e84f
        netmask 48
        gateway XXX
</code><center><i>Extrait de ma conf IP (tel quelle aurait été j'y je n'étais pas chez ces francs-tireurs d'Online)</i></center>

Ou alternative chez Online : 
<ul>
<li>soit on utilise un client dhcpv6 compatible avec le Prefix-Delegation et on lui communique notre duid (voir <a href="http://documentation.online.net/fr/serveur-dedie/reseau/prefixe_ipv6" target="_blank">la doc</a>).
<li>soit on se contente d'une seule ipv6 par serveur (hors du bloc) et dans ce cas il n'y a rien à faire mis à part lancer un dhclient</li>
</ul>
<br />
On redémarre le réseau:
<code>
root@xxxxxx# /etc/init.d/networking force-reload
</code>

J'ai maintenant une IPv6 dans le scope Global :
<code>
root@xxxx# ifconfig
eth0      Link encap:Ethernet  HWaddr c8:0a:a9:c8:e8:4f
          inet adr:88.191.127.234  Bcast:88.191.127.255  Masque:255.255.255.0
          adr inet6: 2a01:e0b:1:127:ca0a:a9ff:fec8:e84f/64 Scope:Global
          adr inet6: fe80::ca0a:a9ff:fec8:e84f/64 Scope:Lien
</code>

Pour vérifier que votre conf est OK, rien ne vaut un ping :
<code>
root@xxxxx:/home/xavier# ping6 ipv6.google.com
PING ipv6.google.com(par03s03-in-x13.1e100.net) from 2a01:e0b:1:127:ca0a:a9ff:fec8:e84f eth0: 56 data bytes
64 bytes from par03s03-in-x13.1e100.net: icmp_seq=1 ttl=57 time=0.977 ms
64 bytes from par03s03-in-x13.1e100.net: icmp_seq=2 ttl=57 time=0.971 ms
</code>

Une fois que vous avez votre IPv6 opérationnelle, vous ajoutez un enregistrement DNS AAAA de votre domaine (vos domaines servi par virtual hosts) vers cette IP.

Si vous avez des des VM qui répondent à des IPv4 différentes (IPfailover chez dedibox) il va falloir toutes les configurer pour l'IPv6.
<i>( j'en ai pas encore donc là je vous laisse vous galérer (attention avec les MAC adresses virtuelles : Online peut vous banir du réseau))</i>

Ensuite il faut éventuellement configurer votre serveur web et vos vhosts si vous avez mis des spécificités IPv4 dans la conf (j'ai pas eu besoin car j'avais des VirtualHost *:80 dans mon apache2)

Et hop ça marche:
<code>
C:\Users\xraffin>ping xavierraffin.com
Envoi d'une requête 'ping' sur xavierraffin.com [2a01:e0b:1:127:ca0a:a9ff:fec8:e84f] avec 32 octets de données :
Réponse de 2a01:e0b:1:127:ca0a:a9ff:fec8:e84f : temps=107 ms
Réponse de 2a01:e0b:1:127:ca0a:a9ff:fec8:e84f : temps=60 ms
</code>
<center><i>Test depuis mon PC à la maison</i></center>

<h3  id="ipv6-lan">3) En tant qu'admin réseau en entreprise</h3>

C'est içi que les problématiques sont les plus complexes et les bouleversements les plus importants.

Si la suppression du NAT est maintenant possible elle n'est pas obligatoire, et il est probable que les entreprises choisissent de ne pas le faire pour des raisons évidentes de confidentialité (on identifie chaque machine par son IP unique).

Ensuite, le DHCP lui aussi peut disparaitre au profit de configurations automatique : affectation d'IP aléatoire (ou depuis la MAC) et découverte des routes par NDP :
<center>
<img src="/sites/xavierraffin.com/files/router_solicitation.png" />
<b>NDP découvre les nouvelles passerelles tout seul !</b> source : <a href="http://packetlife.net/blog/2008/aug/28/ipv6-neighbor-discovery/" target="_blank">packetlife.net</a>
</center>
Il n'est donc plus nécessaire de renseigner les passerelles dans le serveur DHCP : <b>le réseau LAN se configure tout seul</b> (ce qui est un avantage ou un inconvénient suivant le point de vue)

Pour menez à bien ces choix et pour s'y retrouver face à tous ces bouleversements (suppression d'ARP, de ICMP <a href="#transition">pour ceux qui n'ont pas suivi</a>), la formation des administrateurs réseau va devenir une priorité.

<h1 id="conclusion">Conclusion : IPv6 pour tisseo.fr ?</h1>
Ben oui, pour ceux <a href="/content/propos">qui me connaissent</a> ça doit sembler une question fatidique.

Pour ce qui est de tisseo.fr et mobi.tisseo.fr, ça me démange bien.
Maintenant, vu notre roadmap actuelle (on a plein de projets !), je ne pense pas qu'on puisse traiter ce sujet avant fin 2013, voir 2014.
Je vais garder un œil sur les statistiques de progression d'IPv6 en France pour motiver les équipes et la hiérarchie sur cette opération.

Pour notre LAN par contre et après discution avec notre admin réseau, ça semble pas pour tout de suite.
Et quand cela aura lieu il est probable que nous utiliserons du NAT quand même.

<b>Et vous ?</b> Allez-vous migrer en IPv6 ?
N'hésitez pas à vous exprimer dans les commentaires !

<i><u>Note :</u> Si des lecteurs érudits constate des erreurs ou des imprécisions dans ce que j'ai dit, n'hésitez pas à m'en faire part dans les commentaires</i>
