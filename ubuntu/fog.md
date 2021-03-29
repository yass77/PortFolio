## Installation de FOG 1.5.8

### Informations essentiels à propos de FOG

Fog est un outil de cloning et de management. Il va nous permettre de cloner et de déployer plusieurs ordinateurs simultanément. Par exemple déployer une mis à jour ou bien un logiciel, ça nous fait gagner du temps et le temps c’est de l’argent. Attention ! Pour ce logiciel il est nécessaire d’allouer minimum 60 Go d’espace de stockage à votre serveur.

## Pré-requis

Pour Fog c’est très simple, il se met sur un serveur Ubuntu 18.04.4 LTS et il suffit de taper cette suite de commande :

    sudo wget https://github.com/FOGProject/fogproject/archive/1.5.8.tar.gz
    sudo -i
    tar -xzvf fogproject-1.5.8.tar.gz
    cd fogproject-1.5.8/bin
    ./installfog.sh

Il se lancera alors l’installation et il faudra suivre ses étapes :
Choice : 2 -> Type of installation : N -> (Si adresse IP est bonne) Change network : N  -> FOG DHCP : Y   -> Additionnal packages : N
A l’étape suivante, FOG donne une adresse web avec des identifiants, il faut se connecter depuis un ordinateur situé dans le même réseau que notre serveur Ubuntu. Sur la page web et cliquer sur « Install/Upgrade Now », une fois cette étape faite on tape entrée sur le serveur Ubuntu et FOG apparait.

![image](https://user-images.githubusercontent.com/59647512/112829150-fd0b5200-9090-11eb-8752-40f75c7586ad.png)

### Déploiement d’une image Windows depuis FOG

Après avoir installé FOG il faut l’utiliser. Pour cela on va d’abord capturer une image d’un Windows que l’on a nous-même fait. Pour cela on redémarre un Windows situé dans le même réseau que FOG afin de rentrer dans le bios afin d’enregistrer la machine. Un chargement se fera plus ou moins long. Cette étape va enregistrer notre Ordinateur dans la base de données de FOG. Une fois cette étape faites notre machine apparait dans la liste des hosts :

![image](https://user-images.githubusercontent.com/59647512/112829186-08f71400-9091-11eb-96c6-bb4d493539a2.png)

On va cliquer sur le bouton jaune « capture » afin de créer la tâche pour FOG, on lui demandera qu’au prochain redémarrage du PC, FOG copie ce PC dans sa base données. Grosso modo on sauvegarde une copie de Windows sur notre serveur Ubuntu. 

![image](https://user-images.githubusercontent.com/59647512/112829284-2deb8700-9091-11eb-997f-f3911289a00c.png)

Elle sera donc stockée parmi les images de FOG. Pour la déployer il suffit de mettre un ordinateur dans le même réseau que notre amis FOG, sans OS l’ordinateur va booter sur la carte réseau, ce qui va appeler FOG à nous fournir la liste de ses images, il suffira de choisir l’image Windows et FOG installe Windows sur la machine et l’enregistre.

![image](https://user-images.githubusercontent.com/59647512/112829307-36dc5880-9091-11eb-988e-c15a3f3756c6.png)



[retour au sommaire](https://yassineoby.github.io/PortFolio-Yassine-OUBOUYA/home.html)
