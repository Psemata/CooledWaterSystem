# DTR - Decisional tree regressor

Ce document regroupe toutes les informations et explication concernant le modèle Decisional Tree Regressor.
La variante régressive du Decisional tree.

## Approche pour l'extraction de caractéristiques

Ayant déjà effectuée une extraction pour le NeuralNetwork, le groupe décide de garder les mêmes caractéristiques pour le Decisional Tree Regressor.

De cette façon, les différentes caractériques gardées sont :

- TBF [Temperature Before Fans [°C]]
- PBEP [Pressure Between Pumps [bar]]
- AT [Ambient Temperature [°C]]
- FS [Fan Speed [%]]

## La séparation des données

La séparation des données à été faite d'une manière assez simple. Les deux tiers des données sont utilisées pour l'entrainement tandis que le tier restant représente les caractéristiques de test.

Donc de Février à Octobre ce sont des données d'entrainement et celles d'Octobre à Fin Janvier sont allouées aux tests.

## Obtention des résultats

Une pipeline qui utilise un <<StandardScalar>>, qui va permettre de normaliser nos valeurs est créée. Dans cette pipeline se trouve également le DecisionTreeRegressor avec l'hyperparamètre [random_state=0]. De cette façon, la pipeline retourne avec une MSE d'environ 0.114.

## Performances obtenues

Afin d'avoir les meilleures perfomances possibles, un grid-search est mis en place avec les hyperparamètres suivants :

- splitter : ['best', 'random']
- criterion : ['squared_error', 'friedman_mse']
- max_depth : [None, 5, 10]
- min_samples_split : [2, 5, 10]

En effectuant le grid-search avec ces paramètres et un nombre de cross-validation de 3, nous tombons sur une MSE de 0.037 ce qui est significativement meilleur.

Ces paramètres ont été choisis d'une façon un peu aléatoire. En se renseignant sur internet via les documentations et des forums, ces valeurs sont celles qui sont le plus ressorties. Etant donné que ces valeurs se basent plus sur l'expérience que d'une réelle logique derrière, le groupe a décidé de rester avec ces paramètres là.

## Meilleures hyperparamètres

Les meilleurs paramètres qui sont ressortis du grid-search sont :

- criterion : friedman_mse
- max_depth : 10
- min_samples_split : 5
- splitter : random

## Conclusion

En conclusion, le Decisional Tree Regressor est performant, sa valeur de MSE est d'environ 0.114, lors de la superposition des graphes, on voit une ressemblance entre les prédictions et la réalité.
