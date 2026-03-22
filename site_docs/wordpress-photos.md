# Publier Les Photos Sur WordPress

Cette page sert de mode operatoire court pour publier la recherche de photos sur un site WordPress deja en ligne.

## But

Le principe est simple :

- `index_photos.json` doit etre accessible dans `wp-content/uploads/AAAA/MM/`
- la page web BibLegacy doit etre accessible sur le site
- l annee et le mois configures dans la page doivent correspondre au dossier reel du JSON

## Fichiers utiles

- `index.html`
- `index_photos.json`

Le fichier `index.html` est la page de recherche.
Le fichier `index_photos.json` contient la liste des photos disponibles.

## Procedure operateur

1. lancer la production avec l option `Web / Index`
2. verifier que le dossier de sortie contient bien `index.html` et `index_photos.json`
3. verifier dans BibLegacy que l annee et le mois WordPress pointent vers le bon dossier medias
4. envoyer `index_photos.json` dans `wp-content/uploads/AAAA/MM/`
5. envoyer `index.html` sur un emplacement public du site
6. ouvrir d abord l URL directe du JSON pour verifier qu il est bien accessible
7. ouvrir ensuite la page HTML et tester un dossard reel

## Emplacements conseilles

Cas le plus simple :

- page HTML a la racine publique du site
- JSON dans le dossier WordPress du mois cible

Exemple :

- `https://monsite.fr/index.html`
- `https://monsite.fr/wp-content/uploads/2026/06/index_photos.json`

## Verification rapide

Avant de declarer la publication terminee, verifier :

1. l URL du JSON repond sans erreur `404` ou `403`
2. la page HTML affiche que l index a ete charge
3. un dossard connu affiche bien les photos attendues

## Pannes frequentes

- mauvais annee ou mois dans la page web
- `index_photos.json` envoye dans le mauvais dossier
- ancienne version du fichier encore en cache
- page HTML placee dans un sous dossier inattendu

## A retenir

Le point critique n est pas la page HTML elle meme.
Le point critique est la correspondance exacte entre :

- le dossier `wp-content/uploads/AAAA/MM/`
- les valeurs annee mois configurees
- le fichier `index_photos.json` reellement publie