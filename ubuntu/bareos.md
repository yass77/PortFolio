## Installation de Bareos

## Informations essentiels à propos de Bareos

Bareos est un programme de sauvegarde basé sur le modèle client-serveur, il va vous permettre de réaliser des sauvegardes sur votre système d’information par le réseau. En cas de perte de données, de mauvaise manipulation ou d’un ransomware vous aurez la possibilité de récupérer vos données.

## Pré-requis

Pour commencer le mieux c’est de se mettre en root afin d’éviter tout problème de permissions. 
Pour débuter on v modifier la liste des sources sur lequel notre serveur va devoir télécharger les paquets :

    nano /etc/apt/sources.list
    deb http://security.debian.org/debian-security stretch/updates main contrib
    deb-src http://security.debian.org/debian-security stretch/updates main contrib
    deb http://ftp.fr.debian.org/debian/ stretch main contrib
    deb http://ftp.fr.debian.org/debian/ stretch/updates main contrib

Bien sûr il faut créer le dépôt puis ajouter du texte :

    nano /etc/apt/sources.list.d/bareos.list
    deb http://download.bareos.org/bareos/release/latest/xUbuntu_18.04/ /

Téléchargeons désormais la clé et appliquer les changements :

    wget -q http://download.bareos.org/bareos/release/latest/Debian_9.0/Release.key -O- | apt-key add
    apt-get update

Téléchargeons Bareos et une base de données MariaDB, Bareos contient des scripts qui construit une base donnée, il suffit de lancer les scripts :

    apt-get install bareos bareos-database-mysql bareos-webui
    apt-get install mariadb-server
    /usr/lib/bareos/scripts/create_bareos_database
    /usr/lib/bareos/scripts/make_bareos_tables
    /usr/lib/bareos/scripts/grant_bareos_privileges
    systemctl start bareos-dir
    systemctl start bareos-fd
    systemctl start bareos-sd
    systemctl restart apache2

Une fois tout ça fait (c’était compliquer oulalala) on va se connecter via l’interface graphique de Bareos, pour ça on va entrer « bconsole » puis configurer notre accès web depuis le serveur :

    configure add console name=admin password= ‘admin’ profile=webui-admin

Il est important de mettre des guillemets autour du mot de passe afin de le crypter.



[retour à l'acceuil](/README.md)
