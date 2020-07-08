---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: Optimiser un modèle
topic: Tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---


# Optimisation d&#39;un modèle à l&#39;aide de la structure Model Insights

Le Cadre d&#39;analyse de modèle fournit aux chercheurs en données des outils leur permettant [!DNL Data Science Workspace] de faire des choix rapides et éclairés pour des modèles d&#39;apprentissage automatique optimaux basés sur des expériences. Le cadre améliorera la vitesse et l&#39;efficacité du processus d&#39;apprentissage automatique et améliorera la facilité d&#39;utilisation pour les chercheurs en données. Pour ce faire, vous fournissez un modèle par défaut pour chaque type d’algorithme d’apprentissage automatique afin de faciliter le réglage des modèles. Le résultat final permet aux spécialistes des données et aux scientifiques des données citoyens de prendre de meilleures décisions d&#39;optimisation des modèles pour leurs clients finaux.

## Que sont les mesures ?

Après la mise en oeuvre et la formation d&#39;un modèle, l&#39;étape suivante d&#39;un informaticien consiste à déterminer les performances du modèle. Diverses mesures sont utilisées pour déterminer l’efficacité d’un modèle par rapport à d’autres. Voici quelques exemples de mesures utilisées :
- Précision de la classification
- Zone sous la courbe
- Matrice de confusion
- Rapport de classification

## Configuration du code de recette

Actuellement, Model Insights Framework prend en charge les runtimes suivants :
- [Scala](#scala)
- [!DNL Python/Tensorflow](#pythontensorflow)
- [r](#r)

Vous trouverez un exemple de code pour les recettes dans le référentiel de référence [](https://github.com/adobe/experience-platform-dsw-reference) experience-platform-dsw sous `recipes`. Des fichiers spécifiques de ce référentiel seront référencés tout au long de ce didacticiel.

### Scala {#scala}

Il existe deux façons d&#39;intégrer des mesures aux recettes. L’une consiste à utiliser les mesures d’évaluation par défaut fournies par le SDK et l’autre consiste à créer des mesures d’évaluation personnalisées.

#### Mesures d’évaluation par défaut pour Scala

Les évaluations par défaut sont calculées dans le cadre des algorithmes de classification. Voici quelques valeurs par défaut pour les évaluateurs actuellement implémentés :

| Classe d’évaluateur | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

L’évaluateur peut être défini dans la recette du fichier [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) situé dans le `recipe` dossier. L&#39;exemple de code permettant d&#39;activer le `DefaultBinaryClassificationEvaluator` logiciel est illustré ci-dessous :

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Une fois qu’une classe d’évaluateur est activée, un certain nombre de mesures sont calculées par défaut pendant la formation. Les mesures par défaut peuvent être déclarées explicitement en ajoutant la ligne suivante à votre `application.properties`rapport.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>Si la mesure n&#39;est pas définie, les mesures par défaut sont actives.

Une mesure spécifique peut être activée en modifiant la valeur de `evaluation.metrics.com`. Dans l’exemple suivant, la mesure Note F est activée.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

Le tableau suivant indique les mesures par défaut pour chaque classe. Un utilisateur peut également utiliser les valeurs de la `evaluation.metric` colonne pour activer une mesure spécifique.

| `evaluator.class` | Mesures par défaut | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Matrice de précision <br>- <br>de rappel-confusion <br>F-Score <br>-Précision des caractéristiques d&#39;exploitation <br>du récepteur <br>-Zone sous les caractéristiques d&#39;exploitation du récepteur | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Matrice de précision <br>- <br>de rappel-confusion <br>F-Score <br>-Précision des caractéristiques d&#39;exploitation <br>du récepteur <br>-Zone sous les caractéristiques d&#39;exploitation du récepteur | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Précision moyenne <br>normalisée (MAP) Gain cumulé cumulé <br>moyen Ordre de classement <br>métrique réciproque K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Mesures d’évaluation personnalisées pour Scala

L’évaluateur personnalisé peut être fourni en étendant l’interface de `MLEvaluator.scala` dans votre `Evaluator.scala` fichier. Dans l’exemple de fichier [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) , nous définissons des fonctions personnalisées `split()` et `evaluate()` des fonctions. Notre `split()` fonction divise nos données de manière aléatoire avec un rapport de 8:2 et notre `evaluate()` fonction définit et renvoie 3 mesures : MAPE, MAE et RMSE.

>[!IMPORTANT]
>
>Pour la `MLMetric` classe, n’utilisez pas `"measures"` pour `valueType` lors de la création d’une autre `MLMetric` mesure que la mesure ne sera pas renseignée dans le tableau des mesures d’évaluation personnalisées.
>  
> Procédez comme suit : `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Pas ceci : `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Une fois définie dans la recette, l&#39;étape suivante consiste à l&#39;activer dans les recettes. Cette opération est effectuée dans le fichier [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) du `resources` dossier du projet. Ici, la `evaluation.class` classe est définie sur la `Evaluator` classe définie dans `Evaluator.scala`

```properties
evaluation.class=com.adobe.platform.ml.Evaluator
```

Dans la [!DNL Data Science Workspace]boîte de dialogue, l’utilisateur peut voir les informations de l’onglet &quot;Mesures d’évaluation&quot; de la page de l’expérience.

### [!DNL Python/Tensorflow] {#pythontensorflow}

Pour l’instant, il n’existe aucune mesure d’évaluation par défaut pour [!DNL Python] ou [!DNL Tensorflow]. Par conséquent, pour obtenir les mesures d’évaluation pour [!DNL Python] ou [!DNL Tensorflow], vous devez créer une mesure d’évaluation personnalisée. Cela peut être fait en implémentant la `Evaluator` classe.

#### Mesures d’évaluation personnalisées pour [!DNL Python]

Pour les mesures d’évaluation personnalisées, deux méthodes principales doivent être implémentées pour l’évaluateur : `split()` et `evaluate()`.

Par exemple, [!DNL Python]ces méthodes seraient définies dans [évaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) pour la `Evaluator` classe. Suivez le lien [évaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) pour obtenir un exemple du `Evaluator`.

La création de mesures d’évaluation dans [!DNL Python] exige que l’utilisateur mette en oeuvre les `evaluate()` et `split()` méthodes.

La `evaluate()` méthode renvoie l’objet metric qui contient un tableau d’objets metric avec les propriétés de `name`, `value`et `valueType`.

La `split()` méthode a pour but de saisir des données et de produire une formation et un ensemble de données de test. Dans notre exemple, la `split()` méthode saisit les données à l’aide du `DataSetReader` SDK, puis nettoie les données en supprimant les colonnes non liées. De là, d’autres fonctions sont créées à partir des fonctions brutes existantes dans les données.

La `split()` méthode doit renvoyer une base de données de formation et de test qui est ensuite utilisée par les `pipeline()` méthodes pour former et tester le modèle ML.

#### Mesures d’évaluation personnalisées pour Tensorflow

Car [!DNL Tensorflow], comme [!DNL Python], les méthodes `evaluate()` et `split()` dans la `Evaluator` classe devront être implémentées. Par exemple, `evaluate()`les mesures doivent être renvoyées pendant `split()` le retour des ensembles de données de train et d&#39;essai.

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

### r {#r}

À ce jour, il n&#39;existe aucune mesure d&#39;évaluation par défaut pour R. Par conséquent, pour obtenir les mesures d&#39;évaluation pour R, vous devez définir la `applicationEvaluator` classe dans le cadre de la recette.

#### Mesures d’évaluation personnalisées pour R

L’objectif principal de cette méthode `applicationEvaluator` est de renvoyer un objet JSON contenant des paires clé-valeur de mesures.

Ce fichier [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) peut être utilisé comme exemple. Dans cet exemple, la section `applicationEvaluator` est divisée en trois sections courantes :
- Charger les données
- Préparation des données/ingénierie des fonctionnalités
- Récupérer le modèle enregistré et évaluer

Les données sont tout d’abord chargées dans un jeu de données à partir d’une source, comme défini dans [commerce.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). À partir de là, les données sont nettoyées et conçues pour s&#39;adapter au modèle d&#39;apprentissage automatique. Enfin, le modèle est utilisé pour faire une prédiction en utilisant notre jeu de données et à partir des valeurs prédites et des valeurs réelles, les mesures sont calculées. Dans ce cas, MAPE, MAE et RMSE sont définis et renvoyés dans l’ `metrics` objet.

## Utilisation de mesures prédéfinies et de graphiques de visualisation

Il [!DNL Sensei Model Insights Framework] prend en charge un modèle par défaut pour chaque type d’algorithme d’apprentissage automatique. Le tableau ci-dessous présente les classes d’algorithmes d’apprentissage automatique de haut niveau courantes ainsi que les mesures d’évaluation et visualisations correspondantes.

| Type d&#39;algorithme XML | Mesures d’évaluation | Visualisations |
--- | --- | ---
| Régression | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Courbe d’incrustation des valeurs prédites et réelles |
| Classification binaire | - Matrice<br>de confusion - Rappel<br>de précision - Précision<br>- Note F (spécifiquement F1, F2)<br>- AUC<br>- ROC | Courbe ROC et matrice de confusion |
| Classification à plusieurs classes | -Matrice de confusion <br>- Pour chaque classe : <br>- précision du rappel de précision <br>- score F (spécifiquement F1, F2) | Courbe ROC et matrice de confusion |
| Mise en grappe (avec vérité au sol) | - NMI (note d&#39;information mutuelle normalisée), AMI (note d&#39;information mutuelle ajustée)<br>- RI (indice Rand), ARI (indice Rand ajusté)<br>- score d&#39;homogénéité, score d&#39;exhaustivité et mesure<br>V- FMI (indice Fowlkes-Mallow)<br>- Indice de pureté<br>- Jaccard | Graphique en grappes montrant les grappes et les centroïdes avec des tailles de grappe relatives reflétant les points de données appartenant à une grappe |
| Mise en grappe (sans vérité au sol) | - Inertia<br>- Coefficient<br>de silhouette- CHI (indice Calinski-Harabaz)<br>- DBI (indice Davies-Bouldin)<br>- Indice Dunn | Graphique en grappes montrant les grappes et les centroïdes avec des tailles de grappe relatives reflétant les points de données appartenant à une grappe |
| Recommandation | -Précision moyenne <br>normalisée (MAP) Gain cumulé cumulé <br>moyen Ordre de classement <br>métrique réciproque K | À déterminer |
| Cas d’utilisation de TensorFlow | Analyse de modèle TensorFlow (TFMA) | Comparaison approfondie des modèles de réseau neuronal et de la visualisation |
| Autre mécanisme de capture d&#39;erreur | Logique de mesure personnalisée (et graphiques d’évaluation correspondants) définie par l’auteur du modèle. Gestion des erreurs gracieuses en cas de non-correspondance de modèle | Tableau avec des paires clé-valeur pour les mesures d’évaluation |
