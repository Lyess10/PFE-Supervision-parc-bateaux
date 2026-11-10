PFE - Supervision et Télémesure de Flotte EDO

1. Présentation du Projet

Ce projet de fin d'études (PFE) en ingénierie électronique et IoT a pour objectif de concevoir une solution complète de télémesure et de suivi à distance des paramètres de maintenance pour une flotte d'embarcations semi-rigides (6 à 9 mètres - moteurs YAMAHA 200cv).

La chaîne d'acquisition collecte les métriques moteur à bord, les transmet sans fil vers une station terrestre et les restitue sur un tableau de bord centralisé pour optimiser la maintenance en condition opérationnelle (MCO).

Développé initialement sous forme de prototype fonctionnel, le système a pour vocation d'être industrialisé et déployé à terme sur une flotte cible de plus de 500 embarcations, tout en garantissant la prise en compte des évolutions matérielles et des différentes générations de moteurs.

2. Architecture Générale du Système

Le système est découpé en quatre zones principales :

Zone Embarquée (Edge) :

Moteur YAMAHA 200cv et bus NMEA 2000 (CAN bus à 250 kbps).

Valise diagnostique d'acquisition.

Passerelle IoT (Gateway) basée sur un microcontrôleur ESP32 et un transceiver CAN (ex: SN65HVD230).

Zone Liaison Radio :

Transmission sans fil via un protocole de communication RF conforme aux normes Défense.

Zone Infrastructure & Backend :

PC Central / Serveur de réception à la Base Navale.

Système de gestion de base de données (BDD / Back-End) pour le stockage et la structuration des métriques.

Zone Application :

Dashboard "Supervision flotte EDO" pour la visualisation en temps réel et l'analyse de l'état du parc.

3. Matériel et Choix Techniques (Gateway)

Microcontrôleur : ESP32 (S3 / WROOM)

Justification : Périphérique CAN (TWAI) intégré, fréquence d'horloge de 240 MHz, faible consommation (modes Deep Sleep), connectivité native (Wi-Fi/BLE pour le debug sur le terrain) et coût réduit.

Interface Physique Bus CAN : Transceiver CAN 3.3V (SN65HVD230) assurant l'interface entre l'ESP32 et la prise NMEA 2000 / CAN_H / CAN_L.

Démarche de Prototypage : Maquettage sur cartes de développement du commerce pour valider le firmware et le dashboard, suivi d'une modélisation PCB sous KiCad en retour d'expérience (RETEX).

Perspective d'Industrialisation & Scalabilité :

Conception modulaire pensée pour supporter une montée en charge sur 500+ unités.

Abstraction des couches matérielles et logicielles pour assurer l'interopérabilité avec différentes générations d'embarcations et de motorisations.

4. Protocole de Communication (NMEA 2000)

Norme : Standard binaire basé sur le bus CAN (ISO 11783) opérant à 250 kbps.

Données : Transmission par PGN (Parameter Group Numbers) des variables moteurs (régime, températures, pressions).

Évolution : Préparation de la passerelle pour une interopérabilité future avec les standards Ethernet haut débit (NMEA OneNet).

5. Structure du Dépôt

/doc        : Documentation technique, synthèses des normes et études comparatives (NMEA 2000, ESP32 Benchmark).

/firmware   : Code source C++/Arduino pour l'ESP32 (lecture TWAI/CAN, traitement et envoi RF).

/hardware   : Schématiques de câblage et fichiers de conception PCB (KiCad).

/dashboard  : Code de l'interface graphique de supervision et scripts du serveur backend.
