Pi-hole sur Docker (Raspberry Pi) - Setup

Ce projet contient la configuration et le guide étape par étape pour faire fonctionner un serveur de blocage de publicités au niveau du réseau (DNS Sinkhole) en utilisant Docker et Pi-hole.

install Docker: https://docs.docker.com/engine/install/ubuntu/

À quoi sert ce projet ?
* Bloque les publicités et les trackers sur tous les appareils du réseau (TV, smartphones, consoles, PC).
* Améliore la vie privée en bloquant la télémétrie des objets connectés (IoT).
* Interface graphique pour surveiller le trafic en temps réel.


Si tu as le UFW :
sudo ufw allow 53/tcp
sudo ufw allow 53/udp
sudo ufw allow 80/tcp

Apres avoir configurer le docker-compose.yml

Run:
docker compose up -d

Configuration Post-Installation

Pour que le Pi-hole réponde aux requêtes provenant de votre routeur ou de vos appareils :

1.Accédez à http://<IP-DU-RASPBERRY>/admin
(cest possible que le mdp ne functione pas, il faut acceder via bash pour setup le mdp, run : docker exec -it pihole bash
 dans le bash run : pihole setpassword,
)
2.Allez dans Settings > DNS.
3.Dans la section Interface settings, sélectionnez "Permit all origins".
4.Save


Configurer le router:
Modifier le dns server automatique pour manuel e pointer vers l'IP de ta machine (ou se trouve le pihole)






