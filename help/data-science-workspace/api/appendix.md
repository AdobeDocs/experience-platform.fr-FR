---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Annexe
topic: Developer guide
translation-type: tm+mt
source-git-commit: 2940f69d193ff8a4ec6ad4a58813b5426201ef45

---


# Annexe

Les sections suivantes fournissent des informations de référence pour diverses fonctionnalités de l’API d’apprentissage automatique Sensei.

## Paramètres de  pour la récupération des ressources {#query}

L’API d’apprentissage automatique Sensei prend en charge les paramètres de  lors de la récupération des ressources. Les paramètres  disponibles et leur utilisation sont décrits dans le tableau suivant :

| Paramètre de requête | Description | Valeur par défaut |
| --------------- | ----------- | ------- |
| `start` | Indique l’index de début de la pagination. | `start=0` |
| `limit` | Indique le nombre maximal de résultats à renvoyer. | `limit=25` |
| `orderby` | Indique les propriétés à utiliser pour le tri dans l’ordre de priorité. Insérez un tiret (**-**) avant le nom d’une propriété pour trier dans l’ordre décroissant, sinon les résultats sont triés dans l’ordre croissant. | `orderby=created` |
| `property` | Indique le  de comparaison  que doit satisfaire un objet pour être renvoyé. | `property=deleted==false` |

>[!NOTE] Lorsque vous combinez plusieurs paramètres de , ils doivent être séparés par des esperluettes (**&amp;**).

## Configurations du processeur et du processeur graphique Python {#cpu-gpu-config}

Les moteurs Python ont la possibilité de choisir entre un processeur ou un GPU à des fins d&#39;entraînement ou de notation, et sont définis sur une [instance](./mlinstances.md) MLInstance`tasks.specification`comme une spécification de  ().

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

>[!NOTE] Les valeurs de `cpus` et `gpus` ne désignent pas le nombre de processeurs ou de processeurs graphiques, mais plutôt le nombre de machines physiques. Ces valeurs sont autorisées `"1"` et renvoient une exception dans le cas contraire.

## Configurations des ressources PySpark et Spark {#resource-config}

Les moteurs Spark peuvent modifier les ressources de calcul à des fins de formation et de notation. Ces ressources sont décrites dans le tableau suivant :

| Ressource | Description | Type |
| -------- | ----------- | ---- |
| driverMemory | Mémoire du pilote en mégaoctets | int |
| driverCores | Nombre de noyaux utilisés par le pilote | int |
| exécuteurMemory | Mémoire de l&#39;exécuteur testamentaire en mégaoctets | int |
| exécuteurCores | Nombre de noyaux utilisés par l&#39;exécuteur | int |
| numExecutors | Nombre d’exécuteurs | int |

Les ressources peuvent être spécifiées sur une [instance](./mlinstances.md) d&#39;instruction ou de notation individuelle, soit (A) soit (B) dans un objet de spécification supplémentaire (`specification`). Par exemple, les configurations de ressources suivantes sont identiques pour la formation et la notation :

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
