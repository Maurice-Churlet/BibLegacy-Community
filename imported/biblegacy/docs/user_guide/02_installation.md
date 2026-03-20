# 02 - Installation

## Pré-requis
L'application nécessite un environnement Python recent. Dans ce depot, l'environnement de travail courant est en Python 3.14.

### Dependances principales :
- **OpenCV** : Traitement d'image et pre-traitement local (zoom, contraste CLAHE).
- **Pillow** : Support des formats d'image et interface.
- **NumPy** : Calculs numeriques utilises par le pipeline OCR.

## OCR utilise par l'application
L'application actuelle s'appuie sur **RapidOCR** comme moteur OCR principal.

Dans le cadre normal d'utilisation de ce projet, l'installation des dependances du depot suffit :

```bash
pip install -r requirements.txt
```

Il n'y a pas de configuration utilisateur courante a faire pour un autre moteur OCR.

## Composants optionnels
Selon les fonctions activees, d'autres composants peuvent intervenir :

- **TrOCR** : renfort optionnel sur certains cas plus incertains,
- composants de support deja references par le depot et ses dependances.

## Structure du Projet
Pour un fonctionnement optimal via le "Dossier Projet", respectez cette structure :
- `Calibrage_Smart/` : Images ou jeux de travail lies aux fonctions de calibrage et d'optimisation.
- `Production/` : Images a traiter pour l'evenement si vous structurez votre projet ainsi.
- `Base photos/` : Fichiers sources optionnels.
- `Output/` : Destination des fichiers renommés.
