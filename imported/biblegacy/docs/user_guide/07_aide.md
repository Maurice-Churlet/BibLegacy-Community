# 07 - Aide et FAQ

## Avant de conclure qu'il y a un probleme
Dans beaucoup de cas, le comportement observe vient surtout du choix de profil ou d'options.

Ordre conseille :

1. testez d'abord **Express** seul,
2. si trop d'images restent sans dossard, activez **Fallback**,
3. si la couverture prime clairement sur la vitesse, testez **TrOCR**,
4. si besoin, comparez plusieurs executions dans **Stats Production** ou avec un test comparatif.

## Mon dossard n'est pas detecte
Ca peut venir de plusieurs causes :

- image floue ou fortement bougee,
- dossard trop petit dans l'image,
- contraste insuffisant,
- reflet ou pli qui coupe la lecture,
- dossard partiellement cache.

Que faire dans l'ordre :

1. relancer avec **Fallback**,
2. si l'echec persiste, tester **Fallback renforce par TrOCR**,
3. si le lot est globalement difficile, tester **TrOCR**,
4. si le probleme est recurrent sur un meme type de photos, utiliser un profil plus robuste ou passer par un calibrage.

## L'application est plus lente que prevu
La cause la plus frequente est l'activation d'options plus couteuses.

Les plus impactantes sont :

- **TrOCR** sur tout le lot,
- **Fallback** sur des images qui echouent souvent,
- **Fallback renforce par TrOCR** sur des lots tres difficiles,
- certains reglages avances trop agressifs.

Bon reflexe :

1. verifier si **TrOCR** est actif,
2. regarder dans `production.log` ou `maintenance_trace.log` si des consensus TrOCR ou des fallback se declenchent souvent,
3. revenir temporairement a **Express** seul pour mesurer la base de vitesse,
4. ne modifier les reglages avances qu'avec un objectif precis.

## Je ne sais pas quel profil choisir
Resume pratique :

- **Express** : choix par defaut recommande,
- **Standard** : compromis un peu plus robuste,
- **Deep** : utile pour essais et cas plus difficiles,
- **Smart** : reserve aux usages verifies et aux phases d'optimisation.

Si vous hesitez, commencez par **Express** puis ajoutez seulement ce qui manque.

## La documentation integree semble incomplete
L'onglet **Documentation** lit les fichiers du dossier `docs/user_guide/`.

Si une section parait incomplete ou obsolete :

- comparez avec les onglets reels de l'application,
- consultez aussi les rapports et les logs,
- signalez la page concernee pour mise a jour.

## Je veux repartir d'une base propre pour des tests
Utilisez les fonctions adaptees plutot que de supprimer des fichiers au hasard :

- **Purger logs/CSV** pour vider les traces du dossier `logs/`,
- **Effacer sortie prod** pour nettoyer les sorties generees avant une nouvelle production,
- les rapports Markdown restent separes dans `rapports/`.

## Une option est grisee pendant une action
C'est normal.

Pendant une production ou un traitement sensible, certaines options sont temporairement verrouillees pour eviter de modifier la configuration en cours d'execution.

Attendez la fin de l'action avant de changer :

- le profil,
- Fallback,
- TrOCR,
- certains reglages lies au traitement.

## Je veux aider a diagnostiquer un incident
La meilleure methode est de fournir des traces propres et ciblees :

1. reproduire le probleme une fois,
2. relever le contexte exact de l'action,
3. joindre `production.log`,
4. ajouter `maintenance_trace.log` si le mode Maintenance etait actif,
5. ajouter le rapport Markdown genere si le sujet concerne une production ou un comparatif.

## Support
Pour une aide technique utile, transmettez toujours :

- ce que vous etiez en train de faire,
- le profil choisi,
- les options actives,
- l'heure approximative de l'evenement,
- les logs ou rapports associes.

Sans ces elements, le diagnostic est souvent imprecis.
