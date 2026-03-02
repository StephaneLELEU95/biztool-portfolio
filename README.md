# BizTool - Portfolio Case Study

Ce depot public presente le projet sous forme d'etude technique.
Le code source complet est volontairement prive.

## 1) Contexte et objectif produit

BizTool cible la gestion de facturation pour independants et petites structures:
- gestion clients et produits
- cycle devis -> facture
- suivi paiements et statuts

Objectif: fournir une API metier robuste, lisible, testable, et prete a evoluer vers un usage SaaS.

## 2) Architecture (vue engineering)

Architecture en couches:
- `api/`: routes HTTP et contrats d'entree/sortie
- `services/`: logique metier (regles devis/factures/paiements)
- `repositories/`: acces donnees SQLAlchemy
- `models/` + `schemas/`: modelisation DB + validation Pydantic
- `core/`: configuration, DB, securite JWT

Flux metier type:
1. Authentification admin JWT
2. Creation client/produit
3. Creation devis et calculs montants
4. Envoi/validation devis
5. Conversion devis en facture
6. Paiements partiels/complets et transitions d'etat

## 3) Securite implementee

- Auth JWT obligatoire sur routes metier
- `/health` conserve public pour supervision
- Swagger/OpenAPI aligne avec scheme Bearer
- Hygiene secrets (`.env` exclu, `.env.example` safe)
- DB locale (`*.db`) exclue du versioning

## 4) Decisions d'engineering et trade-offs

- SQLAlchemy 2 + couche repository: facilite testabilite et evolution DB
- Alembic: migrations deterministes pour livraisons propres
- Validation Pydantic v2: contrats API stricts
- Separation claire des responsabilites: baisse du couplage

## 5) Qualite logicielle

- Tests Pytest sur workflows critiques (devis, factures, paiements, auth)
- Verification explicite des routes protegees (401 sans token)
- Historique Git structure (import initial, hardening securite, docs)
- Base prete pour CI/CD standard

## 6) Exemples de scenarios couverts

- Creation devis en brouillon, envoi puis verrouillage
- Duplication devis et conversion en facture
- Paiements successifs et passage `partial` -> `paid`
- Refus d'acces sans bearer token sur routes metier

## 7) Travail realise (responsabilites)

- Design et implementation de l'API billing
- Modelisation metier clients/produits/devis/factures/paiements
- Enforcement global de l'auth JWT sur routes metier
- Ecriture/adaptation tests autour des exigences securite
- Hygiene repo et documentation orientee recrutement

## 8) Roadmap technique

- SMTP (envoi devis/factures + relances)
- logs structures JSON + tracing
- durcissement prod (rate limiting, profils env plus stricts)
- extension multi-tenant

## Stack

FastAPI, SQLAlchemy 2, Alembic, Pydantic v2, JWT (python-jose), Pytest.

## Acces code complet

Le code integral est conserve en prive.
Acces possible pour evaluation recruteur/ecole sur demande via le profil GitHub.
