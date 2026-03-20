# 02 - Installation

## Installation de l'executable

La version Windows diffusee aux operateurs est disponible ici :

- `https://lesbalconsdeladrome.fr/BibLegacy/gui.zip`

### Procedure recommandee

1. Telechargez `gui.zip`.
2. Decompressez l'archive dans un dossier simple, par exemple `C:\BibLegacy`.
3. Ouvrez le dossier decompresse puis lancez `gui.exe`.
4. Au premier lancement, choisissez un **Dossier Projet** dedie a votre evenement ou a votre saison.
5. L'application cree la structure projet et renseigne automatiquement le **Dossier Entree** et le **Dossier Sortie**.
6. Il ne reste plus qu'a deposer vos propres fichiers dans les autres dossiers selon l'usage voulu.

## Installation depuis le depot source

Cette partie concerne surtout la maintenance ou le developpement.

L'environnement de travail courant du depot est en Python 3.14.

```bash
pip install -r requirements.txt
python src/gui.py
```

## OCR utilise par l'application

L'application s'appuie principalement sur **RapidOCR**.

Des composants optionnels peuvent aussi intervenir selon les cases activees :

- **Fallback** : relance une passe si aucune lecture exploitable n'a ete produite.
- **TrOCR** : verification complementaire plus lente, reservee aux cas difficiles.

## Dossier Projet

Quand vous selectionnez un **Dossier Projet**, l'application cree ou verifie automatiquement cette structure :

- `Production`
- `Calibrage`
- `Test_OCR`
- `Tests OCR`
- `Base photos`
- `Output`

## Que mettre dans chaque dossier

### `Production`

Dossier optionnel de rangement. Vous pouvez y stocker vos lots source si vous voulez une structure projet propre, mais le traitement de production suit surtout le **Dossier Entree** que vous choisissez dans l'interface.

### `Calibrage`

Dossier des images de reference pour les reglages et pour certains apercus de l'interface.

- vous pouvez y mettre vos propres images representatives
- si vous regenerez un jeu canonique depuis `Base photos`, ce dossier sera recompose automatiquement

Important : les utilisateurs doivent alimenter ce dossier avec leurs propres images si des exemples adaptes ne sont pas deja presents.

### `Test_OCR`

Dossier principal pour les comparatifs courts et longs accessibles depuis l'interface.

- mode court : premiers fichiers de `Test_OCR`
- mode long : ensemble de `Test_OCR`

Si vous voulez evaluer rapidement un moteur ou un profil, c'est ici qu'il faut placer vos images de test.

### `Tests OCR`

Dossier de travail historique conserve par la structure projet. Il peut servir aux tests et a certains diagnostics, mais ce n'est pas le dossier principal des comparatifs courants.

### `Base photos`

Dossier des photos sources representatives d'une course, d'un site ou d'une saison.

- utile pour construire un jeu de calibrage canonique
- utile pour les fonctions Smart ou les preparations de jeux de travail
- a remplir avec des images variees et reelles, idealement deja triees par evenement

### `Output`

Dossier de sortie recommande pour les traitements OCR et les exports web.

On y retrouve selon les options activees :

- les photos renommees
- le sous-dossier `Failback`
- `index.html`
- `generateur_index.py`
- `serveur_lbdld.py`
- `index_photos.json`

## Preparation minimale recommandee

Pour demarrer sans configuration complexe :

1. choisissez un **Dossier Projet** vide
2. laissez l'application renseigner automatiquement **Dossier Entree** et **Dossier Sortie**
3. placez 10 a 30 images representatives dans `Test_OCR`
4. placez vos images de reference dans `Calibrage` si vous voulez utiliser le calibrage dans de bonnes conditions
5. utilisez ensuite les autres dossiers du projet en y deposant vos propres fichiers selon le besoin

## Preparation avancee recommandee

Pour exploiter toutes les fonctions :

1. remplissez `Base photos` avec un echantillon large et varie
2. remplissez `Test_OCR` avec un sous-ensemble court mais representatif
3. remplissez `Calibrage` avec vos cas reels si vous voulez un calibrage pertinent
4. utilisez ensuite les comparatifs, le calibrage puis la production
