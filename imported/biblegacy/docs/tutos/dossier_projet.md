# Dossier Projet

Le **Dossier Projet** est la racine de travail de BibLegacy.

Quand vous le selectionnez, l'application cree automatiquement les dossiers suivants :

- `Production`
- `Calibrage`
- `Test_OCR`
- `Tests OCR`
- `Base photos`
- `Output`

## Role des dossiers

- `Test_OCR` : dossier principal pour les comparatifs courts et longs.
- `Calibrage` : images de reference pour le calibrage et certains apercus.
- `Base photos` : reservoir large d'images reelles pour preparer un jeu canonique.
- `Output` : destination recommandee des traitements OCR et des exports web.
- `Production` : rangement optionnel pour vos lots source.
- `Tests OCR` : dossier historique conserve pour certains usages de test et de diagnostic.

## Bon usage

Pour un projet neuf :

1. choisissez un dossier vide comme Dossier Projet
2. laissez l'application creer la structure
3. mettez quelques images dans `Test_OCR`
4. mettez un plus gros echantillon dans `Base photos` si vous comptez utiliser le calibrage avance
5. utilisez `Output` comme sortie par defaut
