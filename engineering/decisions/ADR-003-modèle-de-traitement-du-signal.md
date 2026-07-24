# Contexte

Le système doit transformer un flux d’échantillons I/Q en messages ADS-B exploitables. Le comportement attendu dépend fortement de la détection du préambule, de la synchronisation et du décodage des bits.

# Problème

Il faut définir le modèle de traitement du signal :
- traitement temps réel ou par lots ;
- niveau de buffering ;
- détection du préambule ;
- paramètres de démodulation ;
- stratégie de validation des trames.

# Solutions envisagées

1. **Traitement temps réel strict**
   - pipeline continu avec faible latence ;
   - exige davantage de rigueur sur le débit et les buffers.

2. **Traitement par blocs glissants**
   - buffers de taille contrôlée, analysés avec recouvrement ;
   - plus simple à stabiliser pour un prototype.

3. **Traitement hybride**
   - acquisition continue, analyse par fenêtres glissantes ;
   - compromis entre latence et robustesse.

# Décision

L’option à privilégier pour le prototype est un **traitement hybride fondé sur des fenêtres glissantes**.

# Justification

- équilibre entre simplicité et robustesse ;
- compatible avec un prototype local ;
- facilite le debug ;
- limite les risques de perte de synchronisation.

# Conséquences

- le dimensionnement des fenêtres devra être mesuré ;
- les seuils de détection devront être ajustés expérimentalement ;
- la latence restera un paramètre à valider par test.
