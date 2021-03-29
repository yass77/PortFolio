## Installation Pfsense.

Afin de sécuriser et administrer notre serveur Windows, nous aurons besoin de mettre en place un pare-feu. Pour cela nous utiliserons l’un des plus connus dans le monde, Pfsense. Nous créerons une machine sous Windows pour avoir accès à l’interface graphique.
Pfsense : Pfsense est un routeur/pare-feu basé sur un système d’exploitation Linux (FreeBSD) pouvant être administré depuis une interface graphique.

Tutoriel :
On commence par télécharger l’image de PfSense
 
Une fois téléchargée, on démarre Win32 Disk Imager. On sélectionne l’image de Pfsense téléchargée précédemment, on prend le bon périphérique et on peut lancer l’écriture de l’image.
 


La clé est maintenant prête, il suffit juste de la brancher à un ordinateur.
Lors du démarrage, on appuie sur la touche nous permettant d’accéder au menu de sélection du disque de démarrage (F12 dans notre cas). On démarre sur la clé où l’on a mis notre Pfsense. Un écran de chargement va dérouler et une fenêtre sur fond bleu apparaitra.
On accepte.

On lance l’installation.
 
Une liste de disposition de clavier est affichée, on sélectionne celle nous concernant.
On valide en appuyant sur « entrée ». On choisit la partition de disque automatique car aucun paramètre particulier n’est à effectuer.

Le schéma de partition est demandé, plusieurs modèles sont proposés. On choisit ici le schéma BSD pour la partition de notre Pfsense

 
La taille de notre espace de stockage et son nom seront affichés, si tout est correcte il suffit juste de valider en appuyant sur « Finish »
 
Une confirmation est demandée, on « Commit ».
 
L’installation de Pfsense est terminée, la fenêtre demande si des modifications finales sont à effectuées dans le Shell, ici non.
 



Il ne reste plus qu’à « Reboot » et tout sera opérationnel.
 
Et voilà il reste plus qu’à configurer le DHCP. Pour ça on choisit l’option 2 quand nous arrivons à l’accueil.
 
On va configurer notre interface LAN afin de mettre en place un DHCP, pour ça on va donner l’adresse IPV4 192.168.1.10/24 en désactivant l’adresse IPV6 à notre Pfsense avec un DHCP de 192.168.1.100 à 192.168.1.200.
Une fois terminer on se connecter à notre interfaces web en tapant l’adresse WAN depuis un ordinateur dans le même réseau de notre Pfsense, on configure le nom de Pfsense, le domaine (cf. Active Directory), notre DNS principal et secondaire sans oublier notre timezone ! Nous sommes en Europe et plus précisément « Europe/Paris"


[retour au sommaire](https://yassineoby.github.io/PortFolio-Yassine-OUBOUYA/home.html)
