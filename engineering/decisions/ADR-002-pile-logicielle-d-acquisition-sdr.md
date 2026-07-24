# Contexte

Le système repose sur un ADALM-Pluto SDR pour capter le signal ADS-B à 1090 MHz et fournir des échantillons I/Q au traitement logiciel.

# Problème

Il faut choisir la pile logicielle qui permettra :
- de piloter le matériel SDR ;
- de récupérer les buffers I/Q ;
- de configurer fréquence, gain et sample rate ;
- de minimiser le risque technique et le temps d’intégration.

# Solutions envisagées

1. **Utiliser le SDK / librairie officielle du Pluto**
   - Accès direct aux capacités du matériel.
   - Dépendance à la maturité de l’écosystème choisi.

2. **Utiliser une couche d’abstraction SDR plus générale**
   - Possibilité de réutiliser le code avec d’autres SDR.
   - Peut ajouter de la complexité ou des limitations.

3. **Écrire une couche d’accès sur mesure**
   - Contrôle fin de l’intégration.
   - Coût de développement plus élevé et risque de maintenance.

# Décision

La pile logicielle d’acquisition doit être choisie en privilégiant **la simplicité d’intégration et l’isolation du matériel via une couche dédiée**.  
Le choix concret de la librairie / SDK reste à confirmer par étude technique avant engagement définitif.

# Justification

- le prototype est court ;
- l’intégration doit être fiable avant d’être généralisable ;
- le matériel cible principal est connu ;
- une couche d’accès isolée préserve une évolution future.

# Conséquences

- le Developer devra respecter une interface d’abstraction stable ;
- le choix définitif de librairie devra être validé avant implémentation ;
- le support d’autres SDR restera un objectif secondaire tant que non justifié.
