---
keywords: Experience Platform;optimiser;modèle;Workspace de science des données;rubriques populaires;informations sur le modèle
solution: Experience Platform
title: Optimiser un modèle à l’aide du framework Model Insights
type: Tutorial
description: Le framework d’informations sur les modèles fournit aux spécialistes des données des outils dans la Workspace de science des données pour faire des choix rapides et éclairés afin d’optimiser les modèles de machine learning basés sur les expériences.
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 78%

---

# Optimiser un modèle à l’aide du framework Model Insights

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Le framework d’informations sur les modèles fournit aux spécialistes des données des outils [!DNL Data Science Workspace] de faire des choix rapides et éclairés pour des modèles de machine learning optimaux basés sur des expériences. Le framework améliorera la vitesse et l’efficacité du processus de machine learning et la facilité d’utilisation pour les analystes de données. Pour ce faire, un modèle par défaut est fourni pour chaque type d’algorithme de machine learning afin de faciliter le réglage des modèles. Le résultat final permet aux analystes de données et aux analystes de données citoyens de prendre de meilleures décisions d’optimisation des modèles pour leurs clients finaux.

## Que sont les mesures ?

Après la mise en œuvre et la formation d’un modèle, l’étape suivante pour un analyste de données consiste à déterminer les performances du modèle. Diverses mesures sont utilisées pour comparer l’efficacité d’un modèle par rapport aux autres. Voici quelques exemples de mesures utilisées :

- Précision de la classification
- Aire sous la courbe
- Matrice de confusion
- Rapport de classification

## Configuration du code de recette

Actuellement, Model Insights Framework prend en charge les exécutions suivantes :

- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

Vous trouverez un exemple de code pour les recettes dans le référentiel [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) sous `recipes`. Des fichiers spécifiques de ce référentiel seront référencés dans ce tutoriel.

### Scala {#scala}

Il existe deux façons d’intégrer des mesures aux recettes. L’une consiste à utiliser les mesures d’évaluation par défaut fournies par le SDK, l’autre consiste à créer des mesures d’évaluation personnalisées.

#### Mesures d’évaluation par défaut pour Scala

Les évaluations par défaut sont calculées dans le cadre des algorithmes de classification. Voici quelques valeurs par défaut pour les évaluateurs actuellement mis en œuvre :

| Classe d’évaluateur | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

L’évaluateur peut être défini dans la recette du fichier [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) du dossier `recipe`. Un exemple de code permettant d’activer le `DefaultBinaryClassificationEvaluator` est illustré ci-dessous :

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Une fois qu’une classe d’évaluateur est activée, un certain nombre de mesures sont calculées par défaut pendant la formation. Les mesures par défaut peuvent être déclarées explicitement en ajoutant la ligne suivante à `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Si la mesure n’est pas définie, les mesures par défaut seront actives.

Une mesure spécifique peut être activée en modifiant la valeur de `evaluation.metrics.com`. Dans l’exemple suivant, la mesure F-Score est activée.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

Le tableau suivant indique les mesures par défaut pour chaque classe. Un utilisateur peut également utiliser les valeurs de la colonne `evaluation.metric` pour activer une mesure spécifique.

| `evaluator.class` | Mesures par défaut | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` | -Précision <br>-Rappel <br>-Matrice de confusion <br>-F-Score <br>-Exactitude <br>-Caractéristiques de fonctionnement du récepteur <br>-Aire sous les caractéristiques de fonctionnement du récepteur | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Précision <br>-Rappel <br>-Matrice de confusion <br>-F-Score <br>-Exactitude <br>-Caractéristiques de fonctionnement du récepteur <br>-Aire sous les caractéristiques de fonctionnement du récepteur | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Précision moyenne (MAP) <br>-Gain cumulatif actualisé normalisé <br>-Rang réciproque moyen <br>-Mesure K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Mesures d’évaluation personnalisées pour Scala

L’évaluateur personnalisé peut être fourni en étendant l’interface de `MLEvaluator.scala` dans votre fichier `Evaluator.scala`. Dans l’exemple de fichier [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala), nous définissons des fonctions `split()` et `evaluate()` personnalisées. Notre fonction `split()` divise nos données de manière aléatoire avec un ratio de 8:2 et notre fonction `evaluate()` définit et renvoie 3 mesures : MAPE, MAE et RMSE.

>[!IMPORTANT]
>
>Pour la classe de `MLMetric`, n’utilisez pas `"measures"` comme `valueType` lors de la création d’une `MLMetric`, sinon la mesure ne sera pas renseignée dans le tableau des mesures d’évaluation personnalisées.
>  
> À faire : `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> À ne pas faire : `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Une fois définie dans la recette, l’étape suivante consiste à l’activer dans les recettes. Cette opération est effectuée dans le fichier [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) du dossier `resources` du projet. Ici, la `evaluation.class` est définie sur la classe `Evaluator` définie dans `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

Dans l’[!DNL Data Science Workspace], l’utilisateur pourrait voir les informations sous l’onglet « Mesures d’évaluation » de la page de l’expérience.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Pour l’instant, il n’existe aucune mesure d’évaluation par défaut pour [!DNL Python] ou [!DNL Tensorflow]. Ainsi, pour obtenir les mesures d’évaluation de [!DNL Python] ou [!DNL Tensorflow], vous devez créer une mesure d’évaluation personnalisée. Pour ce faire, mettez en œuvre la classe `Evaluator`.

#### Mesures d’évaluation personnalisées pour [!DNL Python]

Pour les mesures d’évaluation personnalisées, deux méthodes principales doivent être mises en œuvre pour l’évaluateur : `split()` et `evaluate()`.

Par [!DNL Python], ces méthodes sont définies dans [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) pour la classe `Evaluator`. Suivez le lien [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) pour obtenir un exemple de l’`Evaluator`.

La création de mesures d’évaluation dans [!DNL Python] nécessite que l’utilisateur mette en œuvre les méthodes `evaluate()` et `split()`.

La méthode `evaluate()` renvoie l’objet de mesure qui contient un tableau d’objets de mesure avec les propriétés `name`, `value` et `valueType`.

L’objectif de la méthode `split()` est de saisir des données et de produire un jeu de données de formation et de test. Dans notre exemple, la méthode `split()` saisit les données à l’aide du SDK `DataSetReader`, puis nettoie les données en supprimant les colonnes non liées. Ensuite, des fonctionnalités supplémentaires sont créées à partir des fonctionnalités brutes existantes dans les données.

La méthode `split()` doit renvoyer un cadre de données de formation et de test qui est ensuite utilisé par les méthodes `pipeline()` pour former et tester le modèle ML.

#### Mesures d’évaluation personnalisées pour Tensorflow

Par [!DNL Tensorflow], comme pour [!DNL Python], les méthodes `evaluate()` et `split()` de la classe `Evaluator` doivent être implémentées. Les mesures doivent être renvoyées pour `evaluate()`, tandis que `split()` renvoie les jeux de données de formation et de test.

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

Pour le moment, aucune mesure d’évaluation par défaut n’existe pour R. Par conséquent, vous devrez définir la classe `applicationEvaluator` dans le cadre de la recette afin d’obtenir les mesures d’évaluation pour R.

#### Mesures d’évaluation personnalisées pour R

L’objectif principal de `applicationEvaluator` consiste à renvoyer un objet JSON contenant des paires clé-valeur de mesures.

[applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) peut servir d’exemple. Dans cet exemple, `applicationEvaluator` est divisé en trois sections courantes :

- Chargement des données
- Préparation des données/conception des fonctionnalités
- Récupération du modèle enregistré et évaluation

Les données sont d’abord chargées dans un jeu de données à partir d’une source, comme défini dans [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). Ensuite, les données sont nettoyées et conçues pour s’adapter au modèle de machine learning. Enfin, le modèle est utilisé pour effectuer une prévision à l’aide du jeu de données et des mesures sont calculées à partir des valeurs prédites et des valeurs réelles. Dans ce cas, MAPE, MAE et RMSE sont définis et renvoyés dans l’objet `metrics`.

## Utilisation de mesures préconfigurées et de graphiques de visualisation

Le [!DNL Sensei Model Insights Framework] prend en charge un modèle par défaut pour chaque type d’algorithme de machine learning. Le tableau ci-dessous présente les classes d’algorithme de machine learning de haut niveau courantes et les mesures d’évaluation et visualisations correspondantes.

| Type d’algorithme de ML | Mesures d’évaluation | Visualisations |
| --- | --- | --- |
| Régression | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Courbe de recouvrement des valeurs prédites et réelles |
| Classification binaire | - Matrice de confusion<br>- Précision-rappel<br>- Exactitude<br>- F-score (en particulier F1 et F2)<br>- AUC<br>- ROC | Courbe ROC et matrice de confusion |
| Classification multi-classe | -Matrice de confusion <br>- Pour chaque classe : <br>- précision-rappel exactitude <br>- F-score (en particulier F1 et F2) | Courbe ROC et matrice de confusion |
| Clustering (avec réalité de terrain) | - NMI (note d’information mutuelle normalisée), AMI (note d’information mutuelle ajustée)<br>- RI (indice de Rand), ARI (indice de Rand ajusté)<br>- note d’homogénéité, note d’exhaustivité et V-measure<br>- FMI (indice Fowlkes-Mallows)<br>- Pureté<br>- Indice de Jaccard | Graphique de clusters illustrant les clusters et les centres de gravité dont les tailles de cluster relatives reflètent les points de données appartenant au cluster |
| Clustering (sans réalité de terrain) | - Inertie<br>- Coefficient de silhouette<br>- CHI (indice de Calinski-Harabaz)<br>- DBI (indice de Davies-Bouldin)<br>- Indice de Dunn | Graphique de clusters illustrant les clusters et les centres de gravité dont les tailles de cluster relatives reflètent les points de données appartenant au cluster |
| Recommandation | -Précision moyenne (MAP) <br>-Gain cumulatif actualisé normalisé <br>-Rang réciproque moyen <br>-Mesure K | À déterminer |
| Cas d’utilisation de TensorFlow | TensorFlow Model Analysis (TFMA) | Comparaison/visualisation des modèles de réseaux neuronaux de Deepcompare |
| Autre/Mécanisme de capture d’erreur | Logique de mesure personnalisée (et graphiques d’évaluation correspondants) définie par l’auteur du modèle. Gestion des erreurs élégante en cas de non-correspondance de modèle | Tableau avec des paires clé-valeur pour les mesures d’évaluation |
