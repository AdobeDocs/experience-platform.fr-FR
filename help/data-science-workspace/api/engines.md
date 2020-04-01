---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Moteurs
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# Moteurs

Les moteurs sont les fondations des modèles d’apprentissage automatique dans Data Science Workspace. Ils contiennent des algorithmes d’apprentissage automatique qui résolvent des problèmes spécifiques, des pipelines de fonctionnalités pour l’ingénierie de fonctionnalités, ou les deux.

## Recherchez votre registre Docker.

Les informations d’identification de votre Registre Docker sont requises pour télécharger un fichier Recette compressé, y compris l’URL hôte, le nom d’utilisateur et le mot de passe de votre Docker. Vous pouvez rechercher ces informations en exécutant la requête GET suivante :

**Format API**

```http
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

Une réponse réussie renvoie une charge utile contenant les détails de votre registre Docker, y compris l&#39;URL (`host`), le nom d&#39;utilisateur (`username`) et le mot de passe (`password`) du Docker.

>[!NOTE] Votre mot de passe Docker change chaque fois que vous `{ACCESS_TOKEN}` êtes mis à jour.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Création d’un moteur à l’aide des URL du Docker

Vous pouvez créer un moteur en exécutant une requête POST tout en fournissant ses métadonnées et une URL Docker qui référence une image Docker dans plusieurs formulaires.

**Format API**

```http
POST /engines
```

**Requête**

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
                    "location": "{DOCKER_URL}",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `type` | Type d’exécution du moteur. Cette valeur correspond au langage dans lequel l’image Docker est construite et peut être &quot;Python&quot;, &quot;R&quot; ou &quot;Tensorflow&quot;. |
| `algorithm` | Chaîne spécifiant le type d’algorithme d’apprentissage automatique. Les types d’algorithme pris en charge sont &quot;Classification&quot;, &quot;Régression&quot; ou &quot;Personnalisé&quot;. |
| `artifacts.default.image.location` | Emplacement de l&#39;image du Docker à laquelle est liée une URL du Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond au langage dans lequel l’image Docker est construite et peut être &quot;Python&quot;, &quot;R&quot; ou &quot;Tensorflow&quot;. |


**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du nouveau moteur, y compris son identifiant unique (`id`).

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Création d’un moteur à l’aide d’artefacts binaires

Vous pouvez créer un moteur à l’aide d’artefacts locaux `.jar` ou `.egg` binaires en exécutant une requête POST tout en fournissant ses métadonnées et le chemin d’accès de l’artefact dans des formulaires en plusieurs parties.

**Format API**

```http
POST /engines
```

**Requête**

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
        "algorithm": "Classification",
        "type": "PySpark",
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file.egg'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `algorithm` | Chaîne spécifiant le type d’algorithme d’apprentissage automatique. Les types d’algorithme pris en charge sont &quot;Classification&quot;, &quot;Régression&quot; ou &quot;Personnalisé&quot;. |
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’artefact binaire est construit et peut être &quot;PySpark&quot; ou &quot;Spark&quot;. |


**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du nouveau moteur, y compris son identifiant unique (`id`).

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Création d’un moteur de pipeline de fonctionnalités à l’aide d’artefacts binaires

Vous pouvez créer un moteur de pipeline de fonctionnalités à l’aide d’artefacts locaux `.jar` ou `.egg` binaires en exécutant une requête POST tout en fournissant ses métadonnées et les chemins d’accès de l’artefact dans des formulaires en plusieurs parties. Un moteur PySpark ou Spark peut spécifier des ressources de calcul telles que le nombre de coeurs ou la quantité de mémoire. Pour plus d’informations, consultez la section de l’annexe sur les configurations [des ressources](./appendix.md#resource-config) PySpark et Spark.

**Format API**

```http
POST /engines
```

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "Feature Pipeline Engine",
        "description": "A feature pipeline Engine",
        "algorithm":"fp",
        "type": "PySpark"
    }' \
    -F 'featurePipelineOverrideArtifact=@path/to/binary/artifact/feature_pipeline.egg' \
    -F 'defaultArtifact=@path/to/binary/artifact/feature_pipeline.egg'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `algorithm` | Chaîne spécifiant le type d’algorithme d’apprentissage automatique. Définissez cette valeur sur &quot;fp&quot; pour spécifier que cette création doit être un moteur de pipeline de fonctionnalités. |
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle les artefacts binaires sont construits et peut être &quot;PySpark&quot; ou &quot;Spark&quot;. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du nouveau moteur, y compris son identifiant unique (`id`).

```json
{
    "id": "{ENGINE_ID}",
    "name": "Feature Pipeline Engine",
    "description": "A feature pipeline Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Récupération d&#39;un  de moteurs

Vous pouvez récupérer un de moteurs en exécutant une seule requête GET. Pour vous aider à filtrer les résultats, vous pouvez spécifier des paramètres  dans le chemin de requête. Pour un  de  de disponible, reportez-vous à la section de l’annexe sur les paramètres de [](./appendix.md#query)pour la récupérationdes ressources.

**Format API**

```http
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

Une réponse réussie renvoie un  de moteurs et leurs détails.

```json
{
    "children": [
        {
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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

Vous pouvez récupérer les détails d’un moteur spécifique en exécutant une requête GET qui inclut l’ID du moteur de votre choix dans le chemin d’accès à la requête.

**Format API**

```http
GET /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | ID d’un moteur existant. |

**Requête**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du moteur souhaité.

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Mettre à jour un moteur

Vous pouvez modifier et mettre à jour un moteur existant en écrasant ses propriétés par le biais d’une requête PUT qui inclut l’ID du moteur de  dans le chemin d’accès à la requête et fournit une charge JSON contenant des propriétés mises à jour.

>[!NOTE] Afin de garantir le succès de cette requête PUT, il est conseillé d’effectuer d’abord une requête GET pour [récupérer le moteur par ID](#retrieve-specific). Ensuite, modifiez et mettez à jour l’objet JSON renvoyé et appliquez l’intégralité de l’objet JSON modifié comme charge utile pour la requête PUT.

L’exemple d’appel d’API suivant met à jour le nom et la description d’un moteur lorsque les propriétés suivantes sont au départ :

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

**Format API**

```http
PUT /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | ID d’un moteur existant. |

**Requête**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
    "id": "{ENGINE_ID}",
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

Vous pouvez supprimer un moteur en exécutant une requête DELETE lors de la spécification de l’ID du moteur de  dans le chemin d’accès de la requête. La suppression en cascade d&#39;un moteur entraînera la suppression de toutes les instances MLInstances qui font référence à ce moteur, y compris les exécutions d&#39;expériences et d&#39;expériences appartenant à ces instances MLInstances.

**Format API**

```http
DELETE /engines/{ENGINE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{ENGINE_ID}` | ID d’un moteur existant. |

**Requête**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
