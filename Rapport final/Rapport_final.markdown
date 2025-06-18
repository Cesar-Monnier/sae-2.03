_Monnier César_                  
_De Witte Raphaël_ \
_Lebbrecht Evan_\
**groupe C**  \  
# SAÉ 1.03 : Rapport intermediaire

## Installation manuelle :
Commençons par l'installation manuelle, pour commencer, téléchargez _l'Iso bootable de Debian_ sur le site officiel [_debian.org_](https://www.debian.org/) puis allez sur le logiciel VirtualBox, puis appuyez sur le bouton « nouvelle », donnez un nom à votre nouvelle machine, puis choisissez le type de machine Linux, et prenez la version Debian 12 _Bookworm 64bits_. Choisissez suivant plusieurs fois, puis **« _Terminer_ »**
	![Menu de création de la machine virtuelle](image/instalation_maunelle_1.png)
	
	Vous voici dans _Grub_, ceci est un installateur qui va vous permettre de configurer votre machine une première fois.

Allez ensuite dans l'onglet configuration, puis stockage, cliquez sur le disque bleu, puis dans la partie **« choisissez un lecteur optique »**, cliquez sur le disque bleu et **« choisir un fichier disque »**, ici, sélectionnez votre fichier _".iso"_ précédemment téléchargé, qui fermez les menus.

Tout est prêt ! Vous pouvez désormais démarrer votre machine.
Vous voici dans _Grub_, ceci est un installateur qui va vous permettre de configurer votre machine une première fois.

![Choix du mode d'installation de debian](image/instalation_maunelle_2.png)

Maintenant, vous allez commencer par avoir un menu vous demandant de choisir le langage de notre système, choisissez français puis continuez. Choisissez ensuite votre zone géographique (pour permettre à l'heure de se calibrer). Enfin, choisissez le type de clavier que vous souhaitez utiliser (nous recommandons français) laissez le charger...
![Choix du nom de la machine](image/instalation_maunelle_3.png)


Vous devriez atteindre ce menu, qui vous permettra de donner un nom a votre machine, puis continuez. Vous n'avez pas besoin d'un nom de domaine, continuez sans rien remplir.

Vous allez maintenant configurer les utilisateurs

- Le _superuser_ (_root_) est l'administrateur de la machine et vous permettra de configurer votre machine à 100%, choisissez donc un mot de passe puis continuez.
- L'utilisateur normal, choisissez-lui un nom, un identifiant de mot de passe puis continuez.

Laissez-le charger... Vous allez ensuite configurer la partition de disque, pour commencer nous vous conseillons de choisir assisté, choisissez votre disque, puis « _tout dans une seule partition_ ».\  
![Partionnement du disque dur](image/instalation_maunelle_4.png)     
  
Une fenêtre explicative apparaît, choisissez continuer, confirmez une dernière fois. Puis laissez-le s'installer. S'il vous demande d'analyser d'autres supports, choisissez non.

Vous allez maintenant choisir un miroir (permet d'installer des applications), choisissez France, puis deb.debian.org si vous souhaitez le plus rapide, celui que vous souhaitez sinon. Puis continuez.
Vous n'avez pas de mandataire, laissez blanc et continuez comme cela continue à charger... On vous demande ensuite si vous voulez partager vos données avec Debian, c'est comme vous le souhaitez.

![Sélection des logiciels](image/instalation_maunelle_5.png)\     

Ici, on vous demande ce que vous voulez installer sur votre système de base, choisissez comme sur l'image puis continuez.

L'installation se finalise.
On vous demande d'installer _grub_, qui est votre bootladder (permet de démarrer Debian) choisissez oui, votre disque puis laissez la machine faire jusqu'au redémarrage.

Vous pouvez désormais utiliser votre machine en utilisant ces commandes simples :

- `apt install nom_du_logiciel` pour installer un logiciel
- `apt purge nom_du_logiciel` pour désinstaller un logiciel
- `useradd (username)` pour ajouter un uttilisateur
- `passwd (username)` pour ajouter/changer un mot de passe
- `groupadd [nomgroupe]` pour créer un nouveau groupe
- `usermod -aG (username) [nomgroupe]` pour ajouter un uttilisateur a un groupe pour ajouter les droits `sudo (admin) a un user : usermod -aG (username) sudo`.

![Insersion du l'image CD](image/instalation_maunelle_6.png) \  


Ensuite allez en haut de votre fenêtre pour votre VM et cliquez sur « insérer l'image CD … » comme sur l'image puis tapez dans votre terminal les commandes suivantes :
- `sudo mount /dev/cdrom /mnt`
- `sudo /mnt/VBoxLinuxAdditions.run`

Votre machine est maintenant configurée !

## Installation automatique : 
Nous allons maintenant passer à l'installation automatique qui est beaucoup plus rapide, récupérez le fichier zip autoinstall_Debian.zip de Moodle.

Créez une nouvelle machine comme montré plus haut : sur le logiciel _VirtualBox_, appuyez sur le bouton **« nouvelle »**, donnez un nom à votre nouvelle machine, puis choisissez le type de machine _Linux_, et prenez la version _Debian 12 Bookworm 64bits_. Choisissez suivant plusieurs fois, puis **« Terminer »**. Dans les dossiers, trouvez votre machine (peut être fait plus simplement en allant dans machine > voir dans l'explorateur de fichiers)
![Afficher l'explorateur de fichier](image/instalation_auto_1.png)\  

Puis décompressez ici votre archive.zip téléchargée plus tôt. A l'aide de votre terminal, placez-vous dans ce dossier, puis executez la commande suivante :
- `sed -i -E "s/(--iprt-iso-maker-file-marker-bourne-sh).*$/\1=$(cat /proc/sys/kernel/random/uuid)/" S203-Debian12.viso`
- `sed -i -E "s/(--iprt-iso-maker-file-marker-bourne-sh).*$/\1=$(cat /proc/sys/kernel/random/uuid)/" S203-Debian12.viso`

Cela donnera à votre fichier un _uid_ aléatoire et le rendra utilisable faites ensuite un **« nano »** sur le fichier _preseed.cfg_, ce fichier sert à la configuration automatique lors de l'installation. Puis faites les changements suivants :
1. Ligne 56 ajoutez _sudo_ à la fin (cela créera le groupe sudo et l'ajoutera a l'user).
2. Ligne 83 ajoutez : _mate-desktop_ (cela installera l'environnement graphique de Mate par défaut).
3. Enfin, ligne 84 tapez : `d-i pkgsel/include string sudo git curl bash-completion neofetch` (cela installera automatiquement les pakages sudo, git, ect…).

Bravo, vous n'avez plus qu'à aller dans l'onglet configuration, puis stockage, cliquez sur le disque bleu, puis dans la partie **« choisissez un lecteur optique »**, cliquez sur le disque bleu et **« choisir un fichier disque »**, ici, sélectionnez votre fichier _.viso_, puis fermez les menus.

Vous pouvez lancer votre machine, tout est fait automatiquement et plus rien n'est à configurer.
Nous allons maintenant configurer _git_ pour une utilisation confortable :
Nous avons au préalable installé une machine virtuelle avec git préinstaller dessus, utilisez donc les commandes suivantes afin de configurer votre dépôt local git :

- `git config --global user.name ''votrenomprenom"`
- `git config --global user.email "votre@email"`
- `git config --global init.defaultBranch "master"`

- ces trois commandes permettent de : 
	1. Créer un ''compte'' git a votre nom
	2. de l'associer à votre mail afin d'en faire une **« signature »**
	3. permet de créer une _branche principale_

	Nous allons maintenant installer une interface graphique permettant de visualiser et gérer les _dépôts git_. Allez sur le site [git-scm.com](http://git-scm.com/download/gui/linux) puis prendre la distribution que vous souhaitez (dans ce guide nous allons utiliser _SmartGit_) cliquez donc sur _smartGit_, puis **« download for linux »**.

	L’avantage de _SmartGit_ est qu'il est très simple à installer, comme expliqué dans le _readme_ du dossier téléchargé, il suffit de le décompresser dans le dossier de votre choix et de lancer le script en se plaçant dans le 

![Téléchargement pour linux](image/instalation_auto_2.png) \  

	dossier et tapant la commande :
- `bin/smartgit.sh`
Cela lance alors une interface, nous vous conseillons alors de choisir le mode standard et de confirmer.

![Confguration de SmartGit](image/instalation_auto_3.png)\  

Cela vous demande alors de choisir un nom et un mail, si vous avez tapé les commandes listées plus haut, cela serra rempli automatiquement.

![Terme d'utilisation](image/instalation_auto_4.png)\  

Cela vous demande alors de choisir un nom et un mail, si vous avez tapé les commandes listées plus haut, cela serra rempli automatiquement.

## Gitea

Pour installer _gitea_ :

Premièrement, afin de simplifier les choses, nous allons faire une redirection de ports, cela permettra d'accéder à l'application _gitea_ de la machine virtuelle plus facilement une fois installée.

Allez sur le logiciel de _VirtualBox_, puis dans le menu **« configuration »** et enfin **''réseau''**, cliquez sur avancer, puis sur le bouton ''redirection de ports'', pour cet exemple, nous allons utiliser le_ port 3000_.

![Redirection du port 3000](image/gitea_1.png)\  

Cette étape va permettre d'accéder au port de la machine en tapant _localhost :3000_ dans le navigateur internet.
Cliquez donc sur le bouton vert, puis remplissez comme suit :
  
![Règle de redirection de ports](image/gitea_2.png)  


Vous pouvez maintenant lancer votre machine virtuelle et vous connecter en tant que root (pour simplifier les choses). Nous allons installer _gitea_. Pour ce tuto, nous allons le faire à partir des binaires. Les étapes de l'installations peuvent aussi être trouvées ici : [docs.gitea.com](https://docs.gitea.com/installation/install-from-binary)
- `wget -O gitea https://dl.gitea.com/gitea/1.23.5/gitea-1.23.5-linux-amd64`
Cette commande sert à télécharger les binaires en premier lieu, a l'heure ou ce tuto est écrit, il télécharge la version la plus récente qui est la 1.23.5, libre à vous de modifier la commande avec la bonne version si ce tuto n'est plus à jour.
- Puis :
`chmod +x gitea`
Qui permettra de donner les droits d'exécutions aux fichiers.
- Ensuite :
`wget https://dl.gitea.com/gitea/1.23.5/gitea-1.23.5-linux-amd64.asc gpg --keyserver keys.openpgp.org --recv 7C9E68152594688862D62AF62D9AE806EC1592E2
gpg --verify gitea-1.23.5-linux-amd64.asc gitea-1.23.5-linux-amd64`

Ces commandes servent à télécharger un fichier de vérification, puis à l'utiliser afin de s'assurer que tous les fichiers sont bien en place.

Enfin tapez les commandes suivantes :
- `adduser \`    
- `--system \`
- `--shell /bin/bash \`
- `--gecos 'Git Version Control' \`
- `--group \`
- `--disabled-password \`
 - `--home /home/git \`
- `git`
Cela permet de créer un utilisateur par défaut, sans nom d'utilisateur ni mot de passe, qui servira uniquement à l'installation.

On va maintenant créer les dossiers de gitea manuellement tout en leur accordant les autorisations nécessaires :

- `mkdir -p /var/lib/gitea/custom` 
- `mkdir -p /var/lib/gitea/data`
- `mkdir -p /var/lib/gitea/log`
- `chown -R git:git /var/lib/gitea/`
- `chmod -R 750 /var/lib/gitea/`
- `mkdir /etc/gitea`
- `chown root:git /etc/gitea`
- `chmod 770 /etc/gitea`

Enfin, exportez gitea dans le bon dossier a l'aide de ces commandes :
- `export GITEA_WORK_DIR=/var/lib/gitea/`
- `cp gitea /usr/local/bin/gitea`

Une dernière commande afin de donner tous les droits d'accès nécessaires à gitea :
- `chmod 777 /bin`

Vous pouvez maintenant vous connecter en tant qu'utilisateur normal, et taper la commande
_gitea_
Afin de lancer gitea, puis pour y accéder, allez dans votre navigateur internet et cherchez :
_localhost :3000/_

Puis vous devriez tomber sur une fenêtre comme celle-ci :

![Configuration gitea](image/gitea_3.png)\  

Allez tout en bas, l'onglet **''paramètres du compte utilisateur''**
Et remplissez comme suit :
1. Nom d'uttilisateur : _gitea_
2. Mot de passe : _gitea_
3. E-mail : _git@localhost_

Vous pouvez ensuite cliquer sur le bouton **''installer gitea''** et le reste de l'installation ce fait automatiquement.

Vous pouvez maintenant utiliser gitea avec cette interface :  
![Installer gitea](image/gitea_4.png)\  

Pour des raisons de sécurité, nous allons enfin retirer certains droits d'accès aux dossiers de gitea afin de protéger votre ordinateur, dans un terminal en root tapez ces deux commandes :
- `chmod 750 /etc/gitea`
- `chmod 640 /etc/gitea/app.ini`

Tout est prêt ! Vous pouvez désormais utiliser votre ordinateur configuré correctement, et utiliser les différents outils _gitea_ et _Smartgit_ afin d'utiliser votre machine de manière optimale.

## Diverses questions 

### Des questions sur debians

1. *_Que signifie “64-bit” dans Debian 64-bit ?_*  
Un système d’exploitation de 64 bits est un type de système d’exploitation d’ordinateur conçu pour fonctionner avec des processeurs capables de traiter 64 bits de données à la fois. 
Source : [canada.lenovo.com](https://canada.lenovo.com/fr/ca/en/glossary/64-bit-system/?orgRef=https%253A%252F%252Fwww.google.com%252F )

2. *_Quelle est la configuration réseau utilisée par défaut ?_*  
L'interface de boucle locale est identifiée par le système par lo, et possède l'adresse IP par défaut « 127.0.0.1 ». Elle est visible via la commande ifconfig.
Source :
Source : [ubuntu-fr.org](https://guide.ubuntu-fr.org/server/network-configuration.html#:~:text=L'interface%20de%20boucle%20locale,visible%20via%20la%20commande%20ifconfig.&text=Par%20d%C3%A9faut%2C%20il%20devrait%20y,votre%20interface%20de%20boucle%20locale. )

3.  *_Quel est le nom du fichier XML contenant la configuration de votre machine ?_*  
La machine à pour nom : **“sae203.vbox”**.

4. *_Sauriez-vous le modifier directement ce fichier de configuration pour mettre 2 processeurs à votre machine ?_*  
pour mettre deux processeurs à la machine, il faut Changer la ligne 23 (`<CPU>`) en :
`<CPU count=”2”>`

Ou pour faire plus simple, on peut aller dans l’app virtualbox, sélectionner la machine, aller dans Configuration, Système, Processeur, Processors et changer la valeur CPU tout à droite en 2.


 5. *_Qu’est-ce qu’un fichier iso bootable ?_*   
un fichier iso bootable est un logiciel s’apparentant à une image disque, conçu pour démarrer au lancement de la machine, la machine démarre alors configurée comme l’image disque cela permet d’installer des systèmes (OS) par exemple
source : 
[winzip.com](https://www.winzip.com/fr/learn/file-formats/iso/#:~:text=Un%20fichier%20ISO%20amor%C3%A7able%20est,installer%20un%20syst%C3%A8me%20d'exploitation. )

 6. *_Qu’est-ce que MATE ? GNOME ?_*  
GNOME est un environnement de bureau linux dont MATE est un dérivé, ils servent a avoir une interface graphique personnalisées et des GNOME est un environnement de bureau linux dont MATE est un dérivé, ils servent a avoir une interface graphique personnalisées et des applications préinstallées
MATE (prononcer maté à l’espagnole) est un environnement de bureau
libre utilisant (dans un premier temps) la boîte à outils GTK+ 3.x et
destiné aux systèmes d’exploitation apparentés à UNIX. Il consiste en un
fork de GNOME et son nom vient du yerba maté dont les feuilles sont
utilisées pour préparer une boisson stimulante en Amérique latine 3 .
source :
- [openclassroom](https://openclassrooms.com/fr/courses/7170491-initiez-vous-a-linux/7251996-choisissez-votre-bureau-linux )
- [debian.org](https://debian-facile.org/doc:environnements:environnements)
7.  *_Qu’est-ce qu’un serveur web ? _* 
Un serveur web en linux est un système qui traite la demande d’un utilisateur, récupère la page web demandée et l’envoie à l'utilisateur.
Un « serveur web » peut faire référence à des composants logiciels (software)
ou à des composants matériels (hardware) ou à des composants
logiciels et matériels qui fonctionnent ensemble.
– Au niveau des composants matériels, un serveur web est un ordinateur
qui stocke les fichiers qui composent un site web (par exemple les
documents HTML, les images, les feuilles de style CSS, les fichiers
JavaScript) et qui les envoie à l’appareil de l’utilisateur qui visite
le site. Cet ordinateur est connecté à Internet et est généralement
accessible via un nom de domaine tel que mozilla.org.
– Au niveau des composants logiciels, un serveur web contient différents
fragments qui contrôlent la façon dont les utilisateurs peuvent accéder
aux fichiers hébergés. On trouvera au minimum un serveur HTTP.
Un serveur HTTP est un logiciel qui comprend les URL et le protocole
HTTP (le protocole utilisé par le navigateur pour afficher les pages
web).
Source : 
[ovhcloud](https://www.ovhcloud.com/fr/learn/what-is-web-server/#:~:text=Un%20serveur%20web%20est%20un,la%20page%20au%20serveur%20web)

8. *_Qu’est-ce qu’un serveur ssh ?_*
un SSH est un protocole qui permet au shell d’envoyer des commandes de manière sécurisée (le plus souvent en la cryptant)
SSH, ou Secure Socket Shell, est un protocole réseau qui permet aux administrateurs
d’accéder à distance à un ordinateur, en toute sécurité. SSH
désigne l'ensemble des utilitaires qui mettent en œuvre le protocole.
Source : 
[cloudfare](https://www.cloudflare.com/fr-fr/learning/access-management/what-is-ssh/#:~:text=Le%20protocole%20Secure%20Shell%20(SSH)%20est%20une%20m%C3%A9thode%20permettant%20d,les%20connexions%20entre%20les%20appareils)

9. *_Qu’est-ce qu’un serveur mandataire ?_*
Un serveur mandataire aussi appelé serveur proxy est un serveur délégué qui sert de relais et qui passe les requêtes d’un utilisateur à une machine.
Un serveur mandataire ou proxy (de l’anglais) est un serveur informatique
qui a pour fonction de relayer des requêtes entre un poste client et un
serveur. Les serveurs mandataires sont notamment utilisés pour assurer
les fonctions suivantes :
– mémoire cache ;
– la journalisation des requêtes (” logging “) ;
– la sécurité du réseau local ;
– le filtrage et l’anonymat.
L’utilité des serveurs mandataires est importante, notamment dans le
cadre de la sécurisation des systèmes d’information pour ces questions,
vous devrez trouver les réponses dans la documentation officielle et nous
source : 
[ubuntu](https://help.ubuntu.com/stable/ubuntu-help/net-proxy.html.fr#:~:text=Qu'est%2Dce%20qu',vous%20les%20transmettre%20ou%20non)


10. *_Comment peut-on savoir à quels groupes appartient l'utilisateur ?_*  
c’est stocké dans un fichier dans le système, pour le visualiser, utiliser la commande : cat /etc/group
source : manuel du terminal
 

11. *_Quelle est la version du noyau Linux utilisé par votre VM ?_*  
Debian 12 version la plus simple à trouver de par le fait que lien de
téléchargement sur la page principale de debian télécharge la version 12.
Nous utilisons celle-ci car celle-ci est la version actuelle. 
Source : 
 [Debian.org](https://www.debian.org/releases/)

12. *_À quoi servent les suppléments invités ?_*   Donner 2 principales raisons de les installer.
	Elles permettent d'améliorer l’affichage graphique. De partager le presse papier entre la machine virtuelle et la machine hôte. La possibilité de partager des répertoires entre la machine virtuelle et la machine hôte.

13. *_À quoi sert la commande mount (dans notre cas de figure et dans le cas général) ?_*  
La commande mount permet de demander au système d’exploitation de rendre un système de fichiers accessible, à un emplacement spécifié (le point de montage). La commande mount monte un système de fichiers indiqué comme répertoire à l’aide du paramètre Noeud:Répertoire, sur le répertoire spécifié par le paramètre Répertoire. Une fois la commande mount exécutée, le répertoire indiqué devient le répertoire racine du nouveau système de fichiers monté. Si vous entrez la commande mount sans option, elle affiche les informations suivantes sur les systèmes de fichiers montés :
– le noeud (si le montage est éloigné)
– l’objet monté
– le point de montage
– le type de système de fichiers virtuel
– l’horodatage du montage
– toute option de montage
Vous pouvez utiliser le répertoire /mnt comme point de montage local ou vous pouvez créer un répertoire à l’aide de la commande mkdir. Tout répertoire créé à l’aide de la commande mkdir doit être un sous-répertoire de votre répertoire d’accueil.
Source : le man du terminal

14. *_Qu’est-ce que le Projet Debian ?_*  
Debian est une distribution GNU/Linux. Il s'agit d'un système d'exploitation complet comprenant des logiciels avec leurs systèmes d'installation et de gestion, le tout basé sur le noyau Linux, et des logiciels libres (et notamment ceux du projet GNU).
Source :
[debian.org](https://www.debian.org/doc/manuals/debian-handbook/the-debian-project.fr.html#sect.what-is-debian)

15. *_D’où vient le nom Debian ?_* 
Debian n'est pas un acronyme. Ce nom est en réalité une contraction de deux prénoms : celui de Ian Murdock et de sa compagne d'alors, Debra. Debra + Ian = Debian.
SOurce : 
[debian.org](https://www.debian.org/doc/manuals/debian-handbook/the-debian-project.fr.html#sect.what-is-debian)

16. La maintenance
*_Il existe 3 durées de prise en charge (support) de ces versions : la durée minimale, la durée en support long terme (LTS) et la durée en support long terme étendue (ELTS). Quelles sont les durées de ces prises en charge ?_*  
Le cycle de vie d'une version couvre cinq ans : une prise en charge complète pendant les trois premières années(durée minimale) suivies de deux années supplémentaires (durée en support long terme). Les ETLS durent 5 ans selon le tableau (durée en support long terme étendue).
Source : 
[debian.org](https://www.debian.org/releases/index.fr.html)

17. *__Pendant combien de temps les mises à jour de sécurité seront-elles fournies ?_*  
Vu que c’est un des principaux sujets qui sont assurés par le support, (peu importe si étendu) c’est jusqu’à la fin de la ELTS. (ou LTS si il n’y a pas de ELTS)
Source : 
[debian.org](https://www.debian.org/releases/index.fr.html)

18. *_Nom générique, nom de code et version
Le projet dispose à tout instant de trois à six versions différentes de chaque logiciel, nommées Experimental, Unstable, Testing, Stable, Oldstable, et même Oldoldstable. Donc le minimum est 3.
Source : 
[debian.org](https://www.debian.org/releases/index.fr.html)

19. *_Chaque distribution majeure possède un nom de code différent. Par exemple, la version majeure actuelle (Debian 12) se nomme bookworm. D’où viennent les noms de code données aux distributions ?_*  
le nom de code donné aux différentes versions de debian sont des personnages de toy story. Vour trouverez ci-dessous un tableau contenant le nom, les date de sortie et de fin de vie et les états de chaque version : 

| Nom | Date de sortie | Fin de vie | État |
|-----|----------------|-----------|------|
|Buzz | 17/06/1996 | NA | Archivé |
|Rex | 12/12/1996 | NA| Archivé |
| Bo | 5/06/1997 | NA | Archivé |
| Hamm | 24/07/1998 | NA | stable obsolète |
| Slink | 09/03/1999 | NA | Stable obsolète |
| Potato | 14/08/2000 | NA | Stable obsolète |
| Wooody | 19/07/2002 | NA |  Stable obsolète | 
| Sarge | 06/06/2005 | NA | Stable obsolète | 
| Etch | 08/04/2007 | NA | Stable obsolète |
| Lenny | 14/02/2009 | NA | Stable obsolète | 
| Squeeze | 6/02/2011 | NA | Stable obsolète |
 Wheezy | 04/05/2013 | NA | Stable obsolète |
| Jessie | 25/04/2015 | 17/06/2018 | Archivée |
| Strench | 17/06/2017 | 18/07/2020 | Archivée |
| Buster | 06/07/2019 | 10/09/2022 | Archivée |
| Bullseye | 14/08/2021 | 14/08/2024| Oldstable |
| Bookworm | 10/06/2023 | 10/06/2026 | Stable |
| Trixie | NA| NA| Testing| 
|Forky| NA | NA | NA |

Source : 
- [Debian.org](https://www.debian.org/releases/)
- [Wikipedia.org](https://en.wikipedia.org/wiki/Debian_version_history)
20. *_L’un des atouts de Debian fut le nombre d’architecture (!= processeurs) officiellement prises en charge. Combien et lesquelles sont prises en charge par la version Bullseye ?_*  
	Il y a 9 architecture pris en charge par la version Bullseye:
– amd64 pour les PC AMD64 64 bits / Intel EM64T / x86-64.
– i386 pour les PC i386 32 bits / Intel IA-32.
– ppc64el pour PowerPC 64 bits little-endian Motorola/IBM PowerPC.
– s390x pour les serveurs IBM S/390 64 bits.
– armel pour ARM.-armhf pour les anciens matériels ARM et les architectures
32 bits plus récentes.
– arm64 pour les architectures ARM 64 bits Arch64.
– mipsel pour MIPS 32 bits little-endian.
– mips64el pour MIPS 64 bits little-endian.
[debian.org](https://www.debian.org/releases/bullseye/arm64/release-notes/chwhats-
new.fr.html#idm120)

21. *_Première version avec un nom de code
 Quel a été le premier nom de code utilisé ?
	Le premier nom de code est Buzz_*
 Le nom de code est Buzz
[debian.org](https://www.debian.org/releases/bullseye/arm64/release-notes/chwhats-
new.fr.html#idm120)
 22. *_Quand a-t-il été annoncé ?_*
Elle a été annoncée en 19 août 1991.
[debian.org](https://www.debian.org/releases/bullseye/arm64/release-notes/chwhats-
new.fr.html#idm120)
23. *_Quel était le numéro de version de cette distribution ?_*
	c'était la version 0.99.14               

24. *_Dernière nom de code attribué
 Quel est le dernier nom de code annoncé à ce jour ?_*
 	le nom de code de la version actuelle est Bookworm
	[debian.org](https://www.debian.org/releases/bullseye/arm64/release-notes/chwhats-
new.fr.html#idm120)
25. *_Quand a-t-il été annoncé ?_*
	annoncée le 23 avril 2022
[debian.org](https://www.debian.org/releases/bullseye/arm64/release-notes/chwhats-
new.fr.html#idm120)
 26. *_Quelle est la version de cette distribution ?_*
		 La version actuelle est la version 12
source :
[debian.org](https://www.debian.org/doc/manuals/debian-faq/ftparchives.fr.html#codenames)
Info en plus : 
Intel PRO/1000 MT Desktop (NAT)
Source : application VirtualBox

     ## Des questions sur git

1. *_Qu’est-ce que le logiciel gitk ? Comment se lance-t-il ? _*
gitk est un logiciel de visualisation graphique d’historique. C’est une sorte de d’interface GUI. Pour lancer gitk il faut utiliser la commande suivante “$ gitk [options de git log]”
Source :
[git-scm.com](https://git-scm.com/book/fr/v2/Annexe-A:-Git-dans-d%E2%80%99autres-environnements-Interfaces-graphiques)

2. *_Qu’est-ce que le logiciel git-gui ? Comment se lance-t-il ?_*
Git-gui est l’interface graphique permettant de ciseler les commits. Il s’utilise avec la commande “git gui”

 3. *_Pourquoi avez-vous choisi ce logiciel ?_*
Pour sa simplicité d'utilisation et d’installation, de plus c’est un logiciel payant (si utilisé à usage commercial) ce qui est une preuve de qualité.

4. *_Comment l’avez vous installé ?_*
en le téléchargeant sur internet et suivant les étapes du readme il suffit de décompresser dans le dossier de notre choix et de lancer le script bin/smartgit, qui quand uttilisé pour la première fois lance un installeur
Plus d'information sur la partie installation de gitea.

5. *_Comparer-le aux outils inclus avec git (et installé précédemment) ainsi qu’avec ce qui serait fait
en ligne de commande pure : fonctionnalités avantages, inconvénients_*
cette interface est plus claire et permet une meilleure lisibilité des différentes branches de git, étant donc plus façile a comprendre pour un débutant.

6. Qu’est-ce que Gitea ?
Gitea est un logiciel de service de développement auto-hébergé sans douleur. Il inclut Git hosting, évaluation de code, travail d’équipe, dépôt de paquet et CI/CD. 
Source :
[gitea.com](https://docs.gitea.com/)
7. À quels logiciels bien connus dans ce domaine peut-on le comparer (en citer au moins 2) ?
GitHub, Bitbucket and GitLab

Source :
[gitea.com](https://docs.gitea.com/)

8. Qu’est-ce qu’un fork (dans le domaine du développement logiciel bien entendu) ?
Un fork est la création d’un nouveau logiciel à partir du code source d’un logiciel déjà existant.

9. De quel logiciel Gitea est-il le fork ? Ce logiciel existe-t-il encore ?
Il est fork à partir de Gog






