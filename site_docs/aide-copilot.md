# Aide Copilot

Cette page vous aide a choisir rapidement quoi lancer dans BibLegacy quand vous travaillez avec Copilot et VS Code.

## Si vous voulez juste commencer

1. ouvrez le chat Copilot
2. tapez `/BibLegacy Start Here`
3. ecrivez une phrase simple, par exemple :
   - `je veux verifier si tout marche encore`
   - `je veux tester la GUI`
   - `je veux preparer une release Windows`

## Tableau simple

| Si vous voulez... | Lancez... | Ce que ca fait |
|---|---|---|
| savoir quoi faire | `/BibLegacy Start Here` | vous dit quoi faire ensuite |
| aller a l'essentiel | `/BibLegacy Daily Maintenance` | montre le mini workflow a retenir |
| avoir une aide simple | `/BibLegacy Guided Help` | explique la prochaine action avec des mots simples |
| verifier l'interface | `/BibLegacy GUI Regression` | aide a controler les changements GUI |
| verifier la config ou les profils | `/BibLegacy Persistence Migration` | aide a controler sauvegarde, profils et compatibilite |
| verifier la production | `/BibLegacy Production Pipeline` | aide a controler le run OCR |
| verifier avant livraison | `/BibLegacy Release Readiness` | rappelle les verifications avant release |

## Taches VS Code les plus utiles

Dans `Terminal > Run Task` :

| Si vous voulez... | Lancez... | Ce que ca fait |
|---|---|---|
| ouvrir l'application | `Start BibLegacy GUI` | lance la fenetre BibLegacy |
| verifier vite les zones principales | `Quick Validation Pack` | lance plusieurs validations importantes |
| verifier l'interface | `GUI Regression Suite` | lance les tests GUI principaux |
| verifier config et profils | `Persistence Regression Suite` | lance les tests de persistance |
| verifier la documentation | `Build Public Docs` | reconstruit le site de documentation |
| voir la doc dans le navigateur | `Serve Public Docs Locally` | ouvre un site local MkDocs sur votre machine |

## Voir cette documentation dans le navigateur

1. lancez la tache `Serve Public Docs Locally`
2. ouvrez `http://127.0.0.1:8000`
3. naviguez dans les pages du site

## Si vous voulez rester tres simple

- pour savoir quoi faire : `/BibLegacy Start Here`
- pour verifier vite : `Quick Validation Pack`
- pour ouvrir l'application : `Start BibLegacy GUI`

## Pour aller plus loin

Dans le depot principal, vous pouvez aussi ouvrir :
- `SI_TU_VEUX_X_LANCE_Y.md`
- `DAILY_MAINTENANCE.md`
- `COMMANDS_REFERENCE.md`

Dans le site local, vous pouvez aussi lire :
- `Questions Frequentes Copilot`
- `Exemples de Phrases pour Copilot`