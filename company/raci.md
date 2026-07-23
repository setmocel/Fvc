# Matrice RACI - First Virtual Company (FVC)

## Objectif

Ce document définit les responsabilités de chaque rôle dans la production et la validation des principaux artefacts du projet.

## Légende

| Lettre | Signification |
|---------|---------------|
| **R** | Responsible : réalise le travail |
| **A** | Accountable : valide et porte la responsabilité finale |
| **C** | Consulted : est consulté avant la décision |
| **I** | Informed : est informé après la décision |

---

# Rôles

| Abréviation | Rôle |
|-------------|------|
| CEO | Chief Executive Officer |
| PM | Product Manager |
| RE | Research Engineer |
| SA | System Architect |
| EM | Engineering Manager |
| DEV | Developer |
| QA | QA Manager |

---

# Gouvernance

| Activité | CEO | PM | RE | SA | EM | DEV | QA |
|-----------|:---:|:--:|:--:|:--:|:--:|:---:|:--:|
| Définition de la vision | A | C | I | I | I | I | I |
| Validation des objectifs | A | R | C | C | I | I | I |
| Validation du périmètre MVP | A | R | C | C | I | I | I |

---

# Recherche

| Activité | CEO | PM | RE | SA | EM | DEV | QA |
|-----------|:---:|:--:|:--:|:--:|:--:|:---:|:--:|
| Veille technologique | I | C | R/A | C | I | I | I |
| Études comparatives | I | C | R/A | C | I | I | I |
| Analyse des risques techniques | I | C | R | A | C | I | I |

---

# Produit

| Activité | CEO | PM | RE | SA | EM | DEV | QA |
|-----------|:---:|:--:|:--:|:--:|:--:|:---:|:--:|
| Roadmap | A | R | C | C | I | I | I |
| Backlog | I | R/A | C | C | C | I | C |
| User Stories | I | R/A | C | C | C | I | C |

---

# Architecture

| Activité | CEO | PM | RE | SA | EM | DEV | QA |
|-----------|:---:|:--:|:--:|:--:|:--:|:---:|:--:|
| Architecture système | I | C | C | R/A | C | I | I |
| Choix technologiques | I | C | C | R/A | C | I | I |
| Architecture logicielle | I | C | C | R | A | C | I |
| Architecture matérielle | I | C | C | R/A | C | I | I |
| ADR (Architecture Decision Record) | I | C | C | R/A | C | I | I |

---

# Développement

| Activité | CEO | PM | RE | SA | EM | DEV | QA |
|-----------|:---:|:--:|:--:|:--:|:--:|:---:|:--:|
| Planification des sprints | I | C | I | C | R/A | I | I |
| Implémentation | I | I | I | C | A | R | I |
| Documentation du code | I | I | I | C | A | R | I |
| Tests unitaires | I | I | I | I | C | R | A |

---

# Validation

| Activité | CEO | PM | RE | SA | EM | DEV | QA |
|-----------|:---:|:--:|:--:|:--:|:--:|:---:|:--:|
| Plan de tests | I | C | I | C | C | I | R/A |
| Validation fonctionnelle | I | C | I | I | C | I | R/A |
| Validation technique | I | I | C | C | C | I | R/A |
| Rapport qualité | I | I | I | I | C | I | R/A |

---

# Livraison

| Activité | CEO | PM | RE | SA | EM | DEV | QA |
|-----------|:---:|:--:|:--:|:--:|:--:|:---:|:--:|
| Validation du MVP | A | R | C | C | C | I | C |
| Décision de livraison | A | C | I | C | C | I | C |

---

# Artefacts de référence

| Artefact | Responsable principal |
|-----------|-----------------------|
| `company/vision.md` | CEO |
| `company/org-chart.md` | CEO |
| `company/raci.md` | CEO |
| `research/project-definition.md` | Research Engineer |
| `research/state-of-the-art.md` | Research Engineer |
| `product/backlog.md` | Product Manager |
| `product/roadmap.md` | Product Manager |
| `engineering/system-architecture.md` | System Architect |
| `engineering/implementation-plan.md` | Engineering Manager |
| `engineering/decisions/ADR-*.md` | System Architect |
| `software/` | Developer |
| `tests/` | QA Manager |
| `reports/project-charter.md` | CEO |
| `reports/quality-report.md` | QA Manager |

---

# Principe de fonctionnement

Les agents collaborent exclusivement au travers des artefacts du dépôt GitHub.

Avant de commencer une mission, chaque agent doit :

1. consulter les documents dont il est **Consulted (C)** ou **Informed (I)** ;
2. mettre à jour les artefacts dont il est **Responsible (R)** ;
3. solliciter une validation lorsque le RACI désigne un autre rôle comme **Accountable (A)**.

Le dépôt GitHub constitue la source de vérité de First Virtual Company.
