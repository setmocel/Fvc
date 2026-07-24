# Contexte

Le système doit afficher des aéronefs détectés et maintenir un état courant par piste.

# Problème

Il faut définir le modèle interne de données pour :
- identifier un aéronef ;
- agréger les messages ;
- représenter l’état courant ;
- gérer l’expiration d’une piste.

# Solutions envisagées

1. **Modèle minimal de piste**
   - identifiant, dernier message, horodatage, attributs essentiels.

2. **Modèle enrichi**
   - position, vitesse, cap, altitude, historique court, qualité de réception.

3. **Modèle extensible**
   - noyau minimal avec champs facultatifs et évolution progressive.

# Décision

Le modèle de données doit être conçu comme un **modèle extensible à noyau minimal**.

# Justification

- compatible avec le MVP ;
- évite de bloquer sur des attributs non confirmés ;
- simplifie l’évolution ;
- facilite le travail du Developer et du QA Manager.

# Conséquences

- le schéma devra être stable et documenté ;
- les champs facultatifs devront être clairement définis ;
- la politique d’expiration / mise à jour d’une piste devra être spécifiée.
