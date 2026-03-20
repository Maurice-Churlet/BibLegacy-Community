# Sortie Web et WordPress

## Objectif
Documenter la chaine post-production qui prepare une consultation web locale et une reutilisation aval des photos par numero de dossard, notamment dans un site WordPress.

## Artefacts generes
Le produit peut deposer dans le dossier de sortie :
- `index.html`
- `generateur_index.py`
- `serveur_lbdld.py`
- `index_photos.json` apres execution du generateur ou du serveur local

## Provenance des fichiers
Les fichiers sources vivent dans `src/web/` et sont copies dans le dossier de sortie par le backend et par certains flux GUI.

Points d'entree observes :
- `src/main.py` via `copier_fichiers_auxiliaires(path_out)`
- `src/gui.py` via `_setup_web_files_silently()` et `_launch_web_platform()`

## Roles de chaque fichier
### `index.html`
- fournit un widget de recherche par dossard
- sait fonctionner en mode local avec le serveur Flask
- sait aussi tenter une consultation distante basee sur `index_photos.json`
- propose une logique de recherche adaptee aux noms de fichiers produits

### `generateur_index.py`
- parcourt le dossier courant
- liste les images prises en charge
- ecrit `index_photos.json`

### `serveur_lbdld.py`
- sert `index.html`
- expose `/index` pour regenerer ou lire l'index courant
- expose `/rename` pour le renommage manuel en mode local
- ouvre le navigateur sur `http://127.0.0.1:5000`

### `index_photos.json`
- contient la liste des images disponibles
- sert de base a la recherche par numero de dossard
- peut etre reconsomme par une page WordPress ou un front equivalent

## Workflow local
1. production avec l'option `Web / Index`
2. copie des fichiers web dans le dossier de sortie
3. execution de `generateur_index.py`
4. lancement optionnel de `serveur_lbdld.py`
5. consultation locale via `index.html` ou via le serveur Flask
6. renommage manuel eventuel

## Workflow WordPress
Le principe d'integration n'est pas une API metier complexe. Il repose sur un index photo simple.

Flux typique :
1. deposer `index.html` et `index_photos.json` dans un emplacement servi par le site
2. rendre `index_photos.json` accessible dans une arborescence de type `wp-content/uploads/YYYY/MM/`
3. laisser le widget charger l'index correspondant
4. rechercher les photos a partir du numero de dossard saisi

## Comportement du widget HTML
Le widget inclus dans `src/web/index.html` gere plusieurs cas :
- mode local en `file:` ou via `127.0.0.1:5000`
- mode edition si le serveur Flask est joignable
- mode consultation distante si un `index_photos.json` est expose cote WordPress

Le code essaie de detecter des index sous `wp-content/uploads/YYYY/MM/`, mais le mois cible est volontairement fixe dans le widget puis adapte au moment du deploiement sur le site en fonction du repertoire reel des medias.

Cela privilegie un affichage plus rapide et evite une exploration trop large de l'arborescence distante.

## Convention implicite de nommage
La recherche HTML suppose que les noms de fichiers produits conservent une structure exploitable par regex :
- dossard numerique dans le nom
- separateur `_`, `-` ou `.`
- marquages speciaux pour certains cas comme retouche ou erreur

Toute modification de la convention de nommage doit etre revalidee contre la logique de recherche JavaScript.

## Points sensibles
- ne pas supprimer `index.html` lors des purges de sortie si la sortie web doit etre conservee
- ne pas casser la compatibilite du JSON avec le widget HTML
- ne pas renommer les fichiers web sans mettre a jour la copie backend et GUI
- ne pas modifier les regex de recherche sans verifier les noms de fichiers reels
- attention aux hypotheses implicites sur la structure `wp-content/uploads/YYYY/MM/`
- ne pas generaliser automatiquement la recherche des mois WordPress si le deploiement a besoin d'un chargement cible et rapide

## Validation recommandee
Apres une modification de cette chaine, verifier au minimum :
1. la presence des fichiers web dans le dossier de sortie
2. la generation correcte de `index_photos.json`
3. l'ouverture locale via `serveur_lbdld.py`
4. la recherche par dossard dans `index.html`
5. le chargement distant d'un `index_photos.json` dans une structure WordPress de test
