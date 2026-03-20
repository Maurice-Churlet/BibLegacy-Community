# Profils et Invariants

## Profils canoniques
Le produit repose sur quatre profils canoniques :
- `Express`
- `Standard`
- `Deep`
- `Smart`

Ces profils ne sont pas de simples etiquettes marketing. Ils portent des regles structurelles qui doivent rester coherentes dans la persistence, la propagation Smart et l'UI avancee.

## Axes autorises par profil
Regle canonique a respecter :
- `Express` : seuls `scale` et `clip_limit` sont ajustables
- `Standard` : seuls `scale`, `clip_limit`, `box_thresh` et `text_score` sont ajustables
- `Deep` : tous les axes de calibration moteur sont ajustables
- `Smart` : tous les axes de calibration moteur sont ajustables

## Consequences obligatoires
- tout parametre non editable pour un profil canonique doit revenir a la valeur par defaut moteur
- `Express` et `Standard` ne doivent jamais conserver une derive sur des axes interdits
- les profils actifs et les profils usine doivent etre sanitizes selon les memes regles
- l'UI avancee doit griser et desactiver les lignes immuables
- il ne faut pas reintroduire de comparaison entre profils canoniques avec des axes immuables differents

## Smart
`Smart` est un profil actif a part entiere.

Cela implique :
- presence dans la selection de profil
- profil usine dedie
- restauration et persistence comme les autres profils canoniques
- arret propre avec conservation du meilleur etat valide selon le mode d'arret

## Profils usine vs profils actifs
- les profils usine vivent dans `config/factory_configs.json`
- les profils actifs et derives vivent dans `config/test_configs.json`
- une restauration usine ne doit pas laisser des parametres interdits derives sur un profil canonique

## Modules a surveiller
Les invariants sont particulierement sensibles dans :
- `src/core/calibration.py`
- `src/core/history_manager.py`
- `src/main.py`
- `src/gui.py`

## Regle pratique pour les evolutions
Si une modification touche Smart, la propagation de profils, la sauvegarde de config ou l'UI des parametres avances, il faut verifier explicitement :
1. la sanitisation des profils canoniques
2. la persistence des profils usine et actifs
3. le verrouillage visuel des champs immuables
4. les tests cibles sur profils et historique
