# Utilisation

## Workflow simple

1. selectionnez le Dossier Projet
2. verifiez que le Dossier Entree et le Dossier Sortie ont ete remplis automatiquement
3. placez vos images de test dans Test_OCR
4. choisissez un profil
5. lancez un comparatif si besoin
6. lancez la production sur votre lot reel

## Choix des dossiers selon la fonction

- Comparatifs : Test_OCR
- Calibrage manuel : Calibrage
- Preparation canonique : Base photos
- Resultats : Output

## Choix des profils

- Express : le plus rapide pour l exploitation courante
- Standard : compromis entre vitesse et robustesse
- Deep : plus pousse pour les essais difficiles
- Smart : profil avance pour optimisation et usages verifies

## Options utiles

- Fallback : utile si trop d images sortent sans dossard
- TrOCR : utile sur les cas difficiles, plus lent
- Web / Index : genere une sortie web locale pour controle et relecture

## Documentation detaillee

Le depot principal conserve une documentation plus complete sur les parametres, les usages avances et la maintenance. La facade MkDocs reste volontairement orientee utilisateur final et presentation produit.