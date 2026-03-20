# Architecture

## Vue d'ensemble
BibLegacy est une application desktop Python/Tkinter specialisee dans la detection de dossards et le renommage massif de photos. Le parcours produit courant repose sur RapidOCR, avec TrOCR en renfort optionnel sur certains cas difficiles.

## Blocs principaux
- `src/gui.py` : point d'entree de l'interface et orchestration globale
- `src/ui/` : onglets et composants UI extraits de la GUI principale
- `src/main.py` : backend lance en CLI ou par sous-processus pour les traitements lourds
- `src/core/` : logique metier reutilisable, persistance, logs, rapports, calibration, secours
- `src/ocr/` : abstraction OCR et registre des moteurs actifs
- `src/web/` : artefacts de la plateforme web post-production (`index.html`, `serveur_lbdld.py`, `generateur_index.py`)
- `config/` : persistance runtime et profils
- `logs/` : traces techniques et historiques courts
- `rapports/` : rapports Markdown horodates par categorie

## Architecture d'execution
L'interface pilote les actions utilisateur, mais le traitement OCR lui-meme reste encapsule dans le backend et des services `core/`.

Flux simplifie :
1. l'utilisateur prepare ses chemins, son prefixe et ses options dans la GUI
2. la GUI capture l'etat du run
3. le backend applique le pre-traitement standard image puis l'OCR
4. les modules `core/` enregistrent historique, rapports et traces
5. l'interface restitue la progression, les logs et les syntheses

## Stack active
- Interface : Tkinter
- OCR principal : RapidOCR
- Renfort optionnel : TrOCR
- Vision / pre-traitement : OpenCV
- Runtime inference : ONNX Runtime
- Rapports : Markdown sur disque
- Edition post-run : serveur web local genere dans la sortie

## Registre OCR
Le registre actif est centralise dans `src/ocr/registry.py`.

Etat produit courant :
- `RapidOCR` : actif
- autres moteurs : peuvent encore apparaitre dans des archives ou anciens fichiers de config, mais ne font plus partie du parcours produit courant

## Organisation des responsabilites
### GUI
- collecte les choix utilisateur
- verrouille certaines options pendant les runs
- affiche progression, logs, graphiques et documentation embarquee

### Core
- ne doit pas dependre de `src/ui/`
- gere les invariants, la persistance, les rapports et les services transverses
- constitue la zone prioritaire pour les tests automatises

### Backend OCR
- applique le pre-traitement standard
- appelle l'adaptateur OCR actif
- gere les variantes de production, fallback et renfort TrOCR

## Dossiers importants
- `config/engines/` : espaces de parametres et artefacts moteur encore utiles au runtime
- `config/test_configs.json` : profils actifs et techniques
- `config/factory_configs.json` : profils usine
- `config/test_results.json` : historique des runs
- `config/rescue_profiles.json` : profils de secours persistants
- `rapports/production/` : rapports de production individuels + cumul
- `rapports/test/` : rapports de test/calibrage selon le flux appele

## Sortie web post-production
Le backend copie automatiquement dans le dossier de sortie trois artefacts web issus de `src/web/` :
- `index.html`
- `serveur_lbdld.py`
- `generateur_index.py`

Le serveur local genere ensuite `index_photos.json` a partir des images presentes dans le dossier. Cet index peut servir a deux usages :
- navigation locale et correction manuelle post-production
- alimentation d'une page WordPress ou d'un autre front web qui doit afficher toutes les photos correspondant a un numero de dossard

## Dettes et realite terrain
- `src/gui.py` reste un gros fichier, meme apres plusieurs extractions
- des artefacts legacy peuvent encore exister dans `config/` ou `docs/dev_notes/`
- la source de verite pour le produit courant est le code actif, pas les anciennes notes
