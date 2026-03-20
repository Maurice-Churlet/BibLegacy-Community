# 01 - Présentation

## Qu'est-ce que BibLegacy
**BibLegacy** est une application de lecture OCR orientee dossards de course.

Son objectif est simple :

- lire les numeros presents sur les photos,
- renommer ou classer les images produites,
- fournir assez d'outils de controle pour comparer, verifier et corriger les traitements.

L'application est pensee pour un usage de production, mais elle integre aussi des fonctions d'audit et d'optimisation pour fiabiliser les traitements sur des lots reels.

## Ce que fait l'application aujourd'hui
BibLegacy repose sur un pipeline OCR centre sur :

- des **profils canoniques** de traitement : Express, Standard, Deep et Smart,
- un **fallback** qui ne se declenche qu'en cas d'echec de la premiere passe,
- une verification **TrOCR** optionnelle pour renforcer certains cas,
- des **tests comparatifs** pour mesurer vitesse et couverture,
- des **rapports** et des **logs** pour analyser les executions.

## Pour qui
BibLegacy s'adresse surtout a des utilisateurs qui doivent traiter des lots d'images de course avec un besoin pratique :

- produire vite,
- retrouver un maximum de dossards,
- limiter les corrections manuelles,
- garder des traces exploitables quand un comportement doit etre audite.

## Philosophie d'usage
Le produit ne repose plus sur une accumulation de filtres manuels complexes.

Le fonctionnement courant repose surtout sur :

- le choix du bon profil,
- l'activation ou non de Fallback,
- l'activation ou non de TrOCR,
- un calibrage ponctuel si un type de photos le justifie.

## Points forts
- **Production directe** : traitement de lots avec progression, logs et rapports.
- **Profils lisibles** : Express pour l'exploitation courante, Standard et Deep pour renforcer, Smart pour l'optimisation avancee.
- **Fallback maitrise** : la cascade de secours ne s'active qu'en cas d'echec reel.
- **Renfort TrOCR** : possible sur tout le lot ou seulement dans les passes de fallback.
- **Comparatif integre** : tests courts ou longs pour comparer les modes de travail.
- **Audit exploitable** : onglets Logs, Stats Production et rapports Markdown.
- **Correction aval et diffusion web** : le dossier de sortie peut contenir une page HTML, un serveur local et un fichier d'index des photos pour faciliter la reprise manuelle et l'affichage des images par numero de dossard, y compris dans un usage type WordPress.

## Ce que BibLegacy n'est pas
BibLegacy n'est pas un simple visualiseur de photos ni un OCR generaliste sans cadre.

Il est structure autour d'un usage metier : la lecture et l'exploitation de dossards dans un flux de traitement controle.
