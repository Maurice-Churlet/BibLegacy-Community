# Persistance et Config

## Principe general
BibLegacy persiste une partie importante de son etat dans `config/`. Ces fichiers sont du runtime utilisateur ou des artefacts techniques du produit. Toute evolution de schema doit etre pensee pour rester robuste face aux anciens contenus.

## Fichiers principaux
- `config/config.json` : configuration generale de l'application
- `config/paths.json` : derniers chemins utilises et prefixe
- `config/config_optimum.json` : fichier legacy encore present comme secours technique
- `config/factory_configs.json` : profils usine
- `config/test_configs.json` : profils actifs, overrides et configurations sauvegardees
- `config/test_results.json` : historique des runs et mesures
- `config/rescue_profiles.json` : profils de secours persistants
- `config/photos_metadata_cache.json` : cache de metadonnees photo

## Sous-dossier engines
`config/engines/` contient les espaces de parametres et certains artefacts moteur.

Etat observe en mars 2026 :
- `rapidocr_params.json` reste un fichier actif
- certains fichiers legacy peuvent encore etre presents sans faire partie du parcours produit courant

La regle de maintenance n'est pas de supprimer a l'aveugle, mais d'identifier si un fichier est encore reference par le code actif.

## HistoryManager
`src/core/history_manager.py` centralise une partie critique de la persistence.

Responsabilites principales :
- lecture/ecriture robuste de JSON
- support de plusieurs encodages en lecture
- creation et sanitisation des profils
- migration de certains formats anciens
- limitation de taille de l'historique

## Ecriture robuste
Points a conserver :
- tolerance aux fichiers absents ou partiellement obsoletes
- lecture defensive sur plusieurs encodages
- ecriture UTF-8 simple et previsible
- compatibilite avec les profils canoniques et leurs invariants

## Risques frequents
- ajouter un nouveau champ sans prevoir le fallback sur anciennes donnees
- casser la difference entre profil usine et profil actif
- persister des axes interdits dans `Express` ou `Standard`
- supposer qu'un ancien fichier legacy n'existe plus alors qu'il est encore present chez l'utilisateur

## Regle de modification
Avant toute modification de persistence :
1. verifier les appels dans `src/gui.py`, `src/main.py` et `src/core/history_manager.py`
2. verifier si un fichier est aussi consomme par les rapports, les graphiques ou l'UI
3. garder une logique de migration ou de fallback si des donnees historiques existent deja
