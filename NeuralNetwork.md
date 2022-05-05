# Réseau neuronal

Ce document regroupe toutes les informations et explications sur le réseau neuronal implémenté pour le travail pratique.

La valeur à prédire est la température après le passage des ventilateurs.

## Exploration des caractéristiques

Pour l'exploration des caractéristiques du dataset, les différentes caractéristiques sont renommées et affichées en comparaison de celle voulue dans de multiples graphiques.
De cette manière, on aperçoit une certaine correspondance entre certaines caractéristiques comme par exemple la température avant les ventilateurs et après les ventilateurs.

Cependant, ce n'est pas parce qu'une corrélation entre quelques valeurs dans le graphe existe que les caractéristiques sont liées ! En effet, des valeurs qui possèdent une quelconque correspondance ne sont pas forcément liées, un changement dans une ne va pas obligatoirement influer sur une autre.

Enfin, une table de corrélation a été créée avec le package "Seaborn" pour montrer précisément quelles sont les caractéristiques importantes à la température après le passage des ventilateurs.
La fonction <<Clustermap>> est utilisée pour afficher un tableau en forme de carré qui est finalement une table de valeurs indiquant la corrélation entre les différentes caractéristiques.

Grâce à celà, on peut voir et déterminer que les caractéristiques se trouvant en haut à gauche de la table sont importantes par rapport à la caractéristiques recherchées : la température de l'eau après le passage des ventilateurs. Plus la couleur est claire, plus la corrélation est élevée.

Finalement, une table de valeurs est créée et affichée, celle-ci donne la moyenne, la dérivée standard, la valeur minimum et bien d'autres.

## Étude de métriques de régression

L'étude de métriques de régression a été faite en visualisant des moyennes et médianes glissantes sur des durées de 30 jours. Les caractéristiques sur lesquelles ces études ont été faites sont la température avant le passage des ventilateurs, la température après le passage des ventilateurs et la puissance des moteurs de pompes.

De cette manière on arrive à bien visualiser le comportement des différentes caractéristiques.

## Approche pour l'extraction de caractéristiques

Grâce à la table de corrélation créée plus haut, cinq caractéristiques ont été perçues comme très importantes pour la température après le passage des ventilateurs.

On y voit que les caractéristiques :

- TBF [Temperature Before Fans [°C]]
- PBEP [Pressure Between Pumps [bar]]
- AT [Ambient Temperature [°C]]
- FS [Fan Speed [%]]

Possèdent une certaine influence sur TAF [Temperature After Fans [°C]]. Un set de données ne possédant que ces caractéristiques a été créé.

Cependant, les données reçues au début de projet ont un léger problème : il manque des informations durant le mois de mai !

L'idée est donc de combler ce trou via un remplissage utilisant un calcul de moyenne. Les échantillons utilisés pour ce remplissage sont bien entendu pris toutes les 30 minutes.

## La séparation des données

## Obtention des résultats

## Performances obtenues

Une fois le modèle entrainé, les performances obtenues au bout de 10 epochs sont les suivantes :

- loss : 0.1064
- mse : 0.1064
- val_loss : 0.0445
- val_mse : 0.0445

Lors de l'évaluation du modèle, une loss et une mse de 0.0422 ont été calculées.

## Meilleures hyperparamètres

Quant aux hyperparamètres, aucune gridsearch n'a été faite car les deux étudiants ne savaient pas comment l'effectuer sur un réseau neuronal. Cependant, plusieurs tests d'ajouts de couches ou de changement de nombre de nodes ont été faits.
Le meilleur résultat trouvé a été un modèle à trois couches avec 16 nodes d'entrées, 8 de transition et 1 node de fin.
L'activation des deux premières couches est de type "relu" --> "Rectified Linear Unit"

## Conclusion

En conclusion
