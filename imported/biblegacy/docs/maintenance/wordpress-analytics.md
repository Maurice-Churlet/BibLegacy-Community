# WordPress Analytics BibLegacy

## Objectif
Fournir un backend tres simple pour les statistiques anonymes de BibLegacy sur un site WordPress heberge chez OVH.

Le besoin couvert est limite a deux usages :
- recevoir un resume anonyme envoye par l'application apres une production reussie
- exposer un resume global pour alimenter le cadre `Stat mondiales` de l'interface

## Fichier livre dans le depot
Plugin minimal a deposer dans WordPress :
- `scripts/wordpress/biblegacy-stats.php`

## Endpoints exposes
Le plugin enregistre deux routes REST publiques.

### POST `/wp-json/biblegacy/v1/stats`
Reoit un payload JSON envoye par BibLegacy.

Le `POST` doit aussi contenir le header :

```text
X-BibLegacy-Key: 5a9696f4ffdc449c9ccec1873a23d79695a2648936b94611921e1c3c6a896ef9
```

Payload attendu :

```json
{
  "installation_id": "3c7f6b5f-7d3f-4d31-aed4-3b4ef6cc1f42",
  "app_version": "2.0",
  "event_type": "production_summary",
  "sent_at": "2026-03-21T14:20:00Z",
  "platform": "win32",
  "processed_images_total": 1248,
  "run_images_count": 85,
  "files_in_error": 4,
  "avg_time": 1.42,
  "avg_bibs": 1.17,
  "engine_name": "RapidOCR",
  "profile_name": "Smart",
  "use_fallback": true,
  "use_trocr": false,
  "use_trocr_on_fallback": true
}
```

Reponse attendue :

```json
{
  "ok": true,
  "event_id": 123
}
```

### GET `/wp-json/biblegacy/v1/stats/summary`
Retourne le resume global consomme par l'application.

Reponse attendue :

```json
{
  "installations": 37,
  "processed_images": 182540,
  "updated_at": "2026-03-21 14:20:05"
}
```

## Logique d'agregation
Le plugin ne somme pas toutes les lignes brutes car `processed_images_total` est cumulatif par installation.

Resume calcule :
- `installations` = nombre distinct d'`installation_id`
- `processed_images` = somme du `MAX(processed_images_total)` de chaque installation

Cela evite de surcompter les postes qui envoient plusieurs evenements au fil du temps.

## Installation sur OVH
1. creer un dossier `wp-content/plugins/biblegacy-stats-api/`
2. y copier le fichier `biblegacy-stats.php`
3. activer le plugin depuis l'administration WordPress
4. verifier que les routes REST repondent

Exemples rapides :
- `https://votre-site.tld/wp-json/biblegacy/v1/stats/summary`
- test `POST` via Postman ou `curl`

## Configuration cote BibLegacy
Dans `src/app_version.py`, renseigner les trois constantes :

- `ANALYTICS_ENDPOINT_URL`
- `ANALYTICS_SUMMARY_URL`
- `ANALYTICS_API_KEY`

Exemple :

```python
ANALYTICS_ENDPOINT_URL = "https://votre-site.tld/wp-json/biblegacy/v1/stats"
ANALYTICS_SUMMARY_URL = "https://votre-site.tld/wp-json/biblegacy/v1/stats/summary"
ANALYTICS_API_KEY = "votre-cle-longue-aleatoire"
```

Dans le plugin WordPress, la meme cle doit etre reportee dans la constante `API_KEY`.

## Donnees stockees
Le plugin stocke uniquement :
- identifiant d'installation aleatoire
- version app
- type d'evenement
- compteurs techniques
- moteur et profil
- date de reception

Le plugin ne collecte pas :
- nom de machine
- utilisateur Windows
- chemin local
- numero de serie materiel

## Limites actuelles
- authentification simple par cle partagee uniquement
- pas de limite de debit applicative cote serveur
- pas de purge automatique des evenements anciens

Cette version est volontairement minimale pour valider la chaine de bout en bout sur OVH.

## Durcissement recommande ensuite
1. limiter le debit par IP ou via transient WordPress
2. ajouter une page d'administration pour voir les agregats
3. purger les evenements tres anciens si besoin
4. externaliser la cle dans une configuration serveur plutot qu'en dur dans le plugin