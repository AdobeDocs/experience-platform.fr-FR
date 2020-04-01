---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: Optimisation d’un modèle
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Optimisation d’un modèle


Ce didacticiel décrit :

- Configuration du code de recette
- Définition de mesures personnalisées
- Utilisation de mesures d’évaluation prédéfinies et de graphiques de visualisation

D’ici la fin de ce didacticiel, vous devriez être en mesure de configurer le code de recette, de définir des mesures personnalisées, d’utiliser des mesures d’évaluation prédéfinies et des graphiques de visualisation par défaut.

## Que sont les mesures ?

Après la mise en oeuvre et la formation d&#39;un modèle, l&#39;étape suivante d&#39;un chercheur de données consiste à déterminer les performances du modèle. Diverses mesures sont utilisées pour déterminer l’efficacité d’un modèle par rapport à d’autres. Voici quelques exemples de mesures utilisées :
- Précision de la classification
- Zone sous la courbe
- Matrice de confusion
- Rapport de classification

## Qu&#39;est-ce que le modèle de cadre d&#39;information?

Le modèle de structure d’informations fournit aux chercheurs en données des outils dans Data Science Workspace pour faire des choix rapides et éclairés pour des modèles optimaux d’apprentissage automatique fondés sur des expériences. Le cadre améliorera la vitesse et l’efficacité du processus d’apprentissage automatique et la facilité d’utilisation pour les chercheurs en données. Pour ce faire, vous fournissez un modèle par défaut pour chaque type d’algorithme d’apprentissage automatique afin de faciliter le réglage des modèles. Le résultat final permet aux spécialistes des données et aux scientifiques des données citoyens de prendre de meilleures décisions d&#39;optimisation des modèles pour leurs clients finaux.

## Configuration du code de recette

Actuellement, Model Insights Framework prend en charge les moteurs d’exécution suivants :
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [r](#r)

Vous trouverez un exemple de code pour les recettes dans le référentiel [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) sous `recipes`. Des fichiers spécifiques de ce référentiel seront référencés dans ce didacticiel.

### Scala {#scala}

Il existe deux façons d&#39;intégrer des mesures aux recettes. L’une consiste à utiliser les mesures d’évaluation par défaut fournies par le SDK, l’autre consiste à créer des mesures d’évaluation personnalisées.

#### Mesures d’évaluation par défaut pour Scala

Les évaluations par défaut sont calculées dans le cadre des algorithmes de classification. Voici quelques valeurs par défaut pour les évaluateurs actuellement implémentés :

| Classe d’évaluateur | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

L’évaluateur peut être défini dans la recette du fichier [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) du `recipe` dossier. L’exemple de code permettant d’activer le `DefaultBinaryClassificationEvaluator` logiciel est illustré ci-dessous :

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

Une fois qu’une classe d’évaluateur est activée, un certain nombre de mesures sont calculées par défaut pendant la formation. Les mesures par défaut peuvent être déclarées explicitement en ajoutant la ligne suivante à votre `application.properties`formulaire.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE] Si la mesure n’est pas définie, les mesures par défaut sont actives.

Une mesure spécifique peut être activée en modifiant la valeur de `evaluation.metrics.com`. Dans l’exemple suivant, la mesure Note F est activée.

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

Le tableau suivant indique les mesures par défaut pour chaque classe. Un utilisateur peut également utiliser les valeurs de la `evaluation.metric` colonne pour activer une mesure spécifique.

| `evaluator.class` | Mesures par défaut | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Matrice de précision <br>-de <br>rappel-de-confusion <br>-F-de-précision <br>-Caractéristiques d&#39;exploitation du receveur- <br><br>Zone sous les caractéristiques d&#39;exploitation du receveur | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Matrice de précision <br>-de <br>rappel-de-confusion <br>-F-de-précision <br>-Caractéristiques d&#39;exploitation du receveur- <br><br>Zone sous les caractéristiques d&#39;exploitation du receveur | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Précision moyenne moyenne (MAP) <br>normalisée Gain cumulé cumulé actualisé <br>-Rang réciproque <br>moyen de lamesure K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Mesures d’évaluation personnalisées pour Scala

L’évaluateur personnalisé peut être fourni en étendant l’interface de `MLEvaluator.scala` dans votre `Evaluator.scala` fichier. Dans l’exemple de fichier [Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) , nous définissons des fonctions personnalisées `split()` et `evaluate()` des fonctions. Notre `split()` fonction divise nos données de manière aléatoire avec un ratio de 8:2 et notre `evaluate()` fonction définit et renvoie 3 mesures : MAPE, MAE et RMSE.

>[!IMPORTANT] Pour la `MLMetric` classe, n’utilisez pas `"measures"` pour `valueType` lors de la création d’un nouveau paramètre `MLMetric` sinon la mesure ne sera pas renseignée dans le tableau des mesures d’évaluation personnalisées.
>  
> Procédez comme suit : `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> Pas ceci : `metrics.add(new MLMetric("MAPE", mape, "measures"))`


Une fois définie dans la recette, l&#39;étape suivante consiste à l&#39;activer dans les recettes. Cette opération est effectuée dans le fichier [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) du `resources` dossier du projet. Ici, la `evaluation.class` classe est définie sur la `Evaluator` classe définie dans `Evaluator.scala`

```properties
evaluation.class=com.adobe.platform.ml.Evaluator
```

Dans l’espace de travail des sciences de données, l’utilisateur peut consulter les informations dans l’onglet &quot;Mesures d’évaluation&quot; de la page de l’expérience.

### Python/Tensorflow {#pythontensorflow}

Il n’existe pas, à ce jour, de mesures d’évaluation par défaut pour Python ou Tensorflow. Ainsi, pour obtenir les mesures d’évaluation pour Python ou Tensorflow, vous devez créer une mesure d’évaluation personnalisée. Cela peut être fait en implémentant la `Evaluator` classe.

#### Mesures d&#39;évaluation personnalisées pour Python

Pour les mesures d’évaluation personnalisées, deux méthodes principales doivent être implémentées pour l’évaluateur : `split()` et `evaluate()`.

Pour Python, ces méthodes seraient définies dans [évaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) pour la `Evaluator` classe. Suivez le lien [évaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) pour obtenir un exemple du `Evaluator`.

La création de mesures d&#39;évaluation en Python nécessite que l&#39;utilisateur mette en oeuvre les `evaluate()` méthodes et les `split()` .

La `evaluate()` méthode renvoie l’objet metric qui contient un tableau d’objets metric avec les propriétés `name`, `value`et `valueType`.

La `split()` méthode a pour but de saisir des données et de produire une formation et un jeu de données de test. Dans notre exemple, la `split()` méthode saisit les données à l’aide du `DataSetReader` SDK, puis nettoie les données en supprimant les colonnes non liées. A partir de là, d’autres fonctionnalités sont créées à partir des fonctionnalités brutes existantes dans les données.

La `split()` méthode doit renvoyer une base de données de formation et de test qui est ensuite utilisée par les `pipeline()` méthodes pour former et tester le modèle ML.

#### Mesures d’évaluation personnalisées pour Tensorflow

Pour Tensorflow, similaire à Python, les méthodes `evaluate()` et `split()` dans la `Evaluator` classe devront être implémentées. Par exemple, `evaluate()`les mesures doivent être renvoyées pendant `split()` le retour des ensembles de données de train et d’essai.

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

À ce jour, il n’existe aucune mesure d’évaluation par défaut pour R. Ainsi, pour obtenir les mesures d’évaluation de R, vous devez définir la `applicationEvaluator` classe dans le cadre de la recette.

#### Mesures d’évaluation personnalisées pour R

L’objectif principal de la `applicationEvaluator` méthode est de renvoyer un objet JSON contenant des paires clé-valeur de mesures.

Cet [fichier applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) peut servir d’exemple. Dans cet exemple, la `applicationEvaluator` section est divisée en trois sections courantes :
- Charger des données
- Préparation des données/conception des fonctionnalités
- Récupérer le modèle enregistré et évaluer

Les données sont tout d’abord chargées dans un jeu de données à partir d’une source, comme défini dans [détail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). A partir de là, les données sont nettoyées et conçues pour s&#39;adapter au modèle d&#39;apprentissage automatique. Enfin, le modèle est utilisé pour faire une prédiction à l&#39;aide de notre jeu de données et à partir des valeurs prédites et des valeurs réelles, les mesures sont calculées. Dans ce cas, MAPE, MAE et RMSE sont définis et renvoyés dans l’ `metrics` objet.

## Utilisation de mesures prédéfinies et de graphiques de visualisation

Le cadre Sensei Model Insights Framework prend en charge un modèle par défaut pour chaque type d’algorithme d’apprentissage automatique. Le tableau ci-dessous présente les classes d’algorithme d’apprentissage automatique de haut niveau courantes et les mesures d’évaluation et visualisations correspondantes.

| Type d&#39;algorithme XML | Mesures d’évaluation | Visualisations |
--- | --- | ---
| Régression | - RMSE<br>- MAPE<br>- MASE<br>- MAE | Courbe d’incrustation des valeurs prédites et réelles |
| Classification binaire | - Matrice<br>confusionnelle - Rappel<br>de précision - Précision<br>- Score F (plus précisément F1,F2)<br>- AUC<br>- ROC | Matrice de courbe et de confusion du CRO |
| Classification multi-classe | -Matrice de confusion <br>- Pour chaque classe : <br>- précision du rappel de précision <br>- Score F (en particulier F1, F2) | Matrice de courbe et de confusion du CRO |
| Mise en grappe (avec vérité au sol) | - INM (note d&#39;information mutuelle normalisée), AMI (note d&#39;information mutuelle ajustée)<br>- RI (indice de rand), ARI (indice de rand ajusté)<br>- note d&#39;homogénéité, note d&#39;exhaustivité et mesure<br>V- FMI (indice de Fowlkes-Mallow)<br>- Indice de pureté<br>- Jaccard | Graphique de grappes montrant les grappes et les centroïdes avec des tailles de grappe relatives reflétant les points de données appartenant à la grappe |
| Mise en grappe (sans vérité au sol) | - Inertia<br>- Coefficient<br>de Silhouette- CHI (indice Calinski-Harabaz)<br>- DBI (indice Davies-Bouldin)<br>- Indice de Dunn | Graphique de grappes montrant les grappes et les centroïdes avec des tailles de grappe relatives reflétant les points de données appartenant à la grappe |
| Recommandation | -Précision moyenne moyenne (MAP) <br>normalisée Gain cumulé cumulé actualisé <br>-Rang réciproque <br>moyen de lamesure K | TBD |
| Cas d’utilisation de TensorFlow | Modèle TensorFlow   (TFMA) | Comparaison approfondie des modèles de réseau neuronal et de la visualisation |
| Autre mécanisme de capture/erreur | Logique de mesure personnalisée (et graphiques d’évaluation correspondants) définie par l’auteur du modèle. Gestion des erreurs gracieuse en cas de non-correspondance de modèle | Tableau avec des paires clé-valeur pour les mesures d’évaluation |
