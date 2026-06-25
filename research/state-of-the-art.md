# État de l’art – Récepteurs ADS-B Open Source pour ADALM-Pluto SDR

## Contexte

Le projet ADS-B SDR de First Virtual Company vise à développer un prototype capable de recevoir, décoder et visualiser des trames ADS-B à 1090 MHz à partir d’un SDR ADALM-Pluto.

L’objectif n’est pas uniquement de démontrer la réception ADS-B, mais également de construire une architecture logicielle réutilisable, documentée et extensible à d’autres projets SDR.

Dans ce contexte, l’état de l’art se concentre sur les solutions open source permettant :

- l’acquisition RF ;
- la démodulation ADS-B ;
- le décodage Mode-S ;
- la distribution des données ;
- la visualisation des aéronefs ;
- l’intégration potentielle avec ADALM-Pluto.

---

# Architecture générale d’un récepteur ADS-B

La plupart des solutions existantes suivent l’architecture suivante :

```text
SDR
 ↓
Acquisition IQ
 ↓
Détection ADS-B
 ↓
Démodulation PPM
 ↓
Décodage Mode-S
 ↓
Tracking aéronefs
 ↓
Sorties réseau
 ↓
Visualisation / Agrégation
```

Les différences entre projets concernent principalement :

- les performances DSP ;
- la qualité du décodage ;
- les interfaces réseau ;
- la compatibilité SDR ;
- la maintenabilité du code.

---

# Dump1090

## Présentation

Dump1090 est le projet historique de décodage ADS-B.

Il a été initialement développé par Salvatore Sanfilippo (antirez) puis repris par plusieurs forks majeurs :

- dump1090 original
- dump1090-mutability
- dump1090-fa (FlightAware)

Pendant plusieurs années, il a constitué la référence de l’écosystème ADS-B amateur.

## Architecture

```text
RTL-SDR
 ↓
dump1090
 ↓
Beast / SBS / Raw
 ↓
Carte Web
```

## Avantages

- Très mature
- Documentation abondante
- Écosystème important
- Consommation CPU faible

## Limites

- Architecture ancienne
- Optimisations DSP limitées
- Principalement conçu pour RTL-SDR
- Peu d’évolution récente

## Compatibilité ADALM-Pluto

Compatibilité indirecte.

Une intégration nécessite :

```text
ADALM-Pluto
 ↓
libiio / SoapySDR
 ↓
Adaptation IQ
 ↓
dump1090
```

La modification du code source est généralement nécessaire.

## Évaluation

| Critère | Note |
|----------|--------|
| Performance ADS-B | 3/5 |
| Maintenabilité | 3/5 |
| Compatibilité Pluto | 2/5 |
| Réutilisabilité | 3/5 |

---

# Readsb

## Présentation

Readsb est un fork avancé de dump1090.

Initialement développé par Mictronics puis poursuivi activement par Wiedehopf, il est aujourd’hui considéré comme la référence technique dans de nombreux réseaux ADS-B.

## Fonctionnalités

- Décodage Mode-S amélioré
- CRC optimisé
- Tracking plus robuste
- Support multithread
- Export réseau étendu
- Compatibilité tar1090

## Architecture

```text
SDR
 ↓
readsb
 ↓
Tracking
 ↓
Beast / SBS / JSON
 ↓
Visualisation
```

## Avantages

- Meilleures performances de décodage
- Développement actif
- Architecture moderne
- Intégration facile avec les outils actuels

## Limites

- Plus complexe que dump1090
- Toujours fortement orienté RTL-SDR

## Compatibilité ADALM-Pluto

Très prometteuse.

L’architecture permet relativement facilement de remplacer la couche RTL-SDR par :

- libiio
- SoapySDR
- source IQ personnalisée

Architecture cible :

```text
ADALM-Pluto
 ↓
libiio
 ↓
readsb
 ↓
tar1090
 ↓
Feeders
```

## Évaluation

| Critère | Note |
|----------|--------|
| Performance ADS-B | 5/5 |
| Maintenabilité | 5/5 |
| Compatibilité Pluto | 4/5 |
| Réutilisabilité | 5/5 |

---

# Tar1090

## Présentation

Tar1090 n’est pas un décodeur ADS-B.

Il fournit une interface Web moderne pour l’exploitation des données produites par readsb ou dump1090.

## Fonctionnalités

- Cartographie temps réel
- Historique des positions
- Affichage détaillé des aéronefs
- Statistiques de réception

## Intérêt pour le projet

Tar1090 répond directement au livrable de visualisation prévu dans le projet.

Il permet d’obtenir rapidement une démonstration fonctionnelle sans développer une interface spécifique.

## Compatibilité Pluto

Indirecte.

Compatible dès lors que readsb ou dump1090 produisent les flux attendus.

---

# ADSBExchange

## Présentation

ADSBExchange est principalement un réseau mondial d’agrégation ADS-B.

Le projet fournit :

- infrastructure de collecte ;
- clients de transmission ;
- services MLAT ;
- APIs.

## Rôle dans l’écosystème

```text
readsb
 ↓
Feed client
 ↓
ADSBExchange
```

## Intérêt pour le projet

Faible pour la phase de recherche fondamentale.

Intérêt élevé pour :

- la validation terrain ;
- la comparaison des performances ;
- les tests d’intégration.

## Compatibilité Pluto

Indirecte via readsb.

---

# FlightAware (piaware + dump1090-fa)

## Présentation

FlightAware maintient l’un des forks les plus utilisés de dump1090.

L’écosystème comprend :

- dump1090-fa
- piaware
- outils statistiques

## Avantages

- Très stable
- Large communauté
- Documentation importante

## Limites

- Architecture centrée sur l’écosystème FlightAware
- Peu adaptée comme base de développement expérimental

## Compatibilité Pluto

Moyenne.

L’intégration nécessiterait les mêmes adaptations que dump1090.

---

# GNU Radio

## Présentation

GNU Radio est le framework SDR open source de référence.

Contrairement à dump1090 ou readsb, GNU Radio ne fournit pas directement un décodeur ADS-B complet mais permet de construire l’ensemble de la chaîne de traitement.

## Architecture

```text
ADALM-Pluto
 ↓
GNU Radio
 ↓
Détection ADS-B
 ↓
Démodulation
 ↓
Décodage
```

## Avantages

- Contrôle complet de la chaîne DSP
- Compatible nativement avec PlutoSDR
- Excellent outil de recherche

## Limites

- Développement plus long
- Maintenance plus complexe
- Risque projet plus élevé

## Intérêt pour FVC

Très élevé pour :

- l’analyse DSP ;
- la validation algorithmique ;
- l’étude des performances radio.

Moins pertinent comme base du prototype opérationnel.

---

# gr-adsb

## Présentation

gr-adsb est un module GNU Radio dédié à ADS-B.

Il implémente :

- détection ADS-B ;
- démodulation PPM ;
- décodage de trames.

## Avantages

- Compatible avec l’écosystème GNU Radio
- Bon support pour l’expérimentation

## Limites

- Moins maintenu que readsb
- Moins utilisé en production

## Intérêt pour FVC

Peut servir de référence algorithmique pour comparer les performances du pipeline readsb.

---

# ModesDeco2

## Présentation

ModesDeco2 est souvent considéré comme l’un des meilleurs décodeurs ADS-B disponibles.

## Limitation

Logiciel propriétaire.

## Intérêt

Ne peut pas servir de base logicielle.

Peut toutefois être utilisé comme référence de performances lors des campagnes d’évaluation radio.

---

# Comparaison synthétique

| Solution | Open Source | Décodeur ADS-B | Visualisation | Compatibilité Pluto | Pertinence FVC |
|-----------|-------------|----------------|---------------|--------------------|----------------|
| dump1090 | Oui | Oui | Basique | Moyenne | Moyenne |
| readsb | Oui | Oui | Via tar1090 | Très bonne | Excellente |
| tar1090 | Oui | Non | Oui | Indirecte | Élevée |
| ADSBExchange | Partielle | Non | Non | Indirecte | Moyenne |
| FlightAware | Oui | Oui | Oui | Moyenne | Moyenne |
| GNU Radio | Oui | Oui (à construire) | Non | Excellente | Élevée |
| gr-adsb | Oui | Oui | Non | Excellente | Bonne |
| ModesDeco2 | Non | Oui | Oui | N/A | Référence uniquement |

---

# Recommandation pour le projet FVC

Au regard des objectifs du projet :

- prototype opérationnel en trois mois ;
- architecture réutilisable ;
- coût matériel réduit ;
- ADALM-Pluto comme plateforme SDR ;
- évaluation des performances radio ;

la stratégie la plus pertinente est :

## Solution cible

```text
ADALM-Pluto
 ↓
libiio
 ↓
Couche d’abstraction SDR
 ↓
readsb (adapté Pluto)
 ↓
tar1090
 ↓
Visualisation
```

## Solution de référence

```text
GNU Radio + gr-adsb
```

utilisée comme environnement d’expérimentation et de validation des traitements DSP.

## Justification

Cette approche :

- minimise le risque de développement ;
- maximise la réutilisation de composants éprouvés ;
- respecte les contraintes de calendrier ;
- conserve la possibilité d’étudier les performances radio en profondeur ;
- fournit une architecture réutilisable pour d’autres projets SDR.

## Conclusion

Readsb apparaît comme la meilleure base logicielle pour le prototype ADS-B ADALM-Pluto.

GNU Radio et gr-adsb constituent des outils complémentaires pertinents pour la recherche et l’évaluation algorithmique.

Dump1090 reste une référence historique utile pour la compréhension du domaine mais ne représente plus l’option la plus avantageuse pour une nouvelle architecture SDR orientée recherche et développement.
