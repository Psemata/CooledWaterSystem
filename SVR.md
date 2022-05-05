# SVR - Support Vector Regression

Ce document regroupe toutes les informations et explications sur le modèle SVR - Support Vector Regression créé pour le travail pratique.
Le SVR est la variante régressive du SVM.

La valeur à prédire est la température après le passage des ventilateurs.

## Approche pour l'extraction de caractéristiques

L'extraction des caractéristiques a été fait de manière plutôt optimale pour le modèle de réseau neuronal, c'est donc la même extraction qui a été réutilisée pour ce modèle.
De plus, le remplissage de données manquantes est également le même.

## La séparation des données

Les données ont été séparées de manière assez simple, les caractéristiques d'entraînement (train features) représenteront le deux tiers (66%) des données et les caractéristiques de tests (test features) représenteront le tier restant (33%).

Ainsi, nous récupérons toutes les données présentes entre Février et Octobre pour l'entraînement et entre Octobre et fin Janvier pour les tests. Les labels sont récupérés de manière identique.

Nous voulions d'abord faire une séparation 70% - 30%, et c'est uniquement après que nous nous sommes rendus compte que séparer au mois d'Octobre représentait une séparation 66% - 33%. Cependant, comme le résultat du modèle est très bon, nous avons décidé de laisser ainsi.

## Obtention des résultats

Un pipeline qui utilise un <<StandardScaler>>, qui va permettre de normaliser nos valeurs, est d'abord créé. Ce pipeline possède les hyperparamètres [C=1.0, epsilon=0.2] En lui fournissant les valeurs séparées plus haut, nous arrivons à une valeur MSE d'environ : 0.111, ce qui n'est pas très bon.

## Performances obtenues

Afin d'obtenir de meilleures performances, une gridsearch est effectuée avec comme hyper paramètres :

- C: [1e-2, 1e-3, 1, 0.1]
- kernel: ['linear', 'rbf']
- gamma: [1e-2, 1e-3, 'auto']

Ces paramètres ont été choisis de manière un peu aléatoire. En fouillant sur la documentation de sklearn, ce sont souvent ces valeurs qui sont utilisées.

La performance qui est ressort est une valuer MSE d'environ 0.0370, ce qui est bien meilleur qu'avant.

Lors de la comparaison entre les valeurs prédites et les valeurs réelles, les graphiques sont presques superposés, ce qui indique que le modèle est très performant.

## Meilleures hyperparamètres

Les meilleurs paramètres qui sont ressortis de la gridsearch sont :

- C : 1
- gamma : 0.01
- kernel : linear

## Conclusion
