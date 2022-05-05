# Réseau neuronal

Ce document regroupe toutes les informations et explications sur le réseau neuronal implémenté pour le travail pratique.

La valeur à prédire est la température après le passage des ventilateurs.

## Exploration des caractéristiques

Pour l'exploration des caractéristiques du dataset, les différentes caractéristiques sont renommées et affichées en comparaison de celle voulue dans de multiples graphiques.
De cette manière, on aperçoit une certaine correspondance entre certaines caractéristiques comme par exemple la température avant les ventilateurs et après les ventilateurs.

Cependant, ce n'est pas parce qu'une corrélation entre quelques valeurs dans le graphe existe que les caractéristiques sont liées ! En effet, des valeurs qui possèdent une quelconque correspondance ne sont pas forcément liées, un changement dans une ne va pas obligatoirement influer sur une autre.

Enfin, une table de corrélation a été créée avec le package "Seaborn" pour montrer la corrélation entre les différentes features et voir/comprendre quelles sont les différences/ressemblances entre elles. La corrélation peut parfois être un bon indicateur sur quelle features garder lors de leur extraction.
La fonction <<Clustermap>> est utilisée pour afficher un tableau en forme de carré qui est finalement une table de valeurs indiquant la corrélation entre les différentes caractéristiques.

Grâce à celà, on peut voir et déterminer que les caractéristiques se trouvant en haut à gauche de la table sont plus susceptibles d'être représentatives et cohérentes du dataset. Plus la couleur est claire, plus la corrélation est élevée.

Finalement, une table de valeurs est créée et affichée, celle-ci donne la moyenne, la dérivée standard, la valeur minimum et bien d'autres. Cela nous permet d'avoir un apérçu rapide de la dispersion des données.

## Étude de métriques de régression

L'étude de métriques de régression a été faite en visualisant des moyennes et médianes glissantes sur des durées de 30 jours. Les caractéristiques sur lesquelles ces études ont été faites sont la température avant le passage des ventilateurs, la température après le passage des ventilateurs et la puissance des moteurs de pompes.

De cette manière on arrive à bien visualiser le comportement des différentes caractéristiques et apercevoir leur saisonnalité.

## Approche pour l'extraction de caractéristiques

Grâce à la table de corrélation créée plus haut, cinq caractéristiques ont été perçues comme très importantes pour la représentation du dataset.

On y voit que les caractéristiques :

- TBF [Temperature Before Fans [°C]]
- PBEP [Pressure Between Pumps [bar]]
- AT [Ambient Temperature [°C]]
- FS [Fan Speed [%]]

Sont plutôt bien correlées les unes avec les autres, un set de données ne possédant que ces caractéristiques a alors été créé.

Cependant, les données reçues au début de projet ont un léger problème : il manque des informations durant le mois de mai !

L'idée est donc de combler ce trou via un remplissage utilisant un calcul de moyenne sur les données passées. Les échantillons utilisés pour ce remplissage sont bien entendu pris toutes les 30 minutes.

## La séparation des données

Nous avons séparé le dataset en trois :

- Entrainement (8 mois - de février à octobre 2021)
- Validation (2 mois - de octobre à décembre 2021)
- Test (2 mois - de décembre 2021 à février 2022)

Vu que nous travaillons avec des séries temporelles, il est primordial de ne surtout pas mélanger les données et de garder une cohérence chronologique.

De plus, nous avons appliqué un shift contre le haut d'une ligne pour les labels. En effet, vu que nous devons prédire la valeur après ventilateur 30 minutes dans le futur, nous devons faire correspondre les données au label 30 minutes plus tard.

## Obtention des résultats

Le framework Keras permet facilement d'obtenir l'historique d'entrainement des modèles créés. C'est grâce à cela que nous pouvons afficher les courbes de loss d'entrainement et de validation et ainsi observer que le modèle apprend correctement. À noter que nous trouvons spécial que la loss de validation est inférieure à celle d'entrainement lors des premières époques. Under fitting ou modèle trop simple ? C'est assez difficile à déterminer.

De plus, nous évaluons les performances du modèle sur le dataset de test qu'il n'a jamais vu, nous observons qu'il obtient une mse de 0.0448, ce qui montre bien que le modèle a appris et arrive à prédire des valeurs sur des données inconnues.

## Performances obtenues

Une fois le modèle entrainé, les performances obtenues au bout de 10 epochs sont les suivantes :

- loss : 0.1064
- mse : 0.1064
- val_loss : 0.0445
- val_mse : 0.0445

Lors de l'évaluation du modèle, une loss et une mse de 0.0422 ont été calculées.

## Meilleures hyperparamètres

Plusieurs tests d'ajouts de couches ou de changement de nombre de nodes ont été faits.
Le meilleur résultat trouvé a été un modèle à trois couches avec 16 nodes d'entrées, 8 de transition et 1 node de fin.
L'activation des deux premières couches est de type "relu" --> "Rectified Linear Unit"

## Conclusion

En conclusion, le modèle utilisé pour le réseau neuronal est plutôt performant, avec une valeur de loss très petite, il permet de prédire de manière assez correcte la valeur de la température après le passage de ventilateurs.
Lorsque l'on compare les deux graphiques, celui des valeurs prédites et celui des valeurs réelles, on voit que les pics sont bien trouvés et bien qu'un peu bruitées, les autres valeurs sont justes.
