# Contexte

Le projet a une ambition de prototype fonctionnel rapide, mais les attentes de performance ne sont pas encore formalisées.

# Problème

Il faut définir quelles dimensions de performance seront suivies pour juger la qualité du prototype :
- taux de détection ;
- latence ;
- charge CPU ;
- stabilité ;
- qualité de réception.

# Solutions envisagées

1. **Aucune cible formelle au départ**
   - trop risqué pour la validation.

2. **Cibles qualitatives**
   - plus souple ;
   - peut manquer de précision.

3. **Cibles mesurables minimales**
   - meilleure base pour QA et itérations.

# Décision

Définir des **cibles de performance mesurables minimales** avant la validation du prototype.

# Justification

- améliore l’objectivité des tests ;
- aide à arbitrer les compromis techniques ;
- facilite la validation QA ;
- empêche les décisions purement subjectives.

# Conséquences

- des seuils devront être proposés par le QA Manager avec appui technique ;
- les métriques de mesure devront être documentées ;
- certaines cibles pourront être ajustées après étude technique.
