---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importation d’une recette empaquetée (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 62%

---


# Importation d’une recette empaquetée (API)

This tutorial uses the [!DNL Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) to create an [Engine](../api/engines.md), also known as a Recipe in the user interface.

Before getting started, it is important to note that Adobe Experience Platform [!DNL Data Science Workspace] uses different terms to refer to similar elements within the API and UI. Les termes de l’API sont utilisés dans ce tutoriel et le tableau suivant décrit les termes corrélés :

| Terme de l’interface utilisateur | Terme de l’API |
| ---- | ---- |
| Recette | [Moteur](../api/engines.md) |
| Modèle | [MLInstance](../api/mlinstances.md) |
| Formation et évaluation | [Expérience](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Un moteur contient des algorithmes d’apprentissage automatique et une logique pour résoudre des problèmes spécifiques. The diagram below provides a visualization showing the API workflow in [!DNL Data Science Workspace]. Ce tutoriel se concentre sur la création d’un moteur, le cerveau d’un modèle d’apprentissage automatique.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Prise en main

Ce didacticiel nécessite un fichier de recette empaqueté sous la forme d&#39;une URL Docker. Suivez le tutoriel [Former une recette empaquetée à partir de fichiers source](./package-source-files-recipe.md) pour savoir comment créer un fichier de recette empaquetée ou fournir votre fichier.

- `{DOCKER_URL}` : adresse URL vers une image Docker d’un service intelligent.

Pour suivre ce tutoriel, vous devez avoir terminé le tutoriel [Authentification à Adobe Experience ](../../tutorials/authentication.md) afin d’effectuer avec succès des appels vers les API Platform. [!DNL Platform] Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- `{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{IMS_ORG}` : vos informations d’identification d’organisation IMS, qui se trouvent dans votre intégration unique d’Adobe Experience Platform.
- `{API_KEY}` : valeur de clé API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.

## Création d’un moteur

Vous pouvez créer des moteurs en adressant une requête de POST au point de terminaison /engine. Le moteur créé est configuré en fonction du formulaire du fichier de recette empaqueté qui doit être inclus dans la demande d&#39;API.

### Création d’un moteur avec une URL Docker {#create-an-engine-with-a-docker-url}

Pour créer un moteur avec un fichier de recette empaquetée stocké dans un conteneur Docker, vous devez fournir l’URL Docker au fichier de recette empaquetée.

>[!CAUTION]
>
> Si vous utilisez [!DNL Python] ou R, utilisez la requête ci-dessous. Si vous utilisez PySpark ou Scala, utilisez l’exemple de requête PySpark/Scala situé sous l’exemple Python/R.

**Format d’API**

```http
POST /engines
```

**Demande de Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Propriété | Description |
| -------  | ----------- |
| `engine.name` | Nom souhaité pour le moteur. The Recipe corresponding to this Engine will inherit this value to be displayed in [!DNL Data Science Workspace] user interface as the Recipe&#39;s name. |
| `engine.description` | Description facultative du moteur. The Recipe corresponding to this Engine will inherit this value to be displayed in [!DNL Data Science Workspace] user interface as the Recipe&#39;s description. Ne supprimez pas cette propriété, laissez une chaîne vide pour cette valeur si vous choisissez de ne pas fournir de description. |
| `engine.type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker a été développée. When a Docker URL is provided to create an Engine, `type` is either `Python`, `R`, `PySpark`, `Spark` (Scala), or `Tensorflow`. |
| `artifacts.default.image.location` | Your `{DOCKER_URL}` goes here. A complete Docker URL has the following structure: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Nom supplémentaire du fichier image Docker. Ne supprimez pas cette propriété, laissez une chaîne vide pour cette valeur si vous choisissez de ne pas fournir de nom de fichier image Docker supplémentaire. |
| `artifacts.default.image.executionType` | Type d&#39;exécution de ce moteur. Cette valeur correspond à la langue dans laquelle l’image Docker a été développée. When a Docker URL is provided to create an Engine, `executionType` is either `Python`, `R`, `PySpark`, `Spark` (Scala), or `Tensorflow`. |

**Request PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
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
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est construite sur &quot;PySpark&quot;. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l’image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image du Docker est construite sur &quot;Spark&quot;. |

**Request Scala**

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
| `name` | Nom souhaité pour le moteur. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que nom de la recette. |
| `description` | Description facultative du moteur. La recette correspondant à ce moteur héritera de cette valeur afin d’être affichée dans l’interface utilisateur en tant que description de la recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur comme étant une chaîne vide. |
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image du Docker est construite sur &quot;Spark&quot;. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l’image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image du Docker est construite sur &quot;Spark&quot;. |

**Réponse**

Une réponse réussie renvoie un payload contenant les détails du nouveau moteur, y compris son identifiant unique (`id`). L&#39;exemple de réponse suivant est pour un [!DNL Python] moteur. Les `executionType` clés et `type` les clés changent en fonction du POST fourni.

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

Une réponse réussie affiche un payload JSON contenant des informations sur le moteur créé. La clé `id` représente l’identifiant de moteur unique et est requise dans le tutoriel suivant pour créer une instance MLInstance. Vérifiez que l’identifiant du moteur est enregistré avant de passer aux étapes suivantes.

## Étapes suivantes {#next-steps}

Vous avez créé un moteur à l’aide de l’API et avez obtenu un identifiant de moteur unique dans le corps de la réponse. Vous pouvez utiliser cet identifiant de moteur dans le tutoriel suivant où vous apprendrez à [créer, former et évaluer un modèle à l’aide de l’API](./train-evaluate-model-api.md).