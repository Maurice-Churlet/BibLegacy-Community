# Logs et Rapports

## Deux familles a distinguer
Le produit produit a la fois :
- des logs techniques et traces de run
- des rapports Markdown destines a la lecture humaine apres execution

## Logs
Les traces runtime sont conservees dans `logs/`.

Familles actuellement prises en compte par le produit :
- `production.log`
- `maintenance_trace.log`
- `autotune_trace.log`
- `perf_history.log`
- `run_*.log`
- `trail_ocr_*.log`
- `report_*.csv`
- `smart_evolution_*.csv`

## Console GUI
La console de l'interface doit etre la sortie visible prioritaire pour les actions lancees depuis la GUI.

Regles de maintenance :
- pas de fuite utilisateur vers le terminal quand l'action vient de l'interface
- effacement de console seulement au demarrage d'une action explicite
- conservation du log integral de l'action jusqu'a sa fin
- filtrage des lignes parasites generees par certains runtimes tiers

## LoggerManager
`src/core/logger_manager.py` centralise le comportement des handlers et le muselage de bibliotheques verbeuses.

A surveiller :
- ajout de nouveaux handlers console non desires
- suppression accidentelle du handler GUI persistant
- reintroduction de bruit runtime visible en production

## Rapports
Les rapports sont ecrits dans `rapports/<categorie>/`.

Convention actuelle :
- un rapport individuel horodate par execution
- un fichier cumul reconstruit a partir des derniers rapports
- retention limitee a un petit nombre de rapports individuels

Exemples :
- `rapports/production/production_YYYY-MM-DD_HHhMMmSS.md`
- `rapports/production/production_cumul.md`

## Contenu utile des rapports de production
Les rapports de production consolident notamment :
- moteur et profil
- options fallback / TrOCR
- chemins source et sortie
- resultats globaux
- moyenne dossards/image
- temps et debits
- synthese fallback

## Purge et retention
Le produit a ete realigne pour que :
- le bouton de purge supprime les `.log` et `.csv` pris en charge
- `Logs max` s'applique aux familles reelles de traces

Avant de modifier ce comportement, verifier l'onglet Logs, la logique de purge et les attentes utilisateur documentees dans le guide embarque.
