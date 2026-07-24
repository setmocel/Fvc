# Architecture système v1 — Récepteur ADS-B SDR FVC

## Objectif

Définir une première architecture système cohérente pour le projet ADS-B SDR de First Virtual Company, en tenant compte des besoins métier, des contraintes de coût et de réutilisabilité, et du cadre documentaire du projet. Cette version sert de base de travail pour le Developer, le QA Manager et les futurs ADR. fileciteturn0file0L5-L15 fileciteturn5file0L14-L25

## Contexte

Le projet vise la conception d’un récepteur ADS-B basé sur un SDR ADALM-Pluto, capable de recevoir des trames à 1090 MHz, de décoder des messages Mode-S et d’afficher les aéronefs détectés. L’entreprise demande aussi une architecture réutilisable, avec une documentation complète, et un prototype fonctionnel sous trois mois. fileciteturn0file0L11-L19 fileciteturn5file0L5-L25

Le cadre d’exécution est fortement documenté : la vision, le backlog, la recherche, l’architecture, l’implémentation et la validation sont séparées en artefacts GitHub, et le dépôt est la source de vérité. Le System Architect est responsable de l’architecture système, des composants et des ADR. Le Developer et le QA Manager prendront ensuite le relais pour l’implémentation et la validation. fileciteturn1file0L91-L109 fileciteturn2file0L64-L72 fileciteturn3file0L100-L115

## Architecture globale

L’architecture recommandée est une chaîne de traitement de signal en flux continu, séparée en quatre couches :

1. **Acquisition radio** : le ADALM-Pluto capte le signal 1090 MHz et fournit des échantillons I/Q.
2. **Traitement baseband** : le logiciel applique les étapes de filtrage, détection d’impulsions, synchronisation et démodulation ADS-B/Mode-S.
3. **Décodage et enrichissement** : les trames validées sont décodées, horodatées, normalisées et éventuellement enrichies par calculs dérivés.
4. **Présentation et exploitation** : les aéronefs détectés sont affichés dans une interface utilisateur et exposés à d’autres usages via des sorties de données structurées.

Cette architecture privilégie une séparation nette entre traitement radio, logique de décodage et présentation afin de faciliter la réutilisation et les évolutions futures. fileciteturn5file0L14-L25

En première intention, je recommande une **application monolithique modulaire** plutôt qu’une architecture distribuée. Pour un prototype à trois mois, cela réduit la complexité d’intégration, simplifie les tests et limite les risques d’interface. Une architecture plus distribuée pourra être envisagée plus tard si le besoin de partage multi-consommateurs, de scalabilité ou de séparation forte des responsabilités devient déterminant.

## Composants

### 1. Sous-système matériel RF
Rôle : capter le signal ADS-B à 1090 MHz et le convertir en échantillons numériques.

Composants probables :
- ADALM-Pluto SDR
- Antenne 1090 MHz
- Liaison USB ou équivalent vers l’hôte de calcul

Point d’attention : la qualité de réception dépendra fortement de l’antenne, du placement et du niveau de bruit radio. Ce point devra être étudié plus précisément par le Research Engineer ou confirmé expérimentalement.

### 2. Driver / couche d’accès SDR
Rôle : piloter le récepteur, régler fréquence, gain, taux d’échantillonnage, récupération des buffers I/Q.

Responsabilités :
- initialisation du matériel
- configuration de capture
- lecture des flux d’échantillons
- gestion des erreurs matérielles

Alternative possible : utiliser une librairie de bas niveau ou une couche d’abstraction plus haute selon l’écosystème retenu. Recommandation : choisir l’option qui maximise la simplicité d’intégration avec le prototype tout en gardant une interface isolée.

### 3. Pipeline DSP ADS-B
Rôle : transformer les échantillons RF en trames ADS-B exploitables.

Sous-fonctions :
- prétraitement du signal
- filtrage et détection de préambule
- extraction des bits
- synchronisation temporelle
- vérification d’intégrité
- gestion des paquets valides / invalides

Ce composant est critique pour la performance globale et doit rester découplé des couches d’IHM.

### 4. Décoder Mode-S / ADS-B
Rôle : interpréter la charge utile des trames.

Sous-fonctions :
- identification du type de message
- extraction des champs utiles
- calcul des valeurs dérivées si nécessaire
- normalisation du format de sortie

Point d’attention : la couverture exacte des messages Mode-S à prendre en charge n’est pas encore figée et devra être précisée dans le backlog et/ou une étude technique dédiée.

### 5. Gestionnaire de pistes aéronefs
Rôle : maintenir l’état courant des aéronefs détectés.

Fonctions :
- création / mise à jour / expiration des pistes
- fusion des messages d’un même aéronef
- stockage de l’état courant en mémoire
- préparation des données pour l’affichage

Ce composant sert de pivot entre messages bruts et vue opérationnelle.

### 6. Interface de présentation
Rôle : afficher les aéronefs détectés à l’utilisateur.

Options possibles :
- interface CLI / terminal pour prototype minimal
- interface graphique légère
- export de données structurées pour intégration future

Recommandation : démarrer par une interface simple et robuste, par exemple console enrichie ou vue tabulaire, afin de sécuriser le prototype. Une carte ou une visualisation avancée pourra être ajoutée ensuite.

### 7. Journalisation et observabilité
Rôle : tracer les événements utiles au debug, au diagnostic radio et à la validation.

Fonctions :
- logs techniques
- statistiques de réception
- compteurs de messages reçus / décodés / rejetés
- indicateurs de qualité du flux

Ce composant est indispensable pour le QA et pour l’étude des performances radio.

### 8. Stockage ou export de données
Rôle : conserver ou exposer les données mesurées.

Options possibles :
- fichier local
- export JSON / CSV
- flux local pour consommation externe

Cette brique n’est pas nécessairement prioritaire dans le MVP, mais elle est utile pour la réutilisabilité et les analyses ultérieures.

## Flux de données

### Flux principal
```text
Antenne 1090 MHz
      │
      ▼
ADALM-Pluto SDR
      │  échantillons I/Q
      ▼
Couche d’accès SDR
      │
      ▼
Pipeline DSP ADS-B
      │  trames candidates
      ▼
Décodage Mode-S / ADS-B
      │  messages normalisés
      ▼
Gestionnaire de pistes
      │  état courant aéronefs
      ├──────────────► Journalisation / métriques
      └──────────────► Interface de présentation
```

### Flux secondaires
- **Flux de configuration** : paramètres de fréquence, gain, seuils, mode d’exécution.
- **Flux de diagnostic** : erreurs matérielles, paquets invalids, statistiques de réception.
- **Flux d’export** : écritures de données vers fichier ou sortie structurée.

Le flux principal doit rester continu et non bloquant. Les flux secondaires ne doivent pas perturber le traitement temps réel.

## Interfaces

### Interface matériel ↔ logiciel
Type : API du SDK / driver SDR.

Données échangées :
- fréquence centrale
- gain
- sample rate
- buffers I/Q
- erreurs de capture

### Interface entre acquisition et DSP
Type : flux mémoire ou file de buffers internes.

Exigences :
- faible latence
- pas de copies inutiles
- gestion du backpressure
- tolérance aux buffers incomplets

### Interface entre DSP et décodage
Type : structure de trame candidate.

Données :
- bits bruts ou symboles reconnus
- timestamp
- qualité de détection
- statut de validation

### Interface entre décodage et gestionnaire de pistes
Type : événement métier / message normalisé.

Données :
- identifiant aéronef
- type de message
- position si disponible
- altitude, vitesse, cap si disponibles
- horodatage
- confiance / validité

### Interface vers IHM / export
Type : modèle de vue ou format sérialisé.

Recommandation :
- un format interne structuré pour la logique applicative
- un format d’échange stable, par exemple JSON, pour l’export et les intégrations futures

## Hypothèses

1. Le prototype cible un environnement unique d’exécution, probablement sur un poste de développement ou un mini-PC relié au ADALM-Pluto.
2. La réception visée est centrée sur la bande 1090 MHz ADS-B, sans support initial d’autres protocoles.
3. Le besoin principal du MVP est la chaîne acquisition → décodage → affichage, pas une plateforme multi-utilisateurs.
4. Le système peut fonctionner localement, sans dépendance à un backend distant.
5. La réutilisabilité demandée doit d’abord être obtenue par modularité logicielle, pas par distribution des services.
6. Les performances attendues restent compatibles avec un traitement logiciel classique, mais cela devra être confirmé par étude et mesure.
7. La solution doit rester faible coût, ce qui exclut a priori les architectures matérielles ou logicielles inutilement complexes. fileciteturn5file0L21-L25

## Décisions d’architecture à prendre

Les sujets suivants doivent être formalisés en ADR dans `engineering/decisions/` :

1. **Choix du style d’architecture applicative**
   - monolithe modulaire
   - architecture en pipeline avec modules faiblement couplés
   - éventuelle séparation future en services
   - Recommandation : monolithe modulaire pour le MVP.

2. **Pile logicielle d’acquisition SDR**
   - librairie / SDK à utiliser
   - mode de configuration du Pluto
   - gestion des buffers et du débit

3. **Modèle de traitement du signal**
   - traitement en temps réel ou par lots glissants
   - stratégie de détection du préambule
   - seuils et paramètres de démodulation

4. **Couverture fonctionnelle Mode-S / ADS-B**
   - familles de messages prises en charge au MVP
   - gestion des messages partiels ou non valides

5. **Modèle de données aéronef**
   - schéma interne des pistes
   - durée de vie d’une piste
   - règles de fusion des messages

6. **Interface utilisateur du prototype**
   - CLI simple, TUI, GUI légère, ou combinaison
   - niveau de détail affiché

7. **Format d’export et journalisation**
   - JSON, CSV, fichier local, ou flux interne
   - niveau d’observabilité à conserver

8. **Stratégie de packaging et d’exécution**
   - exécution native, conteneur, ou scripté
   - dépendances système minimales

9. **Critères de performance cible**
   - taux de détection
   - latence acceptable
   - charge CPU maximale
   - stabilité en fonctionnement prolongé

## Questions ouvertes

- Quel sous-ensemble exact de messages ADS-B / Mode-S doit être traité dans le prototype ?
- Faut-il inclure la position géographique des aéronefs dès la V1, ou seulement l’identification et les attributs de vol ?
- Quelle interface de présentation correspond le mieux au MVP : terminal, web local, ou interface graphique ?
- Quel niveau de précision / robustesse est attendu dans les mesures de performance radio ?
- Quels critères de qualité doivent servir à la validation du QA Manager ?
- Le traitement doit-il être strictement temps réel ou simplement suffisamment rapide pour l’affichage local ?
- Faut-il prévoir dès maintenant un export de données vers des outils d’analyse ?
- Quel niveau de réutilisabilité est attendu : réutilisation de code, de pipeline DSP, ou de composants d’IHM ?
- L’architecture doit-elle viser une future exécution sur d’autres SDR que le Pluto ?

## Prochaines étapes

1. Confirmer, avec le Product Manager, le périmètre fonctionnel exact du MVP.
2. Lancer ou compléter une étude technique sur la chaîne SDR/DSP et les options de librairie.
3. Rédiger les ADR pour les choix structurants listés ci-dessus.
4. Produire le diagramme de composants dans `engineering/component-diagram.md`.
5. Transmettre au Engineering Manager les interfaces stables pour la planification.
6. Laisser au Developer la précision des contrats de modules, des formats de messages et de la structure de code.
7. Laisser au QA Manager la définition des critères d’acceptation, des scénarios de test et des seuils de performance.

## Références

- `company/vision.md`
- `company/org-chart.md`
- `company/raci.md`
- `company/development-process.md`
- `company/documentation-standard.md`
- `research/project-definition.md`
