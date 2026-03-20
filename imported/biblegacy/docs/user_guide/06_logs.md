# 06 - Logs et Analyse

## Deux niveaux a distinguer
BibLegacy expose les informations de suivi a deux endroits :

- la **console** en bas de la fenetre, utile pendant l'action en cours,
- l'**onglet Logs**, utile pour relire, sauvegarder ou supprimer des traces deja ecrites.

## Console en bas de l'interface
La console affiche les messages en temps reel pendant une production, un test comparatif, un calibrage ou un diagnostic.

Vous y verrez notamment :

- l'avancement d'une production,
- les messages de fallback,
- les chargements de moteurs,
- les avertissements ou erreurs bloquantes,
- certains messages de maintenance si le mode Maintenance est actif.

Point pratique :

- un **double-clic** sur l'en-tete de console permet d'effacer l'affichage courant,
- une nouvelle action utilisateur importante peut aussi reinitialiser la console pour repartir sur un journal propre.

## Onglet Logs
L'onglet **Logs** permet de consulter les fichiers deja enregistres.

Fonctions principales :

- **Actualiser** : recharge la liste des fichiers visibles,
- **Enregistrer** : sauvegarde le contenu si vous modifiez un fichier editable,
- **Supprimer** : efface les fichiers visibles de la categorie selectionnee,
- **Vue Maintenance** : affiche une lecture plus technique de certains contenus.

Categories principales :

- **Logs** : journaux texte de fonctionnement,
- **Rap** : rapports et traces lisibles d'analyse,
- **IA** et **Doc** : contenus d'assistance et de travail plus specialises.

## Fichiers de traces courants
Les principaux fichiers utilises aujourd'hui se trouvent dans le dossier `logs/`.

Les plus utiles sont :

- `production.log` : journal principal des executions et des messages utiles a l'exploitation,
- `maintenance_trace.log` : traces techniques detaillees quand le mode Maintenance est actif,
- `autotune_trace.log` : details lies a l'Auto-Tune,
- `perf_history.log` : historique technique de performance,
- `run_*.log` : traces de certaines executions ponctuelles,
- `report_*.csv` : sorties CSV d'analyse ou de comparatif,
- `smart_evolution_*.csv` : historique CSV des evolutions Smart.

Les rapports Markdown, eux, sont ranges dans `rapports/` et non dans `logs/`.

## Logs max
Le parametre **Logs max** dans l'onglet Parametres regle combien de fichiers recents sont conserves pour chaque grande famille de traces.

Cela concerne notamment :

- `production.log`,
- `maintenance_trace.log`,
- `autotune_trace.log`,
- `perf_history.log`,
- `run_*.log`,
- `trail_ocr_*.log` s'il en reste d'anciennes series,
- `report_*.csv`,
- `smart_evolution_*.csv`.

Ce reglage permet d'eviter que le dossier `logs/` grossisse inutilement.

## Purger logs/CSV
Le bouton **Purger logs/CSV** supprime les fichiers `.log` et `.csv` du dossier `logs/`.

Il ne supprime pas :

- les rapports Markdown du dossier `rapports/`,
- la documentation du dossier `docs/`.

Utilisez cette fonction si vous voulez repartir d'un dossier de traces propre avant une nouvelle serie de tests.

## Quand activer Maintenance
Le mode **Maintenance** est utile si vous cherchez a comprendre finement ce qui se passe.

Par exemple :

- verifier pourquoi une image prend beaucoup plus de temps qu'une autre,
- voir quand TrOCR ou un fallback a ete declenche,
- analyser un comportement anormal avant de transmettre les traces.

Pour une exploitation courante, il peut rester desactive.

## Bon reflexe d'analyse
En cas de doute :

1. regardez d'abord la console pour comprendre l'action en cours,
2. ouvrez ensuite `production.log` dans l'onglet Logs,
3. si le sujet est technique, activez Maintenance puis consultez `maintenance_trace.log`,
4. si vous comparez plusieurs executions, completez avec les rapports Markdown dans `rapports/`.
