## Installation de IPSEC

## Information essentiels à propos de IPSEC
IPsec (Internet Protocol Security) est un cadre qui regroupe un jeu de protocoles de sécurité au niveau de la couche réseau ou de la couche de traitement des paquets de la communication réseau. 
IPsec fournit deux types de service de sécurité : Authentication Header (AH), qui permet essentiellement l'authentification de l'expéditeur des données, et Encapsulating Security Payload (ESP), qui prend en charge à la fois l'authentification de l'expéditeur et le chiffrement des données.
Les informations spécifiques associées à chacun de ces services sont insérées dans le paquet d’un en-tête qui suit l'en-tête du paquet IP. 
Des protocoles de clé distincts peuvent être sélectionnés, tels que le protocole ISAKMP/Oakley.

## Tutoriel
Pour mettre en place notre VPN IPSEC, il nous faut accéder à l’interface web de nos 2 Pfsense. Et activer l’IPSEC en créer des phases :

Les phases 1 de chaque Pfsense auront les adresse WAN du Pfsense d’en face.
Les phases 2 de chaque Pfsense auront les adresse LAN du Pfsense d’en face.

![image](https://user-images.githubusercontent.com/59647512/112834169-f46a4a00-9097-11eb-8e54-f51733b36440.png)
![image](https://user-images.githubusercontent.com/59647512/112834208-00560c00-9098-11eb-9339-5f90a6dc1dea.png)

On va ensuite créer des règles pour cela on se dirige dans « Firewall -> Rules » et des deux côtés on créer 2 règles :

![image](https://user-images.githubusercontent.com/59647512/112834232-0815b080-9098-11eb-89b8-21a561eabfad.png)


Une fois les règles et phases faites on active le tunnel et on doit obtenir un bon « ETABLISHED » avec un nouveau graphe à l’accueil qui montre le flux IPSEC.
![image](https://user-images.githubusercontent.com/59647512/112834255-11068200-9098-11eb-93c0-016ba031444a.png)

![image](https://user-images.githubusercontent.com/59647512/112834268-12d04580-9098-11eb-80a1-2d0f2938c5d4.png)


[retour au sommaire](https://yassineoby.github.io/PortFolio-Yassine-OUBOUYA/home.html)




