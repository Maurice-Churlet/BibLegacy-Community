# BibLegacy

BibLegacy est une application Windows de lecture OCR de dossards, orientee exploitation terrain, calibrage et post-traitement web.

## Telechargement

- Executable Windows : [BibLegacy-4.0.2.zip](https://lesbalconsdeladrome.fr/BibLegacy/BibLegacy-4.0.2.zip)

## Ce que fait BibLegacy

- renomme automatiquement les photos a partir des dossards detectes
- propose plusieurs profils de travail : Express, Standard, Deep, Smart
- permet de comparer les profils sur un dossier de test
- aide a regler le moteur OCR sur des images reelles
- peut produire une sortie web locale pour relecture et correction

## Demarrage rapide

1. telechargez et decompressez l'executable
2. lancez `BibLegacy.exe`
3. choisissez un **Dossier Projet**
4. laissez l'application renseigner automatiquement les dossiers d'entree et de sortie
5. deposez vos propres images dans `Test_OCR`, `Calibrage` ou `Base photos` selon le besoin

## Pages utiles

- [A propos](a-propos.md)
- [Installation](installation.md)
- [Utilisation](utilisation.md)
- [Accueil Copilot](copilot.html)
- [Dossier Projet](dossier-projet.md)
- [Captures d ecran](captures.md)

## Debuter avec Copilot

Si vous utilisez BibLegacy avec Copilot et VS Code, commencez par ces pages :

- [Accueil Copilot](copilot.html) : point d entree qui regroupe les pages Copilot

Version la plus directe en une page dans le depot : `SI_TU_VEUX_X_LANCE_Y.md`

Pour un demarrage tres simple :

1. lancez `/BibLegacy Start Here` dans le chat Copilot
2. si vous voulez juste verifier vite, lancez `Quick Validation Pack`
3. si vous voulez voir cette documentation dans votre navigateur, lancez `Serve Public Docs Locally`

## Apercu de l application

### Production

![Ecran de production](assets/screenshots/Production.jpg)

### Parametres

![Ecran des parametres](assets/screenshots/Parametres.jpg)

## Documentation technique du depot

La documentation de maintenance et les guides internes restent dans le depot principal. Cette partie MkDocs sert surtout de facade publique et operateur.
