## Installation Windows Server 2016

## Pré-requis

On démarre notre serveur avec l’iso Windows 2016 et on va tomber sur une page de sélection de langues après quelques minutes : 
On cliquera sur le bouton « Installer maintenant » sur la fenêtre suivante.

![image](https://user-images.githubusercontent.com/59647512/112837420-28e00500-909c-11eb-9239-bb446bb8815e.png)

Pour la clé d’activation il suffira de la rentrer dans le champ réservé ou bien de cliquer en bas à droite sur « Je n’ai pas de clé produit »
On va ensuite sélectionner « Windows Server 2016 Standard (Expérience Utilisateur) » afin d’obtenir une interface graphique pour une meilleure utilisation.

![image](https://user-images.githubusercontent.com/59647512/112837436-2e3d4f80-909c-11eb-93ce-cf4c571a679f.png)

Pour le stockage il faudra sélectionner le mode personnalisé et supprimer les autres disques afin qu’il en reste qu’un seul (ci-contre) effectif non supprimable 

![image](https://user-images.githubusercontent.com/59647512/112837453-32696d00-909c-11eb-96a9-e18713cd66fd.png)

Un chargement plus ou moins long se fera et un redémarrage aura lieu laissant apparaitre cette page d’informations où il faudra renseigner un mot de passe robuste.

![image](https://user-images.githubusercontent.com/59647512/112837462-372e2100-909c-11eb-97c7-df40cd8e220a.png)

Le serveur va se démarrer et l’installation sera alors terminer. Il faudra alors se connecter avec les informations fournis, une fois connecter une fenêtre va s'ouvrir, on clique sur la 1ere étape qui est de configurer le server local, après cela on va changer le nom de l'ordinateur en cliquant dessus puis sur « modifier » dans la nouvelle fenêtre. 
Un redémarrage de l'ordinateur est nécessaire. On va ensuite mettre le réseau en statique, pour cela on va dans « Serveur Local » dans le menu de gauche. 

![image](https://user-images.githubusercontent.com/59647512/112837519-48772d80-909c-11eb-869c-5ac59e22c4a9.png)

Puis on clique sur l’Ethernet, vous va faire un clic droit « statut » sur le réseau qui s'affiche puis propriété. On décoche « Protocole IPv6 ». On clique sur « Protocole IPv4 » puis sur « Propriété ». On va attribuer une adresse IP à notre ordinateur. Dans notre cas on a :

![image](https://user-images.githubusercontent.com/59647512/112837535-4dd47800-909c-11eb-9136-fbb9d7bfd2ba.png)

L'étape suivant serai d'installer notre Actice Directory, on se donne rendz-vous [ici](https://yassineoby.github.io/PortFolio-Yassine-OUBOUYA/windowsserver/ad.html)


