# Contexte

Le système doit permettre le debug, l’analyse de performance radio et potentiellement l’export de données pour usages futurs.

# Problème

Il faut définir les formats et principes de journalisation / export :
- structure des logs ;
- niveau de détail ;
- format de sortie des données ;
- compatibilité future.

# Solutions envisagées

1. **Logs uniquement**
   - suffisant pour le debug ;
   - faible effort ;
   - peu réutilisable pour l’analyse.

2. **Logs + export JSON**
   - bon compromis ;
   - format lisible et réutilisable.

3. **Logs + export CSV / base locale**
   - utile pour l’analyse ;
   - peut être plus rigide ou plus coûteux.

# Décision

Privilégier une base de **journalisation structurée** et un **export simple et stable**, avec préférence initiale pour JSON lorsque des sorties structurées sont nécessaires.

# Justification

- lisible ;
- facile à consommer par d’autres outils ;
- compatible avec la réutilisabilité recherchée ;
- bon compromis pour le prototype.

# Conséquences

- les logs devront être cohérents et documentés ;
- l’export devra rester optionnel et non bloquant ;
- le QA Manager devra s’appuyer sur des traces exploitables.
