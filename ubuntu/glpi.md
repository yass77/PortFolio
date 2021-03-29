## Informations à propos de GLPI

Pour nous aider à gérer notre parc informatique nous avons comme outil des gestionnaires de service informatique comme GLPI.
GLPI (Gestionnaire Libre de Parc Informatique) : GLPI est un logiciel libre des services informatiques et de gestion des services d’assistance. Le logiciel est édité en PHP.

## Tutoriel

Pour pouvoir installer GLPI sur notre machine virtuelle, nous aurons besoin tout d’abord de télécharger apache2 pour le serveur web. On commence par vérifier si tous les paquets de notre machine sont à jour.

    sudo apt-get update
    sudo apt-get upgrade

On télécharge le paquet de apache2.

    sudo apt-get install apache2

Une confirmation nous sera demandée.
Souhaitez-vous continuer ? [O/n] 

On appuie sur « Entrée ».
On démarre ensuite le service apache et on l’active.

    systemctl start apache2
    systemctl enable apache2

Pour vérifier si notre serveur Apache2 à bien été installé, il suffit d’aller sur la page apache. Pour cela, on chercher l’adresse ip de notre serveur Ubuntu en tapant ifconfig. On rentre cette adresse sur notre navigateur internet, si toutes les étapes ont bien été effectué [cette page devrait s'afficher](https://i.imgur.com/ouEwnnu.png).
-

L’installation de Apache est terminée, on s’attaque maintenant à celle de MySQL. Comme pour apache2, on télécharge le paquet de MySQL pour avoir une base de données.

    sudo apt-get install mysql-server

Une fois le téléchargement fini, on va créer une base de données pour GLPI.
On accède à MySQL avec la commande :

    sudo mysql 

Puis on crée la base de données, il faut remplacer ‘user_name’ et ‘user_password’ par un nom et mot de passe que l’on choisit nous-même. Le ‘%’ nous permet de nous connecter sur n’importe quel hôte. On attribura tous les droits à l’utilisateur, cela nous servira plus tard :

    CREATE DABATASE glpi;
    USE glpi;
    CREATE USER ‘user_name’@’%’ IDENTIFIED BY ‘user_password’;
    GRANT ALL PRIVILEGES ON *.* TO 'database_user'@'localhost';


La base de données et l’utilisateur sont créés, on peut donc passer à l’installation de GLPI.
Pour fonctionner, GLPI a besoin de nombreux modules PHP :

    sudo apt-get -y install php php-{curl,gd,imagick,intl,apcu,recode,memcache,imap,mysql,cas,ldap,tidy,pear,xmlrpc,pspell,gettext,mbstring,json,iconv,xml,gd,xsl}
    sudo apt-get -y install apache2 libapache2-mod-php


Pour télécharger GLPI, nous aurons besoin d’un programme nous permettant de télécharger des fichiers depuis le web :

    sudo apt-get -y install wget


On va sur le site de GLPI pour voir qu’elle est la dernière version disponible : https://glpi-project.org/downloads/ (ici c’est la 9.5.4).

    wget https://github.com/glpi-project/glpi/releases/download/9.5.4/glpi-9.5.4.tgz


Il faut remplacer le ‘$VER’ par la version actuelle de GLPI. On extrait le fichier télécharger car c’est une archive :

    tar xvf glpi-9.5.4.tgz


On déplace le fichier GLPI décompressé dans le fichier /var/www/html/

    sudo mv glpi /var/www/html/

On accorde à Apache les droits du répertoire :

    sudo chown -R www-data:www-data /var/www/html/glpi/

 
Si le téléchargement et la décompression se sont effectués avec succès, on peut accéder à l’installation de GLPI depuis Internet.

    http://’adresse_de_notre_serveur’/glpi

Selectionnez la langue que vous parlez (en l(occurence français), acceptez les règles d’utilisation (à lire selon votre envie) et procedez à l'installation.
Une page s’affiche ensuite avec la liste des prérequis, s’il en manque une croix rouge s’affichera sur la ligne correspondante. Normalement tout est bon si toutes les étapes ont bien été effectuées. La dernière ligne affiche une erreur mais c’est normal on peut continuer l’installation.
 
Arriver à [cette page](https://i.imgur.com/Cxig4gy.png) on choisit le serveur SQL, pour notre cas c’est localhost. A la place de ‘user_name’ et ‘user_password’, on met les identifiants définis précédemment.

Si la base de données à bien été créée, glpi devrait être disponible lors du choix de la base.
 
La page va ensuite se mettre à charger pendant un certain temps, ensuite [une page](https://i.imgur.com/hS3qORI.png) va s’afficher pour nous annoncer que GLPI est bien installé.

![image](https://user-images.githubusercontent.com/59647512/112827167-46a66d80-908e-11eb-9482-cad7b20d9ff5.png)
