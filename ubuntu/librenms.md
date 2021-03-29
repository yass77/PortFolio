## Installation LibreNMS

Librenms est une surveillance de réseau basée sur PHP/Mysql/SNMP qui inclut le support d’une large gamme de matériel réseau et de systèmes d’exploitation, y compris Cisco, Linux, Juniper, Foundry, et beaucoup plus.
Librenms est une fourche communautaire de la dernière version d’Observium sous licence GPL.
Pour pouvoir installer LIbrenMS sur notre machine virtuelle, nous aurons besoin tout d’abord de télécharger des paquets nécessaires à l’utilisation de celui-ci :

    sudo apt-get update
    sudo apt-get upgrade
    sudo apt install software-properties-common
    sudo add-apt-repository universe
    sudo apt update
    sudo apt install curl composer fping git graphviz imagemagick mariadb-client mariadb-server mtr-tiny nginx-full nmap php7.2-cli php7.2-curl php7.2-fpm php7.2-gd php7.2-json php7.2-mbstring php7.2-mysql php7.2-snmp php7.2-xml php7.2-zip python-memcache python-mysqldb rrdtool snmp snmpd whois

On créer un utilisateur librenms : 

    sudo useradd librenms -d /opt/librenms -M -r
    sudo usermod -a -G librenms www-data

On télécharge LibreNMS : 

    sudo cd /opt
    sudo git clone https://github.com/librenms/librenms.git 

Puis on configure les permissions :

    sudo chown -R librenms:librenms /opt/librenms
    sudo chmod 770 /opt/librenms
    sudo setfacl -d -m g::rwx /opt/librenms/rrd /opt/librenms/logs /opt/librenms/bootstrap/cache/ /opt/librenms/storage/
    sudo setfacl -R -m g::rwx /opt/librenms/rrd /opt/librenms/logs /opt/librenms/bootstrap/cache/ /opt/librenms/storage/

Et pour finir les dependances PHP :

    sudo su – librenms
    ./scripts/composer_wrapper.php install --no-dev
    exit

Passons à la base de données. Ici on va utiliser MariaDB (pour changer un peu), j’ai délibérément laissé « password » comme mot de passe : 

    sudo systemctl restart mysql
    sudo mysql -uroot -p
    CREATE DATABASE librenms CHARACTER SET utf8 COLLATE utf8_unicode_ci;
    CREATE USER 'librenms'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON librenms.* TO 'librenms'@'localhost';
    FLUSH PRIVILEGES;
    exit;


On va configurer le fichier 50-server.conf, pour cela on rentre cette commande :

    sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf

Dans le fichier on va rajouter de lignes dans la section [mysqld] :

    innodb_file_per_table=1
    lower_case_table_names=0

Puis on redémarre mysql :

    sudo systemctl restart mysql
    
Passons à la partie web de notre server. On va s’assurer que la timezone est correctement mise, la liste de toute les timezone que supporte PHP se trouve ici « https://php.net/manual/en/timezones.php ». 
Pour nous ça sera « Europe/Paris », et ça dans les deux fichiers ci-dessous :

    sudo nano /etc/php/7.2/fpm/php.ini
    sudo nano /etc/php/7.2/fpm/php.ini
    sudo systemctl restart php7.2-fpm

Puis on configure NGINX, pour ça on va modifier le fichier librenms.conf situé dans notre dossier NGINX, et on rajoute un bout de code :

    sudo nano /etc/nginx/conf.d/librenms.conf
    server {
        listen      80;
        bts librenms.example.com;
        root        /opt/librenms/html;
        index       index.php;
        charset utf-8;
        gzip on;
        gzip_types text/css application/javascript text/javascript application/x-javascript image/svg+xml text/plain text/xsd text/xsl text/xml image/x-icon;
    location / {
        try_files $uri $uri/ /index.php?$query_string;}
    location /api/v0 {
        try_files $uri $uri/ /api_v0.php?$query_string;}
    location ~ \.php {
        include fastcgi.conf;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;}
    location ~ /\.ht {
        deny all;}
    }
    sudo rm /etc/nginx/sites-enabled/default
    sudo systemctl restart nginx
    
Pour le code rajouter au-dessus on a bts à la 3ème ligne car notre server Ubuntu se nomme bts.
Nous avons bientôt fini, on finit de configurer SNMPD:

    sudo cp /opt/librenms/snmpd.conf.example /etc/snmp/snmpd.conf
    sudo nano /etc/snmp/snmpd.conf

Dans le fichier on modifie RANDOMSTRINGGOESHERE par public.

    curl -o /usr/bin/distro https://raw.githubusercontent.com/librenms/librenms-agent/master/snmp/distro
    sudo chmod +x /usr/bin/distro
    sudo systemctl restart snmpd

On copie les fichiers .cron et .logrotate dans notre librenms puis on configure les permissions :

    sudo cp /opt/librenms/librenms.nonroot.cron /etc/cron.d/librenms
    sudo cp /opt/librenms/librenms.nonroot.cron /etc/cron.d/librenms
    sudo chown -R librenms:librenms /opt/librenms
    sudo setfacl -d -m g::rwx /opt/librenms/rrd /opt/librenms/logs /opt/librenms/bootstrap/cache/ /opt/librenms/storage/
    sudo setfacl -R -m g::rwx /opt/librenms/rrd /opt/librenms/logs /opt/librenms/bootstrap/cache/ /opt/librenms/storage/

La partie server et terminer. On se connecte sur notre interfaces WEB de LibreNMS via le lien : http://librenms.example.com/install.php
Et voilà notre LibreNMS configurer et prêt à l’emplois !
