# Workflow Copilot pour BibLegacy

## Objectif
Ce document explique comment utiliser le pack de prompts, skills et taches VS Code ajoute au depot pour travailler plus proprement, meme avec un niveau technique limite.

## Idee generale
Le depot contient maintenant trois couches utiles :
- `AGENTS.md` : regles globales critiques du projet
- `.github/prompts/` : commandes ponctuelles faciles a lancer depuis le chat
- `.github/skills/` : workflows plus structures pour les zones sensibles

## Comment lancer un prompt ou un skill
Dans le chat Copilot :
1. taper `/`
2. choisir le prompt ou le skill voulu
3. decrire le changement ou le probleme en une phrase simple

Point d'entree recommande : `BibLegacy Start Here`

## Tableau de choix rapide
| Besoin | Choix recommande | Pourquoi |
|---|---|---|
| Je suis perdu | `BibLegacy Start Here` | oriente vers le bon prompt, fichier ou test |
| Je veux une version ultra simple | `BibLegacy Daily Maintenance` | montre l'essentiel a retenir |
| J'ai modifie la GUI | `BibLegacy GUI Regression` | cible les zones GUI fragiles |
| J'ai modifie la config ou les profils | `BibLegacy Persistence Migration` | cible la persistance et la compatibilite |
| J'ai modifie la production OCR | `BibLegacy Production Pipeline` | cible le pipeline operateur |
| Je prepare une livraison | `BibLegacy Release Readiness` | rappelle les controles de release |
| Je veux verifier vite plusieurs zones | `Quick Validation Pack` | enchaine les validations principales |

## Prompts disponibles
- `BibLegacy Start Here` : point d'entree simple pour choisir le bon prochain pas
- `BibLegacy Daily Maintenance` : version tres courte pour retenir l'essentiel au quotidien
- `BibLegacy Guided Help` : aide simple si vous ne savez pas quoi faire ensuite
- `BibLegacy GUI Regression` : verification ciblee d'un bug ou d'une regression GUI
- `BibLegacy Persistence Migration` : travail autour des configs et migrations runtime
- `BibLegacy Production Pipeline` : analyse d'un probleme de production
- `BibLegacy Release Readiness` : verifier si une release est prete
- `BibLegacy Windows Release` : preparer la release Windows
- `BibLegacy Docs Sync` : gerer la doc publique et la synchronisation communautaire
- `BibLegacy Artifact Cleanup` : trier les artefacts a supprimer ou garder

## Ce que fait chaque commande en une phrase
- `BibLegacy Start Here` : vous dit quel prompt, quelle tache ou quel fichier utiliser ensuite
- `BibLegacy Daily Maintenance` : vous donne la version la plus courte du workflow quotidien
- `BibLegacy Guided Help` : vous explique simplement la prochaine action la plus sure
- `BibLegacy GUI Regression` : vous aide a verifier qu'un changement GUI n'a pas casse une zone sensible
- `BibLegacy Persistence Migration` : vous aide a valider config, profils, sauvegarde et compatibilite
- `BibLegacy Production Pipeline` : vous aide a raisonner sur le run OCR et ses impacts operateur
- `BibLegacy Release Readiness` : vous aide a verifier qu'une release est vraiment prete
- `BibLegacy Windows Release` : vous guide pour produire et controler la release Windows
- `BibLegacy Docs Sync` : vous aide a mettre a jour et synchroniser la documentation
- `BibLegacy Artifact Cleanup` : vous aide a trier les artefacts a supprimer ou conserver

## Skills disponibles
- `gui-regression`
- `persistence-migrations`
- `production-pipeline`
- `release-windows`
- `docs-community-sync`

## Taches VS Code utiles
Voir `.vscode/tasks.json` pour lancer sans retaper les commandes :
- lancement GUI
- suite GUI ciblee
- suite persistence ciblee
- suite production ciblee
- pack de validation rapide
- build docs MkDocs
- build Windows PyInstaller
- synchronisation doc communautaire

## Ce que fait chaque tache en une phrase
- `Start BibLegacy GUI` : ouvre l'application depuis le code source
- `GUI Regression Suite` : execute une verification GUI ciblee
- `Persistence Regression Suite` : execute les tests critiques de config et profils
- `Production Smoke Suite` : execute une verification rapide du pipeline de production
- `Quick Validation Pack` : enchaine les validations principales
- `Build Public Docs` : reconstruit la documentation publique
- `Build Windows EXE` : reconstruit l'executable Windows
- `Sync Community Docs` : lance la synchronisation vers la documentation communautaire

## Recommandation pratique
Pour une personne non specialiste :
1. commencer par `BibLegacy Start Here`
2. si le probleme touche un onglet ou un bouton, utiliser `BibLegacy GUI Regression`
3. si le probleme touche les dossiers, la config ou une mise a jour, utiliser `BibLegacy Persistence Migration`
4. avant une livraison, utiliser `BibLegacy Release Readiness`

Version encore plus simple : ouvrir `DAILY_MAINTENANCE.md` pour retenir seulement 3 commandes et 3 taches.

Reference concise complete : ouvrir `COMMANDS_REFERENCE.md`.

Version une-page ultra directe : ouvrir `SI_TU_VEUX_X_LANCE_Y.md`.

## Regle de prudence
Les prompts et skills aident a aller plus vite, mais ils ne remplacent pas une verification ciblee. Sur BibLegacy, les zones les plus fragiles restent :
- les profils canoniques
- la persistence runtime
- le pipeline production
- `src/gui.py`