# Documentation Maintenance

Ce dossier contiendra la documentation technique destinee a un developpeur qui veut comprendre, auditer ou faire evoluer le produit.

## Objectifs
- decrire l'architecture reelle du programme
- documenter le pipeline de production et la persistance
- expliciter les invariants metier a ne pas casser
- faciliter les audits et evolutions futures

## Fichiers prevus
- `architecture.md`
- `pipeline-production.md`
- `profils-et-invariants.md`
- `persistance-et-config.md`
- `logs-et-rapports.md`
- `sortie-web-et-wordpress.md`
- `tests-et-validation.md`
- `points-sensibles.md`
- `documentation-sync.md`

## Fichiers disponibles
- `architecture.md` : vue d'ensemble du decoupage actuel, des roles et des dossiers critiques
- `pipeline-production.md` : deroulement du run de production, fallback, sortie et points d'attention
- `profils-et-invariants.md` : regles canoniques a ne jamais casser sur Express, Standard, Deep et Smart
- `persistance-et-config.md` : cartographie des fichiers `config/` et principes de compatibilite
- `logs-et-rapports.md` : fonctionnement des traces, de la console GUI et des rapports Markdown
- `sortie-web-et-wordpress.md` : chaine post-production HTML, index JSON, serveur local et integration WordPress
- `tests-et-validation.md` : repertoire de tests utiles et strategie de validation ciblee
- `points-sensibles.md` : liste courte des zones a haut risque de regression
- `documentation-sync.md` : synchronisation automatique vers le depot BibLegacy-Community
- `copilot-workflow.md` : usage pratique des prompts, skills et taches VS Code ajoutes au depot
- `../../COPILOT_START_HERE.md` : point d'entree simple pour utiliser le pack Copilot du depot
- `../../DAILY_MAINTENANCE.md` : tableau de bord quotidien ultra court
- `../../COMMANDS_REFERENCE.md` : reference concise commande par commande et tache par tache
- `../../SI_TU_VEUX_X_LANCE_Y.md` : tableau compact en une page pour choisir vite

## Ordre de lecture recommande
1. `architecture.md`
2. `profils-et-invariants.md`
3. `pipeline-production.md`
4. `sortie-web-et-wordpress.md`
5. `persistance-et-config.md`
6. `logs-et-rapports.md`
7. `tests-et-validation.md`
8. `points-sensibles.md`
9. `documentation-sync.md`
10. `copilot-workflow.md`
11. `../../COPILOT_START_HERE.md`
12. `../../DAILY_MAINTENANCE.md`
13. `../../COMMANDS_REFERENCE.md`
14. `../../SI_TU_VEUX_X_LANCE_Y.md`

## Regle
Cette documentation doit etre redigee a partir du comportement verifie du code, pas a partir d'hypotheses ou d'anciennes notes.