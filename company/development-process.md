# Processus de développement

## Objectif

Ce document décrit le processus de développement utilisé par First Virtual Company (FVC).

Tous les rôles de l'entreprise doivent respecter ce processus.

Le dépôt GitHub constitue la source de vérité du projet.

---

# Cycle de vie d'une fonctionnalité

Une fonctionnalité suit les étapes suivantes.

```text
Vision
   │
   ▼
Product Management
   │
   ▼
Étude technique
   │
   ▼
Architecture
   │
   ▼
Planification
   │
   ▼
Développement
   │
   ▼
Tests
   │
   ▼
Validation
   │
   ▼
Livraison
```

---

# Étape 1 — Vision

Responsable :

- CEO

Objectif :

Définir les objectifs métier.

Livrables :

- company/vision.md
- reports/project-charter.md

---

# Étape 2 — Product Management

Responsable :

- Product Manager

Objectif :

Transformer les objectifs en besoins fonctionnels.

Livrables :

- product/backlog.md
- product/roadmap.md

---

# Étape 3 — Recherche

Responsable :

- Research Engineer

Objectif :

Étudier les solutions techniques.

Livrables :

- research/state-of-the-art.md
- research/technical-study-XXX.md

---

# Étape 4 — Architecture

Responsable :

- System Architect

Objectif :

Concevoir le système.

Livrables :

- engineering/system-architecture.md
- engineering/component-diagram.md
- engineering/decisions/ADR-XXX.md

---

# Étape 5 — Planification

Responsable :

- Engineering Manager

Objectif :

Préparer le développement.

Livrables :

- engineering/implementation-plan.md
- engineering/sprint-plan.md

---

# Étape 6 — Développement

Responsable :

- Developer

Objectif :

Implémenter les fonctionnalités.

Livrables :

- software/
- documentation technique

---

# Étape 7 — Validation

Responsable :

- QA Manager

Objectif :

Garantir la conformité du produit.

Livrables :

- tests/
- reports/quality-report.md

---

# Gestion des questions ouvertes

Une question ouverte ne doit jamais rester dans une conversation ChatGPT.

Elle doit devenir un artefact.

Selon sa nature :

- métier → CEO
- fonctionnelle → Product Manager
- scientifique → Research Engineer
- architecturale → System Architect
- organisationnelle → Engineering Manager
- qualité → QA Manager

Les décisions retenues sont documentées.

---

# Gestion des décisions

Toute décision importante doit être formalisée.

Les décisions d'architecture sont enregistrées dans :

engineering/decisions/

sous la forme :

ADR-XXX-<titre>.md

---

# Règles de collaboration

Les agents :

- lisent les artefacts nécessaires avant toute mission ;
- ne modifient que les artefacts dont ils sont responsables ;
- documentent systématiquement leurs décisions ;
- utilisent GitHub comme mémoire collective.

Aucune information importante ne doit rester uniquement dans une conversation ChatGPT.
