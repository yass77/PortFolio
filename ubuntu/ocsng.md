## Installation OCS Inventory

### Informations essentiels et pré-requis

Open Computer and Software Inventory est une application conçue pour aider les administrateurs systèmes ou réseau à suivre les configurations matérielles et les logiciels sur le réseau. Il peut aussi déployer des paquets sur des postes Windows ou Linux.
Pour cela on rentre ces commandes sur notre serveur Ubuntu :


        sudo apt install apache2 php libapache2-mod-php mysql-server php-mysql
        sudo apt install php-curl php-gd php-intl php-json php-mbstring php-xml php-zip
        sudo apt install libdbd-mysql-perl libnet-ip-perl libsoap-lite-perl libxml-libxml-perl libc6-dev perl libapache2-mod-perl2 libxml-simple-perl libio-compress-perl libdbi-perl libapache-dbi-perl php7.0-mbstring 

Pour finir il suffit d’installer le paquet ocsinventory-server grâce à la commande :

        sudo apt-get install ocsinventory-server

## Finalisation

Après avoir configurer votre Apache et votre PHP il suffira de redémarrer Apache et de vous rendre sur le site https://IP_SERVER/ocsreports/index.php pour configurer votre OCS.
Pour les clients il suffira d’opter pour le paquet ocsinventory-client et de mettre l’IP de notre server.



[retour à l'acceuil](/README.md)
