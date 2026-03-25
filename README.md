Pi-hole sur Docker (Raspberry Pi) - Setup
![piHole Workflow](/pihole.png)
Ce projet contient la configuration et le guide étape par étape pour faire fonctionner un serveur de blocage de publicités au niveau du réseau (DNS Sinkhole) en utilisant Docker et Pi-hole.

install Docker: https://docs.docker.com/engine/install/ubuntu/

À quoi sert ce projet ?
* Bloque les publicités et les trackers sur tous les appareils du réseau (TV, smartphones, consoles, PC).
* Améliore la vie privée en bloquant la télémétrie des objets connectés (IoT).
* Interface graphique pour surveiller le trafic en temps réel.


Si tu as le UFW :
```
sudo ufw allow 53/tcp
sudo ufw allow 53/udp
sudo ufw allow 80/tcp
```
Apres avoir configurer le docker-compose.yml

Run:
```
docker compose up -d
```
Configuration Post-Installation

Pour que le Pi-hole réponde aux requêtes provenant de votre routeur ou de vos appareils :

1.Accédez à "http://<IP-DU-RASPBERRY>/admin"
(cest possible que le mdp ne functione pas, il faut acceder via bash pour setup le mdp
run :
```
docker exec -it pihole bash
```
 dans le bash run :
 
```
pihole setpassword

```
)
2.Allez dans Settings > DNS.
3.Dans la section Interface settings, sélectionnez "Permit all origins".
4.Save


Configurer le router:
Modifier le dns server automatique pour manuel e pointer vers l'IP de ta machine (ou se trouve le pihole)


Sécurité et Bonnes Pratiques
L'utilisation de Pi-hole sur un Raspberry Pi est très sûre pour un usage domestique, mais il est important de respecter ces quelques règles de sécurité :

1. Ne jamais ouvrir le port 53 sur votre Box (Router)
Danger : Si vous créez une règle de "Port Forwarding" pour le port 53 (DNS) sur votre routeur (Swisscom, Salt, Sunrise), votre Pi-hole devient un Open Resolver.
Risque : Des attaquants externes peuvent utiliser votre Raspberry Pi pour lancer des attaques DDoS à travers le monde.
Solution : Laissez le port 53 fermé sur votre box. Le Pi-hole doit rester accessible uniquement depuis votre réseau local (LAN/WLAN).

2. Protection de l'Interface Admin
L'interface de gestion (/admin) est le cœur de votre configuration.
Risque : Toute personne connectée à votre Wi-Fi peut tenter d'accéder au panneau de contrôle.
Solution : Utilisez un mot de passe complexe pour la variable WEBPASSWORD dans votre fichier docker-compose.yml. Ne partagez jamais votre mot de passe réel sur GitHub.

3. Gestion de l'espace disque (Carte SD)
Le Pi-hole génère des journaux (logs) quotidiennement pour afficher les statistiques.
Risque : Si votre carte SD atteint 100% d'utilisation, le service DNS s'arrêtera brusquement, coupant ainsi l'accès internet à toute votre maison.
Solution : Surveillez régulièrement l'espace disque avec la commande df -h et nettoyez les anciens conteneurs avec docker system prune.

4. Accès SSH au Raspberry Pi
Le Pi-hole n'est aussi sûr que le système qui l'héberge.
Solution : Changez le mot de passe par défaut de votre utilisateur Raspberry (sudo raspi-config) et, si possible, utilisez des clés SSH pour vous connecter.



