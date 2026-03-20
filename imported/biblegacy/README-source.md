# BibLegacy

Projet OCR oriente detection de dossards avec interface graphique, profils canoniques, fallback, verification TrOCR optionnelle et outils de calibrage / audit.

## Modes de Fonctionnement

> Note produit (Mars 2026) : les filtres manuels de pre-traitement ne sont plus utilises. Le pipeline est desormais centre sur le calibrage moteur et le pre-traitement standard (scale/clip).

### 🎯 Mode Calibrage (Optimisation)
Le calibrage est l'étape essentielle pour adapter l'OCR à la qualité de vos photos. Il s'ouvre via un dialogue dédié et propose trois niveaux d'analyse :

- **⚡ Express (Tier 1)** : Scan rapide des paramètres de pré-traitement (Zoom, Contraste). Idéal pour un premier réglage rapide.
- **⚖ Standard (Tier 2)** : Équilibre entre rapidité et précision. Teste les paramètres de base + les réglages essentiels du moteur OCR.
- **🧠 Deep (Tier 3)** : Recherche exhaustive sur l'intégralité des paramètres disponibles pour une précision maximale.

**Fonctionnalités du calibrage :**
- **Gestionnaire d'images** : Ajoutez vos propres images de test (limite de 10) pour optimiser sur des cas réels.
- **Visualisation** : Mode Liste ou Mode Vignettes (vignettes de 120px) avec visionneuse intégrée (double-clic).
- **Grid Search** : Recherche automatique de la meilleure combinaison de paramètres.
- **Densité variable** : Ajustez la finesse de la recherche via un curseur dédié.

### 🚀 Mode Production
Utilise la configuration optimisee pour le renommage massif des images du dossier d'entree vers le dossier de sortie.

- **Nomenclature intelligente** : 
    - Fichiers reconnus : `PREFIXE_DOSSARD1_DOSSARD2.ext`
    - Fichiers non reconnus : `PREFIXE_000-X.ext` (où X est un compteur d'erreurs commençant à 1).
- **Mode Express ⭐** : traitement prioritaire pour l'exploitation courante.
- **Gestion des doublons** : Ajout automatique d'un suffixe (-1, -2) si plusieurs photos portent le même nom après renommage.
- **STOP/Arrêt propre** : Interruption instantanée et sécurisée via le bouton STOP.
- **🌐 Plateforme Web d'Édition** : À la fin du traitement, le système déploie automatiquement dans le dossier `output` une page HTML, les scripts web associés et un mécanisme de génération d'index photo. Cet ensemble permet de visualiser les photos, de renommer manuellement les dossards via un serveur local sécurisé (`http://127.0.0.1:5000`) et de réutiliser l'index pour afficher les images d'un dossard sur une page WordPress.

## Installation

1. **Créer l'environnement virtuel** :
   ```bash
   python -m venv venv
   ```
2. **Activer l'environnement** :
   - Windows : `.\venv\Scripts\activate`
   - Linux/Mac : `source venv/bin/activate`
3. **Installer les dépendances** :
   ```bash
   pip install -r requirements.txt
   ```

## Utilisation

Le projet se pilote via son **interface graphique organisée en onglets**.

```bash
python src/gui.py
```

### Onglets de l'Interface
- **🚀 Production** : Tout le necessaire pour le traitement massif quotidien.
- **📖 Read me** : Accès direct à cette documentation avec formatage dynamique.

### Interface Professionnelle
- **📂 Gestion compacte** : Dossiers d'entree/sortie et Prefixe regroupes pour une efficacite maximale.
- **⚙️ Paramètres Moteur** : Section rétractable pour ajuster manuellement les paramètres fins si nécessaire.
- **📉 Graphiques de Performance** : Visualisez les résultats de vos calibrages (Temps vs Réussite) via le menu de diagnostic (clic droit).

## Workflow Recommandé

1. **Phase Initiale** : Ouvrez le **Calibrage**, ajoutez quelques photos représentatives de votre course, et lancez un calibrage **Standard**.
2. **Validation** : Vérifiez les statistiques et graphiques de performance.
3. **Optimisation finale** : Appliquez les meilleurs paramètres trouvés via le bouton dédié.
4. **Production** : Réglez votre préfixe (ex: "2026_Drôme") et lancez le **Traitement OCR**.

## CLI (Ligne de commande)
Pour les utilisateurs avancés ou l'automatisation :
```bash
# Lancer un calibrage Deep avec la configuration courante
python src/main.py --mode CALIB --calib-tier 3

# Lancer la production
python src/main.py --mode P --input C:\Photos\In --output C:\Photos\Out --prefix "Trail_2026"
```

## Système de Configuration
Les fichiers sont stockés dans le dossier `config/` :
- `engines/*.json` : Parametres de travail et historiques techniques conserves par le projet.
- `test_configs.json` : Historique de vos calibrages.
- `paths.json` : Chemins et préfixe persistants.
