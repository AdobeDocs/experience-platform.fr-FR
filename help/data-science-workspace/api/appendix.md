---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Annexe
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 5%

---


# Annexe

Les sections suivantes contiennent des informations de référence sur les différentes fonctionnalités de l’ [!DNL Sensei Machine Learning] API.

## Paramètres de Requête pour la récupération de ressources {#query}

L’ [!DNL Sensei Machine Learning] API prend en charge les paramètres de requête lors de la récupération des ressources. Les paramètres de requête disponibles et leur utilisation sont décrits dans le tableau suivant :

| Paramètre de requête | Description | Valeur par défaut |
| --------------- | ----------- | ------- |
| `start` | Indique l’index de début de la pagination. | `start=0` |
| `limit` | Indique le nombre maximal de résultats à renvoyer. | `limit=25` |
| `orderby` | Indique les propriétés à utiliser pour le tri dans l’ordre de priorité. Insérez un tiret (**-**) avant le nom d’une propriété pour effectuer un tri dans l’ordre décroissant, sinon les résultats sont triés dans l’ordre croissant. | `orderby=created` |
| `property` | Indique l’expression de comparaison qu’un objet doit satisfaire pour être renvoyé. | `property=deleted==false` |

>[!NOTE]
>
>Lorsque vous combinez plusieurs paramètres de requête, ils doivent être séparés par des esperluettes (**&amp;**).

## Configurations Python CPU et GPU {#cpu-gpu-config}

Les moteurs Python ont la possibilité de choisir entre un processeur ou un GPU pour son entraînement ou son score, et est défini sur une [instance](./mlinstances.md) MLInstance comme une spécification de tâche (`tasks.specification`).

Voici un exemple de configuration qui spécifie l’utilisation d’un processeur pour la formation et d’un processeur graphique pour la notation :

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>Les valeurs de `cpus` et `gpus` ne désignent pas le nombre d&#39;UC ou de GPU, mais plutôt le nombre de machines physiques. Ces valeurs sont autorisées `"1"` et génèrent une exception dans le cas contraire.

## Configurations des ressources PySpark et Spark {#resource-config}

Les moteurs Spark permettent de modifier les ressources de calcul à des fins de formation et de notation. Ces ressources sont décrites dans le tableau suivant :

| Ressource | Description | Type |
| -------- | ----------- | ---- |
| driverMemory | Mémoire du pilote en mégaoctets | int |
| driverCores | Nombre de noyaux utilisés par le pilote | int |
| exécuteurMémoire | Mémoire de l&#39;exécuteur en mégaoctets | int |
| exécuteurCores | Nombre de coeurs utilisés par l&#39;exécuteur | int |
| numExecutors | Nombre d&#39;exécuteurs | int |

Les ressources peuvent être spécifiées sur une [instance](./mlinstances.md) de la MLI en tant que (A) paramètres de formation ou de notation individuels, ou (B) dans un objet de spécification supplémentaire (`specification`). Par exemple, les configurations de ressources suivantes sont identiques pour la formation et la notation :

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
