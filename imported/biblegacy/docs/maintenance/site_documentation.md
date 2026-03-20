# Site de documentation MkDocs

Ce depot peut maintenant produire une documentation web publique a partir d une configuration MkDocs distincte de la documentation technique interne.

## Fichiers ajoutes

- `mkdocs.yml`
- `docs-requirements.txt`
- `site_docs/`

## Objectif

La documentation sous `site_docs/` sert de facade publique ou operateur :

- presentation generale du produit
- lien de telechargement de l executable
- explication du workflow utilisateur
- integration progressive de captures d ecran

La documentation sous `docs/` reste la base technique, de maintenance et de reference pour le projet.

## Installation locale

```bash
pip install -r docs-requirements.txt
mkdocs serve
```

## Build local

```bash
mkdocs build
```

Le site genere est emis dans `site/`.

## Regle de maintenance

- garder `site_docs/` simple et public
- garder `docs/` plus detaille, technique ou interne
- si une information doit apparaitre aux deux endroits, la version publique doit rester plus courte et plus directe
