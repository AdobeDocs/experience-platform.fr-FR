---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Moteurs
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 3%

---


# Moteurs

Les moteurs sont les fondements des modèles d’apprentissage automatique dans Data Science Workspace. Ils contiennent des algorithmes d&#39;apprentissage automatique qui résolvent des problèmes spécifiques, des pipelines de fonctionnalités pour effectuer l&#39;ingénierie de fonctionnalités, ou les deux.

## Rechercher votre registre Docker

>[!TIP]
>Si vous n&#39;avez pas d&#39;URL Docker, consultez les fichiers source du [package dans un didacticiel de recette](../models-recipes/package-source-files-recipe.md) pour découvrir comment créer une URL hôte Docker étape par étape.

Vos informations d&#39;identification de registre Docker sont requises pour télécharger un fichier Recette compressé, y compris votre URL d&#39;hôte Docker, votre nom d&#39;utilisateur et votre mot de passe. Vous pouvez rechercher ces informations en exécutant la requête GET suivante :

**Format d’API**

```https
GET /engines/dockerRegistry
```

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails de votre registre Docker, y compris l&#39;URL (`host`) du Docker, le nom d&#39;utilisateur (`username`) et le mot de passe (`password`).

>[!NOTE]
>
>
>Votre mot de passe Docker change chaque fois que vous `{ACCESS_TOKEN}` êtes mis à jour.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Création d’un moteur à l’aide des URL du Docker {#docker-image}

Vous pouvez créer un moteur en exécutant une requête POST tout en fournissant ses métadonnées et une URL Docker qui référence une image Docker dans des formulaires en plusieurs parties.

**Format d’API**

```https
POST /engines
```

**Demande de Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `type` | Type d&#39;exécution du moteur. Cette valeur correspond au langage dans lequel l&#39;image Docker est construite et peut être &quot;Python&quot;, &quot;R&quot; ou &quot;Tensorflow&quot;. |
| `algorithm` | Chaîne spécifiant le type d’algorithme d’apprentissage automatique. Les types d’algorithme pris en charge sont &quot;Classification&quot;, &quot;Régression&quot; ou &quot;Personnalisé&quot;. |
| `artifacts.default.image.location` | Emplacement de l&#39;image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d&#39;exécution du moteur. Cette valeur correspond au langage dans lequel l&#39;image Docker est construite et peut être &quot;Python&quot;, &quot;R&quot; ou &quot;Tensorflow&quot;. |

**Demande de PySpark/Scala**

Lors d&#39;une demande de recettes PySpark, le `executionType` et `type` est &quot;PySpark&quot;. Lors d&#39;une demande de recettes Scala, le `executionType` et `type` est &quot;Spark&quot;. L’exemple de recette Scala suivant utilise Spark :

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `type` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est construite. La valeur peut être définie sur Spark ou PySpark. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. Ce champ doit être défini sur `databricks-spark`. |
| `artifacts.default.image.location` | Emplacement de l&#39;image Docker. Seul Azure ACR ou Public (non authentifié) Dockerhub est pris en charge. |
| `artifacts.default.image.executionType` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est construite. Il peut s’agir de &quot;Spark&quot; ou de &quot;PySpark&quot;. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du nouveau moteur, y compris son identifiant unique (`id`). L&#39;exemple de réponse suivant est pour un moteur Python. Toutes les réponses du moteur suivent ce format :

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

## Création d’un moteur de pipeline de fonctionnalités à l’aide des URL du Docker {#feature-pipeline-docker}

Vous pouvez créer un moteur de pipeline de fonctionnalités en exécutant une requête POST tout en fournissant ses métadonnées et une URL Docker qui référence une image Docker.

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
| `type` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est construite. La valeur peut être définie sur Spark ou PySpark. |
| `algorithm` | L’algorithme utilisé, définissez cette valeur sur `fp` (pipeline de fonctionnalités). |
| `name` | Nom souhaité pour le moteur de pipeline de fonctionnalités. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. Ce champ doit être défini sur `databricks-spark`. |
| `artifacts.default.image.location` | Emplacement de l&#39;image Docker. Seul Azure ACR ou Public (non authentifié) Dockerhub est pris en charge. |
| `artifacts.default.image.executionType` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est construite. Il peut s’agir de &quot;Spark&quot; ou de &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | Type d&#39;emballage du moteur. Cette valeur doit être définie sur `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Paramètres de votre fichier `pipeline.json` de configuration. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du nouveau moteur de pipeline de fonctionnalités, y compris son identifiant unique (`id`). L’exemple de réponse suivant est pour un moteur de pipeline de fonctionnalités PySpark.

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

## Récupération d&#39;une liste de moteurs

Vous pouvez récupérer une liste de moteurs en exécutant une seule requête GET. Pour faciliter le filtrage des résultats, vous pouvez spécifier des paramètres de requête dans le chemin d’accès à la requête. Pour une liste des requêtes disponibles, reportez-vous à la section de l&#39;annexe sur les paramètres de [requête pour la récupération](./appendix.md#query)des ressources.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

### Récupérer un moteur spécifique {#retrieve-specific}

Vous pouvez récupérer les détails d&#39;un moteur spécifique en exécutant une requête GET qui inclut l&#39;ID du moteur de votre choix dans le chemin d&#39;accès à la requête.

**Format d’API**

```https
GET /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | ID d&#39;un moteur existant. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du moteur de votre choix.

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

## Mettre à jour un moteur

Vous pouvez modifier et mettre à jour un moteur existant en remplaçant ses propriétés par une requête PUT qui inclut l’ID du moteur de cible dans le chemin de la requête et fournit une charge utile JSON contenant des propriétés mises à jour.

>[!NOTE]
>
>Afin d&#39;assurer le succès de cette requête PUT, il est conseillé d&#39;effectuer d&#39;abord une requête GET pour [récupérer le moteur par ID](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la demande PUT.

L&#39;exemple d&#39;appel d&#39;API suivant met à jour le nom et la description d&#39;un moteur lorsque ces propriétés sont initialement définies :

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
| `{ENGINE_ID}` | ID d&#39;un moteur existant. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Une réponse réussie renvoie une charge utile contenant les détails mis à jour du moteur.

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

Vous pouvez supprimer un moteur en exécutant une requête de DELETE tout en spécifiant l&#39;ID du moteur de cible dans le chemin de la requête. La suppression d&#39;un moteur entraîne la suppression en cascade de toutes les instances MLInstances qui font référence à ce moteur, y compris les exécutions d&#39;expériences et d&#39;expériences appartenant à ces instances MLInstances.

**Format d’API**

```https
DELETE /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | ID d&#39;un moteur existant. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
