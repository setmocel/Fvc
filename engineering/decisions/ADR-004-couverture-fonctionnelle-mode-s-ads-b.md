# Contexte

Le projet doit recevoir des trames ADS-B à 1090 MHz, décoder des messages Mode-S et afficher les aéronefs détectés. Le détail exact du sous-ensemble de messages à supporter n’est pas encore figé.

# Problème

Il faut décider quelles familles de messages seront prises en charge dans le prototype, et comment gérer les messages partiels ou non valides.

# Solutions envisagées

1. **Support minimal**
   - identification de l’aéronef ;
   - messages essentiels à l’affichage.

2. **Support élargi**
   - ajout des attributs de vol utiles ;
   - gestion plus riche des états piste.

3. **Support progressif**
   - noyau minimal au MVP ;
   - extension par incréments documentés.

# Décision

Le prototype doit démarrer avec un **support minimal extensible**, avec extension progressive documentée.

# Justification

- réduit le risque de retard ;
- permet de valider la chaîne complète rapidement ;
- facilite la priorisation avec le Product Manager ;
- garde la porte ouverte à une couverture plus riche.

# Conséquences

- le backlog devra préciser le périmètre MVP ;
- les règles de rejet / tolérance des messages devront être explicites ;
- la validation QA devra couvrir les limites du support retenu.
