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
- `site_docs` vers `site_docs` a la racine du depot cible
- `mkdocs.yml` vers `mkdocs.yml` a la racine du depot cible
- `docs-requirements.txt` vers `docs-requirements.txt` a la racine du depot cible
- `.github/workflows/pages.yml` vers `.github/workflows/pages.yml` a la racine du depot cible
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

Depuis l ajout du site MkDocs public, la synchronisation peut aussi mettre a jour automatiquement les fichiers racine necessaires a GitHub Pages. Le flux `Commit + Push` de BibLegacy peut donc publier :

- le contenu synchronise sous `imported/biblegacy`
- la facade publique MkDocs (`site_docs`, `mkdocs.yml`, workflow Pages, dependances de build)

## Tache VS Code
Une tache VS Code `Sync Community Docs` est ajoutee dans `.vscode/tasks.json` pour lancer la synchronisation sans retaper la commande.

## Integration a l'interface BibLegacy
Le flux `Synchronisation Totale (Commit + Push)` de l'interface declenche aussi cette synchronisation automatiquement quand les fichiers exportes vers la documentation communautaire ont change.

Concretement :
- push principal de `BibLegacy`
- puis synchro automatique vers `BibLegacy_Doc`
- commit et push du depot `BibLegacy-Community`

Si aucun fichier publie n'a change, la synchro communautaire est ignoree pour eviter un commit inutile.