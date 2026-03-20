# Tests et Validation

## Objectif
La validation doit couvrir en priorite les comportements sensibles du produit : production, persistence, profils canoniques, logs GUI et documentation embarquee.

## Suite pytest presente
Le depot contient notamment des tests sur :
- le chargement de la documentation embarquee
- les variantes de production express et fallback
- la persistence des profils et resultats
- la gestion des verrous runtime GUI
- la barre de progression et les resumes de production
- les logs et la redirection stdout/stderr
- les profils de secours
- TrOCR

## Fichiers representatifs
Quelques tests utiles comme point d'entree :
- `tests/test_doc_tab_loading.py`
- `tests/test_comparative_express_variants.py`
- `tests/test_history_manager_profiles.py`
- `tests/test_history_manager_production_metrics.py`
- `tests/test_logger_manager_stdout_mirror.py`
- `tests/test_logs_delete_behavior.py`
- `tests/test_rescue_profiles.py`
- `tests/test_trocr_verifier.py`

## Strategie pratique
### Pour une modification documentaire
- verifier la page modifiee
- verifier si elle est exposee dans `docs/user_guide/`
- lancer au minimum le test de chargement documentation si le comportement d'affichage est touche

### Pour une modification de profils / Smart / persistence
- relire les invariants canoniques
- executer les tests `history_manager`, profils et secours
- verifier l'absence de derive sur les axes interdits

### Pour une modification logs / console / sous-processus
- executer les tests logger, logs et verrous GUI
- verifier qu'aucun bruit runtime n'apparait dans la console utilisateur

### Pour une modification du pipeline production
- executer les tests de variantes express/fallback
- controler les compteurs et rapports lies a la production

## Validation manuelle recommandee
Selon la nature du changement, faire au moins un controle manuel sur :
- lancement GUI
- affichage des onglets concernes
- production courte sur un lot simple
- creation de rapport et mise a jour du dossier `logs/`

## Regle de prudence
Ne pas elargir une correction a des zones non testees sans verification. Le depot comporte encore des artefacts historiques et un gros `src/gui.py`, ce qui augmente le risque de regression laterale.
