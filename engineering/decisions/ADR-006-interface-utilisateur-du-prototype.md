# Contexte

Le projet doit afficher les aéronefs détectés. L’interface utilisateur n’est pas encore fixée.

# Problème

Il faut choisir une interface de présentation qui :
- soit rapide à mettre en œuvre ;
- facilite la validation ;
- ne surcharge pas le prototype ;
- permette une future évolution.

# Solutions envisagées

1. **Interface terminal / CLI**
   - la plus simple ;
   - rapide pour le debug et la validation.

2. **Interface graphique légère**
   - meilleure lisibilité ;
   - plus coûteuse à développer.

3. **Export de données uniquement**
   - utile pour l’intégration ;
   - insuffisant seul pour le MVP si l’affichage direct est requis.

# Décision

La recommandation actuelle est de démarrer par une **interface terminal / CLI**, éventuellement enrichie de vues textuelles structurées.

# Justification

- faible coût ;
- rapide à valider ;
- adaptée au prototype ;
- compatible avec une extension ultérieure.

# Conséquences

- l’UI avancée peut être différée ;
- les données devront être présentées via un modèle stable ;
- les exigences d’ergonomie devront rester simples et mesurables.
