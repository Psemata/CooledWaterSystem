# SVR - Support Vector Regression

Ce document regroupe toutes les informations et explications sur le modèle SVR - Support Vector Regression créé pour le travail pratique.
Le SVR est la variante régressive du SVM.

La valeur à prédire est la température après le passage des ventilateurs.

## Approche pour l'extraction de caractéristiques

L'extraction des caractéristiques a été faite de manière plutôt optimale pour le modèle de réseau neuronal, c'est donc la même extraction qui a été réutilisée pour ce modèle.
De plus, le remplissage de données manquantes est également le même.

## La séparation des données

Les données ont été séparées de manière assez simple, les caractéristiques d'entraînement (train features) représenteront le deux tiers (66%) des données et les caractéristiques de tests (test features) représenteront le tier restant (33%).

Ainsi, nous récupérons toutes les données présentes entre Février et Octobre pour l'entraînement et entre Octobre et fin Janvier pour les tests. Les labels sont récupérés de manière identique.

Nous ne faisons pas de dataset de validation car nous souhaitons laisser le grid-search se charger de faire la séparation. Pour tester une première performance de la baseline, nous n'avons pas souhaité faire de validation vu que nous allions le faire avec le grid-search.

## Obtention des résultats

Un pipeline qui utilise un <<StandardScaler>>, qui va permettre de normaliser nos valeurs, est d'abord créé. Ce pipeline possède les hyperparamètres [C=1.0, epsilon=0.2] En lui fournissant les valeurs séparées plus haut, nous arrivons à une valeur MSE d'environ : 0.111, ce qui est acceptable mais nous pensons pouvoir faire mieux.

## Performances obtenues

Afin d'obtenir de meilleures performances, un grid-search est effectué avec comme hyper paramètres :

- C: [1e-2, 1e-3, 1, 0.1]
- kernel: ['linear', 'rbf']
- gamma: [1e-2, 1e-3, 'auto']

Ces paramètres ont été choisis de manière heuristique. En fouillant sur la documentation de sklearn, ce sont souvent ces valeurs qui sont utilisées.

La performance qui en ressort est une valeur MSE d'environ 0.0370, ce qui est bien meilleur qu'avant.

Lors de la comparaison entre les valeurs prédites et les valeurs réelles, les graphiques sont presques superposés, ce qui indique que le modèle est très performant.

## Meilleures hyperparamètres

Les meilleurs paramètres qui sont ressortis du grid-search sont :

- C : 1
- gamma : 0.01
- kernel : linear

## Conclusion

En conclusion, le SVR employé est performant, sa valeur MSE est de 0.0370 et lors de la superposition des graphes on voit clairement une ressemblance entre les prédictions et la réalité.
