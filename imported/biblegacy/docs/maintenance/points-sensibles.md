# Points Sensibles

## 1. Invariants des profils canoniques
C'est la zone la plus fragile fonctionnellement.

Ne jamais casser :
- `Express` limite a `scale` et `clip_limit`
- `Standard` limite a `scale`, `clip_limit`, `box_thresh`, `text_score`
- `Deep` et `Smart` ouverts a tous les axes moteur

## 2. Fallback
Le fallback doit rester un secours declenche sur echec, pas une routine appliquee a toutes les images. Toute regression ici se paie immediatement en temps de production.

## 3. GUI massive
`src/gui.py` reste volumineux. Une petite modification locale peut avoir des effets de bord sur :
- persistence
- console GUI
- verrous d'execution
- resumes et tableaux de synthese

## 4. Separation UI / Core
`src/core/` ne doit pas importer `src/ui/` ni `gui.py`. Cette frontiere est importante pour la testabilite et pour eviter de remettre de la logique metier dans l'interface.

## 5. Documentation embarquee
L'onglet Documentation charge `docs/user_guide/` directement. Toute page fausse ou obsolete dans ce dossier devient un probleme produit visible immediatement.

## 6. Legacy non archive
Il subsiste encore des artefacts historiques dans le depot :
- notes de developpement
- fichiers de config anciens
- anciens termes OCR dans les archives

Ne pas confondre presence dans le depot et capacite encore supportee par le produit.

## 7. Bruit runtime
Le code actif contient encore quelques filtres defensifs contre des sorties verbeuses de runtimes tiers. Les supprimer sans verification peut degrader fortement la lisibilite de la console utilisateur.

## 8. Rapports et metriques
Les rapports sont lus humainement pour prendre des decisions. Si une metrique change de sens, il faut mettre a jour en meme temps :
- le code producteur
- les tableaux de synthese
- la documentation embarquee ou maintenance qui s'y refere
