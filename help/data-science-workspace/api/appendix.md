---
keywords: Experience Platform;guide de développement;point de terminaison;Data Science Workspace;rubriques les plus consultées
solution: Experience Platform
title: Guide de l’API d’apprentissage automatique Sensei
description: Les sections suivantes fournissent des informations de référence pour différentes fonctionnalités de l’API Sensei Machine Learning.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 66%

---

# [!DNL Sensei Machine Learning] annexe du guide de l’API

Les sections suivantes fournissent des informations de référence pour différentes fonctionnalités de l’API [!DNL Sensei Machine Learning].

## Paramètres de requête pour la récupération de ressources {#query}

L’API [!DNL Sensei Machine Learning] prend en charge les paramètres de requête pour la récupération des ressources. Les paramètres de requête disponibles et leurs utilisations sont décrits dans le tableau suivant :

| Paramètre de requête | Description | Valeur par défaut |
| --------------- | ----------- | ------- |
| `start` | Indique l’index de départ de pagination. | `start=0` |
| `limit` | Indique le nombre de résultats maximum à renvoyer. | `limit=25` |
| `orderby` | Indique les propriétés à utiliser pour trier dans l’ordre de priorité. Incluez un tiret (**-**) devant un nom de propriété pour trier dans l’ordre décroissant. Dans le cas contraire, les résultats sont triés dans l’ordre croissant. | `orderby=created` |
| `property` | Indique l’expression de comparaison qu’un objet doit satisfaire pour être renvoyé. | `property=deleted==false` |

>[!NOTE]
>
>Lorsque vous combinez plusieurs paramètres de requête, ils doivent être séparés par des esperluettes (**&amp;**).

## Configurations du processeur et du processeur graphique Python {#cpu-gpu-config}

Avec les moteurs Python, vous avez la possibilité de choisir entre un processeur ou un processeur graphique à des fins de formation ou de notation. Ceux-ci sont définis sur une [MLInstance](./mlinstances.md) en tant que spécification de tâche (`tasks.specification`).

L’exemple suivant présente une configuration qui précise l’utilisation d’un processeur à des fins de formation et d’un processeur graphique à des fins de notation :

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
>Les valeurs `cpus` et `gpus` ne signifient pas le nombre de processeurs ou de processeurs graphiques, mais plutôt le nombre de machines physiques. Ces valeurs sont acceptablement `"1"` et renverront une exception dans le cas contraire.

## Configurations des ressources PySpark et Spark {#resource-config}

Les moteurs Spark permettent de modifier des ressources de calcul à des fins de formation et de notation. Ces ressources sont décrites dans le tableau suivant :

| Ressource | Description | Type |
| -------- | ----------- | ---- |
| driverMemory | Mémoire du pilote en mégaoctets | ent |
| driverCores | Nombre de noyaux utilisés par le pilote | ent |
| executorMemory | Mémoire de l’exécuteur en mégaoctets | ent |
| executorCores | Nombre de noyaux utilisés par l’exécuteur | ent |
| numExecutors | Nombre d’exécuteurs | ent |

Vous pouvez préciser les ressources dans une [MLInstance](./mlinstances.md) en tant que soit (A) en paramètres de formation ou de notation uniques, soit (B) au sein d’un objet de spécifications supplémentaire (`specification`). Par exemple, les configurations de ressource suivantes sont les mêmes aussi bien pour la formation que la notation :

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
