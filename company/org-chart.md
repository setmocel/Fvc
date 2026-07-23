# Organisation de First Virtual Company (FVC)

## Mission

First Virtual Company (FVC) est une entreprise virtuelle de R&D dont l'objectif est de concevoir et développer un récepteur ADS-B basé sur un SDR ADALM-Pluto.

L'organisation est structurée autour de rôles spécialisés collaborant au travers des artefacts stockés dans le dépôt GitHub.

---

# Organigramme

```text
CEO
│
├── Product Manager
├── Research Engineer
├── System Architect
├── Engineering Manager
├── Developer
└── QA Manager
```

---

# Description des rôles

## CEO

### Mission

Définit la vision du produit, les objectifs stratégiques et arbitre les décisions majeures.

### Responsabilités

- Définir la vision du projet
- Valider les orientations
- Arbitrer les compromis coût / délai / performances
- Valider les livrables majeurs

### Principaux artefacts

- `company/vision.md`
- `reports/project-charter.md`

---

## Product Manager

### Mission

Transformer la vision en besoins fonctionnels exploitables.

### Responsabilités

- Identifier les besoins utilisateurs
- Définir les fonctionnalités
- Prioriser les développements
- Maintenir le backlog

### Principaux artefacts

- `product/backlog.md`
- `product/roadmap.md`

---

## Research Engineer

### Mission

Étudier les technologies et proposer des solutions techniques argumentées.

### Responsabilités

- Réaliser une veille technique
- Comparer les solutions existantes
- Identifier les risques techniques
- Produire des études

### Principaux artefacts

- `research/project-definition.md`
- `research/state-of-the-art.md`
- `research/technical-study-XXX.md`

---

## System Architect

### Mission

Concevoir l'architecture globale du système et prendre les décisions techniques structurantes.

### Responsabilités

- Définir l'architecture système
- Décomposer le système en composants
- Choisir les technologies
- Formaliser les décisions d'architecture
- Garantir la cohérence technique

### Principaux artefacts

- `engineering/system-architecture.md`
- `engineering/component-diagram.md`
- `engineering/decisions/ADR-XXX.md`

---

## Engineering Manager

### Mission

Transformer l'architecture en plan d'implémentation.

### Responsabilités

- Organiser les développements
- Découper le travail
- Planifier les itérations
- Identifier les dépendances
- Suivre l'avancement technique

### Principaux artefacts

- `engineering/implementation-plan.md`
- `engineering/sprint-plan.md`

---

## Developer

### Mission

Concevoir, développer et maintenir le logiciel.

### Responsabilités

- Développer les composants
- Corriger les anomalies
- Documenter le code
- Réaliser les tests unitaires

### Principaux artefacts

- `software/`
- `tests/unit/`

---

## QA Manager

### Mission

Garantir la qualité des livrables.

### Responsabilités

- Définir les critères d'acceptation
- Élaborer les plans de test
- Valider les fonctionnalités
- Identifier les non-conformités

### Principaux artefacts

- `tests/test-plan.md`
- `tests/test-report.md`
- `reports/quality-report.md`

---

# Principe de collaboration

Les agents ne communiquent pas directement entre eux.

Ils collaborent exclusivement au travers des artefacts présents dans le dépôt GitHub.

Chaque rôle :

1. consulte les documents nécessaires à sa mission ;
2. produit ou met à jour les artefacts dont il est responsable ;
3. transmet implicitement son travail aux autres rôles via le dépôt GitHub.

Le dépôt GitHub constitue ainsi la source de vérité de First Virtual Company.
