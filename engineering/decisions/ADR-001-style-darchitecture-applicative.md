# Contexte

Le projet ADS-B SDR FVC doit produire un prototype fonctionnel en trois mois, avec une architecture réutilisable, faible coût et documentée. Le système comprend acquisition RF, traitement DSP, décodage Mode-S, gestion des pistes et présentation. Le périmètre MVP n’est pas encore entièrement figé.

# Problème

Il faut choisir un style d’architecture applicative qui permette :
- un prototype rapide à intégrer ;
- une séparation claire des responsabilités ;
- une bonne testabilité ;
- une évolution possible vers davantage de modularité.

# Solutions envisagées

1. **Monolithe modulaire**
   - Tous les composants résident dans un seul exécutable ou une seule application.
   - Les modules sont séparés par des interfaces internes claires.

2. **Architecture distribuée / microservices**
   - Les composants sont séparés en services indépendants.
   - Les échanges passent par des interfaces réseau ou des bus de messages.

3. **Architecture hybride avec pipeline interne**
   - Une application principale orchestrant des modules de traitement en chaîne.
   - Éventuelle extraction ultérieure de certains modules.

# Décision

À ce stade, l’option recommandée est le **monolithe modulaire**, avec une organisation interne en pipeline de traitement.

# Justification

- meilleure simplicité d’intégration pour le MVP ;
- moins de risques d’interface et de déploiement ;
- meilleure vitesse de développement ;
- tests plus simples ;
- coût opérationnel plus faible.

# Conséquences

- les composants devront être bien découplés malgré l’exécution commune ;
- les interfaces internes devront être stables et explicites ;
- une extraction future en services restera possible si un besoin réel apparaît ;
- la réutilisabilité dépendra de la qualité du découpage interne.
