# 03 - Utilisation

## Usage standard
Pour un operateur occasionnel, le parcours normal est simple:
1. Renseignez le **Dossier Entree** avec les photos a traiter.
2. Renseignez le **Dossier Sortie** pour recevoir les photos renommees.
3. Verifiez le **Prefixe** de l'evenement.
4. Choisissez un **profil** de travail.
5. Activez, si besoin, les options **Fallback** ou **TrOCR**.
6. Lancez **Production** depuis l'onglet Production.

## Que renseigner avant de lancer Production
- **Dossier Entree** : lot d'images source a analyser.
- **Dossier Sortie** : dossier qui recevra les images renommees et les sous-dossiers generes.
- **Dossier Projet** : racine de travail du projet, utile pour les tests, calibrages et outils de maintenance.
- **Prefixe** : texte ajoute au debut des noms de fichiers produits.

## Choisir le bon profil
- **Express** : profil recommande pour l'exploitation courante. C'est le plus rapide.
- **Standard** : compromis entre vitesse et robustesse.
- **Deep** : plus complet, surtout utile pour des essais ou des cas difficiles.
- **Smart** : profil avance, reserve aux usages verifies et aux phases d'optimisation.

## Choisir les bonnes options
- **Fallback** : n'intervient que si la premiere passe ne trouve aucun dossard.
- **Fallback renforce par TrOCR** : ajoute TrOCR uniquement dans les passes de fallback. Cette option n'est utile que si Fallback est actif.
- **TrOCR** : verification plus couteuse mais plus robuste sur les cas incertains. A reserver aux lots ou la couverture prime clairement sur la vitesse.

## Recommandations pratiques
- Pour un lot normal: commencez par **Express**.
- Si trop d'images restent sans dossard: activez **Fallback**.
- Si la couverture est prioritaire et le temps secondaire: testez **TrOCR**.
- Si vous ne savez pas quoi choisir: consultez l'onglet **Stats Production** apres quelques executions comparees.

## Pendant la production
- La barre de progression et la console affichent l'avancement.
- Certaines options deviennent temporairement verrouillees pendant le traitement pour eviter les changements incoherents en cours d'execution.
- Si **Effacer sortie prod** est coche, le programme demande une confirmation avant de supprimer les images deja presentes a la racine du dossier de sortie et les sous-dossiers generes par la production.

## Apres la production
- Les photos sont renommees dans le **Dossier Sortie**.
- Si **Web / Index** est coche, le dossier de sortie recoit aussi les artefacts web de post-production.
- Les statistiques de session alimentent l'onglet **Stats Production**.
- Un rapport Markdown est genere dans `rapports/production/`.

## Sortie web et index photo
Quand l'option **Web / Index** est active, la production prepare dans le dossier de sortie :
- `index.html`
- `generateur_index.py`
- `serveur_lbdld.py`
- `index_photos.json` apres generation de l'index

Cette sortie sert a deux usages :
- controler et corriger localement les photos via la galerie et le serveur local
- reutiliser l'index des photos pour afficher toutes les images d'un numero de dossard sur une page WordPress ou un autre front web

## Workflow recommande pour WordPress
1. lancer la production avec **Web / Index** active
2. verifier que le dossier de sortie contient bien `index.html` et `index_photos.json`
3. controler localement la galerie si une reprise manuelle est necessaire
4. utiliser `index_photos.json` comme source de liste pour la page WordPress qui affiche les photos correspondant au dossard saisi

Le point cle est que l'outil ne produit pas seulement des fichiers renommes. Il prepare aussi une base web simple pour la consultation et la diffusion aval.

## Quand utiliser le calibrage
Le calibrage n'est pas obligatoire pour un usage occasionnel.

Il devient utile si:
- le type de photos change fortement,
- la distance ou l'eclairage degradent la lecture,
- vous voulez optimiser un profil pour une serie de courses recurrentes.
