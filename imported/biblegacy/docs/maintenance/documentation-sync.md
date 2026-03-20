# Synchronisation vers BibLegacy-Community

## Principe
La documentation source reste dans ce depot. Le depot `BibLegacy_Doc` recoit une copie generee dans un sous-dossier dedie, afin d'eviter d'ecraser ses fichiers propres comme le `README.md` public ou les annonces.

Le point d'entree est le script PowerShell `scripts/sync-community-docs.ps1`.

## Depot cible
- depot local par defaut : `D:\Dev\BibLegacy_Doc`
- remote attendu : `https://github.com/Maurice-Churlet/BibLegacy-Community.git`

## Ce qui est copie
Le contenu exporte est defini dans `docs/community-sync-manifest.json`.

Configuration initiale :
- `docs/user_guide` vers `imported/biblegacy/docs/user_guide`
- `docs/tutos` vers `imported/biblegacy/docs/tutos`
- `docs/marketing` vers `imported/biblegacy/docs/marketing`
- `docs/maintenance` vers `imported/biblegacy/docs/maintenance`
- `README.md` du depot source vers `imported/biblegacy/README-source.md`

Tu peux retirer ou ajouter des elements dans le manifeste selon ce que tu veux publier.

## Commandes
Depuis le depot source `BibLegacy` :

```powershell
./scripts/sync-community-docs.ps1
```

Pour synchroniser puis creer un commit dans `BibLegacy_Doc` :

```powershell
./scripts/sync-community-docs.ps1 -Commit
```

Pour synchroniser, committer puis pousser :

```powershell
./scripts/sync-community-docs.ps1 -Push
```

`-Push` implique aussi le commit si des changements existent.

## Resultat
Le script recree entierement le dossier gere `imported/biblegacy` dans le depot cible, puis genere un fichier `SYNC_MANIFEST.md` avec :
- le commit source
- la date de synchronisation
- la liste des repertoires et fichiers exportes

Cette approche garantit deux choses :
- le depot public garde ses fichiers manuels a la racine
- la partie synchronisee reste reproductible et simple a revoir dans Git

## Tache VS Code
Une tache VS Code `Sync Community Docs` est ajoutee dans `.vscode/tasks.json` pour lancer la synchronisation sans retaper la commande.

## Integration a l'interface BibLegacy
Le flux `Synchronisation Totale (Commit + Push)` de l'interface declenche aussi cette synchronisation automatiquement quand les fichiers exportes vers la documentation communautaire ont change.

Concretement :
- push principal de `BibLegacy`
- puis synchro automatique vers `BibLegacy_Doc`
- commit et push du depot `BibLegacy-Community`

Si aucun fichier publie n'a change, la synchro communautaire est ignoree pour eviter un commit inutile.