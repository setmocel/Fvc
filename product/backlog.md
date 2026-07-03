# product/backlog.md

# Product Backlog – MVP ADS-B SDR

## Introduction

Ce backlog décrit le périmètre fonctionnel du premier MVP du récepteur ADS-B basé sur un SDR ADALM-Pluto.

L'objectif est de démontrer une chaîne complète permettant de :

- recevoir les signaux ADS-B à 1090 MHz ;
- démoduler et décoder les messages Mode S / ADS-B ;
- identifier les aéronefs détectés ;
- visualiser les résultats.

Le backlog est organisé par Épics afin de faciliter la planification technique et les futurs sprints de développement.

---

# Epic 1 – Acquisition RF

## Objectif

Mettre en place la chaîne de réception radio avec l'ADALM-Pluto.

### US-1.1 – Configuration du SDR

**En tant que** développeur  
**Je veux** configurer automatiquement l'ADALM-Pluto pour la réception ADS-B  
**Afin de** recevoir correctement les signaux à 1090 MHz.

**Priorité :** Haute

**Critères d'acceptation**

- le SDR est détecté automatiquement ;
- la fréquence est configurée à 1090 MHz ;
- le taux d'échantillonnage est configurable ;
- le gain peut être ajusté.

**Dépendances**

- pilotes ADALM-Pluto
- bibliothèque IIO/libiio

---

### US-1.2 – Acquisition des échantillons IQ

**En tant que** système

**Je veux** acquérir un flux IQ continu

**Afin de** transmettre les données au pipeline de traitement.

**Priorité :** Haute

**Critères d'acceptation**

- acquisition continue ;
- absence de perte importante d'échantillons ;
- possibilité d'arrêter proprement le flux.

**Dépendances**

- performances USB
- taille des buffers

---

# Epic 2 – Démodulation ADS-B

## Objectif

Transformer le signal RF en impulsions exploitables.

### US-2.1 – Détection des préambules ADS-B

**Priorité :** Haute

**Critères d'acceptation**

- détection des préambules conformes à la norme ADS-B ;
- faible taux de faux positifs ;
- journalisation des détections.

**Dépendances**

- qualité du signal RF

---

### US-2.2 – Démodulation des trames

**Priorité :** Haute

**Critères d'acceptation**

- conversion correcte des impulsions en bits ;
- gestion des trames courtes et longues ;
- calcul du taux d'erreurs.

**Dépendances**

- algorithme de synchronisation

---

# Epic 3 – Décodage Mode S / ADS-B

## Objectif

Extraire les informations utiles des messages.

### US-3.1 – Décodage des messages Mode S

**Priorité :** Haute

**Critères d'acceptation**

- décodage des Downlink Formats pris en charge par le MVP ;
- vérification du CRC ;
- rejet des trames invalides.

**Dépendances**

- bibliothèque de décodage ou implémentation interne

---

### US-3.2 – Identification des aéronefs

**Priorité :** Haute

**Critères d'acceptation**

- extraction de l'adresse ICAO ;
- extraction de l'identifiant (callsign) lorsqu'il est disponible ;
- maintien d'une liste des aéronefs actifs.

**Dépendances**

- décodage correct des messages ADS-B

---

### US-3.3 – Décodage des informations de position

**Priorité :** Moyenne

**Critères d'acceptation**

- décodage des messages de position lorsque les données nécessaires sont disponibles ;
- affichage latitude/longitude ;
- indication lorsqu'une position ne peut pas être calculée.

**Dépendances**

- implémentation CPR (Compact Position Reporting)

---

# Epic 4 – Visualisation

## Objectif

Afficher les résultats de manière exploitable.

### US-4.1 – Liste des aéronefs détectés

**Priorité :** Haute

**Critères d'acceptation**

- affichage en temps réel ;
- rafraîchissement automatique ;
- affichage minimum :
  - ICAO
  - Callsign
  - Nombre de messages reçus
  - Heure de dernière réception

**Dépendances**

- pipeline de décodage

---

### US-4.2 – Affichage des informations détaillées

**Priorité :** Moyenne

**Critères d'acceptation**

- affichage de la position (si disponible) ;
- altitude ;
- vitesse ;
- cap.

**Dépendances**

- disponibilité des messages ADS-B correspondants

---

# Epic 5 – Qualité et Exploitabilité

## Objectif

Garantir un prototype robuste et réutilisable.

### US-5.1 – Journalisation

**Priorité :** Moyenne

**Critères d'acceptation**

- journal des erreurs ;
- journal des événements principaux ;
- niveaux de log configurables.

---

### US-5.2 – Configuration du système

**Priorité :** Moyenne

**Critères d'acceptation**

- paramètres centralisés ;
- fréquence configurable ;
- gain configurable ;
- taux d'échantillonnage configurable.

---

### US-5.3 – Documentation d'installation

**Priorité :** Basse

**Critères d'acceptation**

- procédure d'installation ;
- procédure de lancement ;
- dépendances documentées.

---

# Priorisation globale

| Epic | Priorité |
|------|----------|
| Acquisition RF | Haute |
| Démodulation ADS-B | Haute |
| Décodage Mode S / ADS-B | Haute |
| Visualisation | Haute |
| Qualité & Documentation | Moyenne |

---

# Questions ouvertes

## Architecture

- Quel langage principal sera retenu (C++, Rust, Python, autre) ?
- Quelle architecture logicielle (pipeline, événements, modules) sera adoptée ?
- Une bibliothèque existante de décodage ADS-B sera-t-elle utilisée ou un développement interne est-il privilégié ?

## Performance

- Quel débit minimal doit être garanti ?
- Quel taux maximal de perte de trames est acceptable ?
- Quels objectifs de consommation CPU et mémoire sont visés ?

## Visualisation

- Le MVP doit-il proposer une interface graphique ou une interface en ligne de commande suffit-elle ?
- Une cartographie est-elle prévue après le MVP ?

## Validation

- Quels jeux de données IQ enregistrés seront utilisés pour les tests ?
- Quels indicateurs permettront de mesurer les performances radio (sensibilité, taux de décodage, portée) ?

## Évolutions futures

- Support des messages TIS-B.
- Export des données (JSON, CSV, MQTT).
- Intégration avec des outils comme dump1090 ou Virtual Radar Server.
- Affichage cartographique temps réel.
- Déploiement embarqué directement sur la plateforme cible.
