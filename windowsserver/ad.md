## Installation de l'Active Directory

## Informations essentiels à propos de l'Active Directory

L'objectif principal d'Active Directory est de fournir des services centralisés d'identification et d'authentification à un réseau d'ordinateurs utilisant le système Windows, MacOs et encore Linux. Il permet également l'attribution et l'application de stratégies ainsi que l'installation de mises à jour critiques par les administrateurs. Active Directory répertorie les éléments d'un réseau administré tels que les comptes des utilisateurs, les serveurs, les postes de travail, les dossiers partagés (en), les imprimantes, etc. Un utilisateur peut ainsi facilement trouver des ressources partagées, et les administrateurs peuvent contrôler leur utilisation grâce à des fonctionnalités de distribution, de duplication, de partitionnement et de sécurisation de l’accès aux ressources répertoriées.

## Pré-requis

On va donc installer l'active Directory. Pour cela dans la barre d’outils on clique sur « Gérer » puis « Ajouter des rôles et fonctionnalités », On va cliquer 2 fois sur Suivant, puis à la 3ème fenêtre on va sur « Service AD DS » puis « Ajouter des fonctionnalités » 

![image](https://user-images.githubusercontent.com/59647512/112837907-c20f1b80-909c-11eb-8c14-a4c08b5a9e30.png)

On clique 3 fois sur « Suivant ».
Et on attend qu'une ligne apparais avec marquer « Promouvoir ce serveur en contrôleur de domaine ». Dans la nouvelle fenêtre on va ajouter une nouvelle forêt avec le comme nom « bts.lan », on valide puis on va entrez notre mot de passe puis revalider. On valider jusqu'à arriver sur l'installation. Une fois celle-ci faites notre ordinateur va redémarrer.
On vient de créer un domaine au nom de bts.lan. Il sera à rentrer dans les réglages généraux de notre Pfsense.

Pour la création d’un utilisateur il suffit de se diriger dans « Outils » -> « Utilisateurs et ordinateurs Active Directory » puis on créer un utilisateur :

![image](https://user-images.githubusercontent.com/59647512/112837959-d0f5ce00-909c-11eb-90bb-bc97c7d4e298.png)
![image](https://user-images.githubusercontent.com/59647512/112837975-d3f0be80-909c-11eb-80f6-ccc697904779.png)


[retour au sommaire](https://yassineoby.github.io/PortFolio-Yassine-OUBOUYA/home.html)
