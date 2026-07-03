# Project Charter – ADS-B SDR

## Contexte

First Virtual Company lance un projet de recherche et développement visant à concevoir un récepteur ADS-B basé sur un SDR ADALM-Pluto.

Le projet a pour ambition de démontrer la faisabilité d'une chaîne complète de réception, décodage et visualisation des données ADS-B tout en construisant une architecture logicielle réutilisable.

---

## Objectifs

### Objectif principal

Développer un prototype fonctionnel capable de recevoir, décoder et afficher les données ADS-B à 1090 MHz à partir d'un ADALM-Pluto SDR dans un horizon de trois mois.

### Objectifs détaillés

- Recevoir les trames ADS-B à 1090 MHz
- Réaliser l'acquisition RF du signal
- Démoduler les trames ADS-B
- Décoder les messages Mode-S
- Afficher les aéronefs détectés
- Étudier les performances radio de la solution
- Construire une architecture logicielle réutilisable
- Maintenir un coût matériel faible
- Produire une documentation complète du système

---

## Livrables

### L1 – Architecture du système

- Description de l'architecture matérielle et logicielle
- Diagrammes de flux de traitement

### L2 – Chaîne de réception SDR

- Configuration ADALM-Pluto
- Module d'acquisition RF

### L3 – Chaîne de traitement ADS-B

- Module de démodulation
- Module de décodage Mode-S

### L4 – Interface de visualisation

- Affichage des aéronefs détectés
- Visualisation des informations essentielles

### L5 – Rapport d'évaluation

- Mesures de performances radio
- Analyse des limites
- Recommandations d'amélioration

### L6 – Documentation complète

- Guide d'installation
- Guide utilisateur
- Documentation technique
- Procédure de reproduction du prototype

---

## Jalons

```text
+------+------------------------------------------+----------------+
| ID   | Description                              | Échéance       |
+------+------------------------------------------+----------------+
| M1   | Architecture validée                     | Fin du mois 1  |
| M2   | Acquisition RF opérationnelle            | Semaine 6      |
| M3   | Démodulation et décodage fonctionnels    | Semaine 8      |
| M4   | Affichage des aéronefs opérationnel      | Semaine 10     |
| M5   | Validation des performances              | Semaine 11     |
| M6   | Prototype complet et documentation       | Fin du mois 3  |
+------+------------------------------------------+----------------+
```

---

## Risques

```text
+--------------------------------------+--------+----------------------------------------------+
| Risque                               | Impact | Plan de mitigation                           |
+--------------------------------------+--------+----------------------------------------------+
| Sensibilité RF insuffisante          | Élevé  | Optimisation des paramètres SDR              |
| Difficultés de synchronisation ADS-B | Élevé  | Tests progressifs sur signaux enregistrés    |
| Complexité du décodage Mode-S        | Moyen  | Validation unitaire du pipeline              |
| Performances insuffisantes           | Moyen  | Profilage et optimisation continue           |
| Documentation incomplète             | Moyen  | Documentation à chaque jalon                 |
| Dépassement du délai de 3 mois       | Élevé  | Priorisation des fonctionnalités critiques   |
+--------------------------------------+--------+----------------------------------------------+
```

---

## Critères de succès

Le projet sera considéré comme réussi lorsque :

- Les trames ADS-B à 1090 MHz sont correctement reçues.
- Les messages Mode-S sont décodés avec succès.
- Les aéronefs détectés sont affichés de manière exploitable.
- Le prototype fonctionne sur la plateforme ADALM-Pluto.
- Les performances radio sont documentées et analysées.
- La documentation permet à un tiers de reproduire le système.
- L'architecture développée est réutilisable pour d'autres projets SDR.

---

## Gouvernance

```text
+----------------+------------------------------------+
| Élément        | Valeur                             |
+----------------+------------------------------------+
| Sponsor        | First Virtual Company              |
| Responsable    | CEO – First Virtual Company        |
| Domaine        | Recherche & Développement SDR      |
| Durée cible    | 3 mois                             |
| Statut initial | Projet de lancement                |
+----------------+------------------------------------+
```

---

## Validation finale

Le projet sera clôturé après :

- Validation de l'ensemble des livrables
- Démonstration du prototype en environnement réel
- Publication de la documentation complète
- Validation par le sponsor du projet
