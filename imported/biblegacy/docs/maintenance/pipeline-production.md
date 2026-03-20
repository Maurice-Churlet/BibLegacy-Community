# Pipeline Production

## Objectif
Le mode Production lit un dossier d'images, detecte les dossards, renomme les fichiers et prepare une sortie exploitable rapidement, y compris une plateforme web locale d'edition si necessaire.

## Entrees du pipeline
- dossier source
- dossier de sortie
- prefixe de nommage
- moteur actif : RapidOCR
- profil choisi : Express, Standard, Deep ou Smart
- options de renfort : fallback, TrOCR global, TrOCR sur fallback

## Etapes du traitement
1. validation des chemins et capture des options du run
2. chargement des parametres du profil actif
3. pre-traitement image standard : redimensionnement, CLAHE, budget OCR
4. lecture OCR principale
5. fallback si active et seulement en cas d'echec de lecture exploitable
6. verification ou renfort TrOCR selon l'option active
7. normalisation des dossards detectes
8. renommage / copie vers la sortie
9. copie des artefacts web de sortie et generation de l'index photo exploitable en post-production
10. alimentation des compteurs, logs, rapports et vues de synthese

## Regle de fallback
Le fallback doit rester un mecanisme de secours, pas une seconde passe systematique.

En pratique :
- si la lecture principale suffit, on n'active pas les profils de secours
- si la lecture echoue, on peut tenter le fallback
- si `TrOCR sur fallback` est active, TrOCR ne vient renforcer que ce chemin de secours

## Nommage de sortie
Principes actuels :
- image reconnue : prefixe + dossard(s)
- image non reconnue : compteur d'erreur de type `000-X`
- doublon : ajout d'un suffixe numerique pour eviter l'ecrasement

## Dossiers de sortie a connaitre
Selon les cas, la production peut alimenter :
- la sortie principale renommee
- `Best/` pour les fichiers tres bien classes selon la logique metier du projet
- `A_Calibrer/` pour les images a reutiliser lors d'un futur calibrage
- dossiers d'erreur ou equivalents pour les cas sans dossard exploitable
- artefacts web locaux pour la correction manuelle finale et la diffusion via page HTML / index photo

## Artefacts web generes
Le pipeline peut deposer dans le dossier de sortie :
- `index.html` pour la galerie ou page de consultation locale
- `serveur_lbdld.py` pour servir localement le dossier et gerer certains renommages
- `generateur_index.py` pour reconstruire l'index des photos
- `index_photos.json` une fois l'index genere

Ce mecanisme est important parce qu'il ne sert pas seulement a corriger localement le lot. Il permet aussi d'exposer toutes les images d'un dossard donne dans une page WordPress ou un front equivalent base sur l'index.

## Mesures suivies
Le pipeline nourrit notamment :
- nombre total de fichiers traites
- nombre d'images en erreur
- dossards moyens par image
- temps total, temps OCR, temps fallback
- debit images/seconde
- indicateurs de succes utilises dans les rapports et graphiques

## Points d'attention
- une option utilisateur doit etre capturee au lancement du run et ne pas changer en cours de traitement
- la console GUI doit montrer l'action courante sans fuite parasite vers le terminal
- le STOP doit rester propre et ne pas corrompre les fichiers de persistance
- les descriptions produit doivent rester coherentes avec un pipeline RapidOCR + renforts, pas avec un ancien discours multi-moteur
