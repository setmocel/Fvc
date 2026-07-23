# Standard documentaire

## Objectif

Définir les règles de rédaction utilisées dans tous les documents produits par First Virtual Company.

---

# Langue

La langue de travail est le français.

Les termes techniques peuvent rester en anglais lorsqu'ils sont d'usage courant.

---

# Format

Tous les documents utilisent Markdown.

Extension :

.md

Encodage :

UTF-8

---

# Structure minimale

Chaque document doit commencer par :

```markdown
# Titre

## Objectif

## Contexte

## Contenu

## Conclusion

## Références
```

Les sections inutiles peuvent être supprimées.

---

# Titres

Utiliser :

# Niveau 1

## Niveau 2

### Niveau 3

Éviter plus de quatre niveaux.

---

# Listes

Utiliser :

- listes à puces

ou

1. listes numérotées

Éviter les listes imbriquées profondes.

---

# Diagrammes

Les diagrammes simples utilisent :

```text
Composant A
      │
      ▼
Composant B
```

Lorsque nécessaire, utiliser Mermaid.

---

# Nommage des fichiers

Utiliser exclusivement :

minuscules

mots séparés par des tirets

Exemples :

project-charter.md

system-architecture.md

technical-study-001.md

---

# Architecture Decision Records

Nom :

ADR-001-titre.md

Structure :

# Contexte

# Problème

# Solutions envisagées

# Décision

# Justification

# Conséquences

---

# Études techniques

Nom :

technical-study-XXX.md

Structure :

# Objectif

# Contexte

# Solutions étudiées

# Comparaison

# Recommandation

# Références

---

# Comptes-rendus

Structure :

# Participants

# Date

# Sujet

# Décisions

# Actions

---

# Références

Les références doivent être regroupées à la fin du document.

Préciser :

- article
- norme
- dépôt GitHub
- documentation constructeur
- publication scientifique

---

# Versionnement

Les documents ne comportent pas de numéro de version.

Le suivi des versions est assuré exclusivement par Git.

---

# Règles générales

Les documents doivent être :

- concis ;
- précis ;
- factuels ;
- argumentés ;
- traçables.

Les hypothèses doivent être explicitement identifiées.

Les décisions doivent être justifiées.

Les questions ouvertes doivent être listées.

---

# Principe fondamental

Le dépôt GitHub représente la mémoire permanente de First Virtual Company.

Les conversations avec les agents IA servent à produire ou à mettre à jour les artefacts, mais ne constituent jamais la documentation officielle du projet.
