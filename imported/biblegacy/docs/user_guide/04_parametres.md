# 04 - Parametres

## Configuration generale
La zone **Configuration Generale** regroupe les reglages indispensables a l'exploitation quotidienne.

### Dossiers
- **Dossier Entree** : source des images a traiter.
- **Dossier Sortie** : destination des images renommees et des dossiers produits.
- **Dossier Projet** : dossier de travail du projet, utile pour les fonctions de support, de calibrage et de maintenance.

### Prefixe
Le **Prefixe** est ajoute au nom des fichiers produits. Il permet d'identifier rapidement la course ou la serie traitee.

## Profils
Les profils regissent la maniere dont le moteur OCR travaille.

- **Express** : le plus rapide, recommande pour la plupart des productions.
- **Standard** : plus tolerant, plus lent.
- **Deep** : plus poussé, utile pour l'analyse et l'optimisation.
- **Smart** : profil avance, reserve aux usages verifies.

## Options de traitement

### Fallback
Si **Fallback** est active, le programme ne lance des passes de repli que si la passe principale n'a trouve aucun dossard.

Usage recommande:
- a activer si trop d'images sortent sans dossard,
- a laisser desactive si la vitesse est prioritaire et que le lot est deja bien lu.

### Fallback renforce par TrOCR
Cette option utilise **TrOCR uniquement dans les passes de fallback**.

Regles importantes:
- elle n'a de sens que si **Fallback** est actif,
- elle est desactivee si **TrOCR** global est actif,
- elle sert a renforcer les cas d'echec sans appliquer TrOCR a tout le lot.

### TrOCR
Active une verification plus robuste mais plus lente.

Usage recommande:
- pour les lots difficiles,
- quand l'objectif principal est de recuperer un maximum de dossards,
- a eviter comme choix par defaut si le temps de traitement est critique.

## Reglages systeme utiles

### Logs max
Definit combien de fichiers recents sont conserves pour les principales familles de traces.

Ce reglage agit sur les journaux et traces techniques du dossier `logs/`.

### Purger logs/CSV
Supprime les fichiers `.log` et `.csv` du dossier `logs/`.

Ce bouton n'efface pas les rapports Markdown de `rapports/`.

### Maintenance
Active les traces plus techniques et detaillees, utiles surtout pour l'audit ou le developpement.

### Warnings
Controle les confirmations et avertissements interactifs.

### Web
Prepare les artefacts web de sortie : page HTML, scripts locaux et index des photos.

Usage typique:
- ouvrir localement la galerie de controle post-production,
- regenerer l'index des photos du dossier de sortie,
- exploiter cet index pour afficher toutes les images d'un dossard donne dans une page WordPress ou un site equivalent.

### Effacer sortie prod
Avant une nouvelle production, supprime uniquement les images de sortie deja generees a la racine du dossier choisi et les sous-dossiers geres par la production.

Le programme demande une confirmation avant cette purge.

## Reglages avances moteur
Les reglages avances permettent d'agir plus finement sur le moteur OCR.

Les plus frequents sont:
- **scale** : agrandissement de l'image avant OCR,
- **clip_limit** : renforcement de contraste local.

Selon le moteur et le profil, d'autres parametres peuvent apparaitre.

Pour un operateur occasionnel, il vaut mieux ne modifier ces valeurs qu'apres essai ou recommandation issue d'un calibrage.

## Point important
Les anciens filtres manuels ne font plus partie du fonctionnement normal du produit.
La logique actuelle repose surtout sur:
- le choix du profil,
- les options Fallback / TrOCR,
- les reglages moteur valides pour le profil actif.
