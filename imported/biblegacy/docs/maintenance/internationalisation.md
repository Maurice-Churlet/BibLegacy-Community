# Internationalisation FR/EN

## Objectif

Mettre en place une base simple et durable pour faire coexister une interface FR/EN sans dupliquer la logique GUI.

## Etat actuel

La base initiale repose sur :

- `src/ui/i18n.py` pour les libelles UI migrés
- `src/ui/tooltips.py` pour les infobulles FR/EN
- la preference persistante `ui_language` dans `paths.json`
- un resolveur runtime `root._ui_language_resolver` pour les widgets dependants de la langue

## Premiere zone migree

Les premiers elements relies a cette base sont :

- la case `Tool Tips` de l'onglet Production
- les cases systeme de l'onglet Parametres (`Maintenance`, `Web / Index`, `Tool Tips`, analytics, purge sortie prod)
- le selecteur `ui_language`
- les infobulles centralisees

## Regle de migration

Pour chaque nouveau texte migre :

1. ajouter une cle dans `src/ui/i18n.py` pour les libelles UI
2. ajouter une cle dans `src/ui/tooltips.py` pour les infobulles
3. eviter les chaines en dur dans les widgets Tkinter quand le texte doit devenir bilingue
4. preferer une migration par groupes coherents d'ecran plutot qu'un melange partiel ligne par ligne

## Portee restante

La majeure partie de l'interface reste encore en francais direct dans `src/gui.py` et les modules sous `src/ui/tabs/`.

Les prochaines cibles naturelles sont :

- les titres d'onglets et boutons principaux de Production
- les messages de boite de dialogue les plus frequents
- les libelles de l'onglet Parametres hors bloc systeme
- les libelles de l'onglet Logs

## Compatibilite

- valeur par defaut : `fr`
- si une ancienne config ne contient pas `ui_language`, la migration retombe sur `fr`
- si une cle manque en anglais, le fallback reste le francais
