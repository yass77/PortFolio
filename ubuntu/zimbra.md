## Installation de Zimbra

## Informations essentiels à propos de Zimbra

Zimbra n’est d’autre qu’un cousin de Outlook 2.0 il permet d’obtenir son propre mail (nomprénom@monentreprise.com). Ici nous avons installer Zimbra sur Ubuntu 18.04.1 LTS.

## Pré-requis

Afin d’installer Zimbra il est nécessaire d’avoir plus de 60 Gb d’espace de stockage. D’abord modifier un fichier yaml :

    sudo vim /etc/netplan/50-cloud-init.yaml
    # This file is generated from information provided by
    # the datasource.  Changes to it will not persist across an instance.
    # To disable cloud-init's network configuration capabilities, write a file
    # /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
    # network: {config: disabled}
    network:
        ethernets:
            enp0s3:
                addresses: [192.168.1.111/24]
                gateway4: 192.168.1.10
                nameservers:
                addresses: [192.168.2.51,1.1.1.1]
            dhcp4: no
        version: 2

On applique changement puis on modifiera notre nom ainsi que celui de notre machine pour qu’il soit différent du mot « Zimbra »

    sudo netplan apply
    sudo vim /etc/hostname
    sudo vim /etc/hosts
    127.0.0.1 localhost
    192.168.0.253 nomFQDN.mondomaine.fr nomFQDN
 
    # The following lines are desirable for IPv6 capable hosts
    ::1 localhost ip6-localhost ip6-loopback
    ff02::1 ip6-allnodes
    ff02::2 ip6-allrouters

Enfin on modifie le fichier resolv.conf avec notre serveur DNS puis on reboot :

    sudo vim /etc/resolv.conf
    nameserver 127.0.0.1
    nameserver 192.168.2.51
    nameserver 1.1.1.1
    reboot



On télécharge la dernière version de Zimbra, décompresse et lance le script d’installation :

    wget https://files.zimbra.com/downloads/8.8.15_GA/zcs-8.8.15_GA_3794.UBUNTU18_64.20190329045002.tgz
    tar xzvf zcs-8.8.15_GA_3794.UBUNTU18_64.20190329045002.tgz
    cd zcs-8.8.15_GA_3794.UBUNTU18_64.20190329045002 
    sudo ./install.sh

Il va se lancer une série de ligne qui nous fera passer pour des hackers professionnels dans l’installation d’une messagerie de fortune.
Voici les étapes importantes à ne pas louper :

    Install zimbra-ldap [Y] Y
    Install zimbra-logger [Y] Y
    Install zimbra-mta [Y] Y
    Install zimbra-dnscache [Y] Y
    Install zimbra-snmp [Y] Y
    Install zimbra-store [Y] Y
    Install zimbra-apache [Y] Y
    Install zimbra-spell [Y] Y
    Install zimbra-memcached [Y] Y
    Install zimbra-proxy [Y] Y
    Install zimbra-drive [Y] Y
    Install zimbra-imapd (BETA - for evaluation only) [N] N
    Install zimbra-chat [Y] Y
    The system will be modified.  Continue ? [N] Y

Une fois ces étapes passées on doit configurer la TimeZone (Menu 1 puis 7 et enfin  104 pour sélectionner « Europe/Berlin ». On revient au menu principal pour sélectionner le menu 7 le « zimbra-store » pour configurer le mot de passe administrateur dans le sous-menu 4. Une fois des deux choses faites on fait « r » pour valider les configurations finales. De nouvelles lignes apparaissent puis une fois finis la phrase « Starting servers... ». 


On vérifie l’état de Zimbra et contrôlons notre port d’administration de serveur :

    sudo su -
    su zimbra
    zmcontrol status
    netstat –e –l –p | grep 7071
    
Si tout est bon il suffit de se connecter à notre serveur via notre serveur web en tapant notre adresse IP :

![image](https://user-images.githubusercontent.com/59647512/112831592-7789a100-9094-11eb-9063-d5908529dee9.png)

