---
keywords: Experience Platform;guide de développement;point de terminaison;Data Science Workspace;rubriques les plus consultées;moteurs;api d’apprentissage automatique sensei
solution: Experience Platform
title: Point de terminaison de l’API Moteurs
description: Les moteurs sont le fondement des modèles de machine learning dans l’espace de travail de science des données. Ils contiennent des algorithmes de machine learning qui permettent de résoudre des problèmes spécifiques, des pipelines de fonctionnalités permettant de concevoir des fonctionnalités, ou les deux.
role: Developer
exl-id: 7c670abd-636c-47d8-bd8c-5ce0965ce82f
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 65%

---

# Point de terminaison des moteurs

Les moteurs sont le fondement des modèles de machine learning dans l’espace de travail de science des données. Ils contiennent des algorithmes de machine learning qui permettent de résoudre des problèmes spécifiques, des pipelines de fonctionnalités permettant de concevoir des fonctionnalités, ou les deux.

## Recherche de votre registre Docker

>[!TIP]
>
>Si vous ne disposez pas d’une URL Docker, consultez le tutoriel [Former une recette empaquetée à partir de fichiers source](../models-recipes/package-source-files-recipe.md) pour une présentation détaillée de la création d’une URL d’hôte Docker.

Les informations d’identification de votre registre Docker sont nécessaires pour charger un fichier de recette empaqueté, y compris l’URL de votre hôte Docker, votre nom d’utilisateur et votre mot de passe. Vous pouvez rechercher ces informations en exécutant la requête GET suivante :

**Format d’API**

```https
GET /engines/dockerRegistry
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails de votre registre Docker, y compris l’URL Docker (`host`), le nom d’utilisateur (`username`), et le mot de passe (`password`).

>[!NOTE]
>
>Votre mot de passe Docker change chaque fois que votre `{ACCESS_TOKEN}` est mis à jour.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Création d’un moteur à l’aide des URL Docker {#docker-image}

Vous pouvez créer un moteur en exécutant une requête POST tout en fournissant ses métadonnées et une URL Docker qui référence une image Docker dans des formulaires en plusieurs parties.

**Format d’API**

```https
POST /engines
```

**Demander Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour le moteur. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que nom de la recette. |
| `description` | Description facultative du moteur. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que description de la recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur comme étant une chaîne vide. |
| `type` | Type d’exécution du moteur. Cette valeur correspond au langage dans lequel l’image Docker est conçue, et peut être soit « Python », « R » ou « Tensorflow ». |
| `algorithm` | Chaîne spécifiant le type d’algorithme de machine learning. Les types d’algorithmes pris en charge comprennent la « Classification », la « Régression » ou la « Personnalisation ». |
| `artifacts.default.image.location` | Emplacement de l’image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond au langage dans lequel l’image Docker est conçue, et peut être soit « Python », « R » ou « Tensorflow ». |

**Demander PySpark/Scala**

Lors de l’exécution d’une requête pour les recettes PySpark, les `executionType` et `type` sont &quot;PySpark&quot;. Lors de l’exécution d’une requête pour les recettes Scala, les `executionType` et `type` sont &quot;Spark&quot;. L’exemple de recette Scala suivant utilise Spark :

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour le moteur. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que nom de la recette. |
| `description` | Description facultative du moteur. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que description de la recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur comme étant une chaîne vide. |
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée. La valeur peut être définie sur Spark ou PySpark. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. Ce champ doit être défini sur `databricks-spark`. |
| `artifacts.default.image.location` | Emplacement de l’image Docker. Seul Azure ACR ou Public (non authentifié) Dockerhub est pris en charge. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée. Il peut s’agir de &quot;Spark&quot; ou de &quot;PySpark&quot;. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails du nouveau moteur, y compris son identifiant unique (`id`). L’exemple de réponse suivant est pour un moteur Python. Toutes les réponses du moteur suivent ce format :

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Création d’un moteur de pipeline de fonctionnalités à l’aide des URL Docker {#feature-pipeline-docker}

Vous pouvez créer un moteur de pipeline de fonctionnalités en exécutant une requête de POST tout en fournissant ses métadonnées et une URL Docker qui référence une image Docker.

**Format d’API**

```https
POST /engines
```

**Requête**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| Propriété | Description |
| --- | --- |
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée. La valeur peut être définie sur Spark ou PySpark. |
| `algorithm` | L’algorithme en cours d’utilisation, définissez cette valeur sur `fp` (pipeline de fonctionnalités). |
| `name` | Nom souhaité pour le moteur de pipeline de fonctionnalités. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que nom de la recette. |
| `description` | Description facultative du moteur. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que description de la recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur comme étant une chaîne vide. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. Ce champ doit être défini sur `databricks-spark`. |
| `artifacts.default.image.location` | Emplacement de l’image Docker. Seul Azure ACR ou Public (non authentifié) Dockerhub est pris en charge. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée. Il peut s’agir de &quot;Spark&quot; ou de &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | Type de package du moteur. Cette valeur doit être définie sur `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Vos paramètres de fichier de configuration `pipeline.json`. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails du nouveau moteur de pipeline de fonctionnalités, y compris son identifiant unique (`id`). L’exemple de réponse suivant concerne un moteur de pipeline de fonctionnalités PySpark.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## Récupération d’une liste de moteurs

Vous pouvez récupérer une liste de moteurs en exécutant une seule requête GET. Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres de requête dans le chemin de requête. Pour obtenir une liste des requêtes disponibles, reportez-vous à la section de l’annexe concernant les [paramètres de requête pour la récupération des ressources](./appendix.md#query).

**Format d’API**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste de moteurs et leurs détails.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### Récupération d’un moteur spécifique {#retrieve-specific}

Vous pouvez récupérer les détails d’un moteur spécifique en exécutant une requête GET qui inclut l’identifiant du moteur de votre choix dans le chemin d’accès à la requête.

**Format d’API**

```https
GET /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | Identifiant d’un moteur existant. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails du moteur concerné.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## Mise à jour d’un moteur

Vous pouvez modifier et mettre à jour un moteur existant en écrasant ses propriétés par le biais d’une requête PUT qui inclut l’identifiant du moteur cible dans le chemin d’accès à la requête et en fournissant un payload JSON contenant des propriétés mises à jour.

>[!NOTE]
>
>Afin de garantir le succès de cette requête de PUT, il est conseillé d’effectuer d’abord une requête de GET pour [récupérer le moteur par l’identifiant](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié en tant que payload de la requête PUT.

L’exemple d’appel API suivant met à jour le nom et la description d’un moteur lorsque les propriétés initiales sont les suivantes :

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**Format d’API**

```https
PUT /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | Identifiant d’un moteur existant. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**Réponse**

Une réponse réussie renvoie un payload contenant les détails mis à jour du moteur.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Suppression d’un moteur

Vous pouvez supprimer un moteur en exécutant une requête DELETE tout en spécifiant l’identifiant du moteur cible dans le chemin d’accès à la requête. La suppression d’un moteur entraînera la suppression en cascade de toutes les MLInstances qui font référence à ce moteur, y compris toutes les expériences et les exécutions d’expériences appartenant à ces MLInstances.

**Format d’API**

```https
DELETE /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | Identifiant d’un moteur existant. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
