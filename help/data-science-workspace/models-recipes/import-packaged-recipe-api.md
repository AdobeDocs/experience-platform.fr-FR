---
keywords: Experience Platform;importer une recette empaquetée;Workspace de science des données;rubriques populaires;recettes;api;machine learning sensei;créer un moteur
solution: Experience Platform
title: Importer une recette empaquetée à l’aide de l’API Sensei Machine Learning
type: Tutorial
description: Ce tutoriel utilise l’API Sensei Machine Learning pour créer un moteur, également appelé recette dans l’interface utilisateur.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 50%

---

# Importer une recette empaquetée à l’aide de l’API Sensei Machine Learning

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Ce tutoriel utilise le [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) pour créer un [moteur](../api/engines.md), également appelé recette dans l’interface utilisateur.

Avant de commencer, il est important de noter que Adobe Experience Platform [!DNL Data Science Workspace] utilise des termes différents pour faire référence à des éléments similaires dans l’API et l’interface utilisateur. Les termes de l’API sont utilisés dans ce tutoriel et le tableau suivant décrit les termes corrélés :

| Terme de l’interface utilisateur | Terme de l’API |
| ---- | ---- |
| Recette | [Moteur](../api/engines.md) |
| Modèle | [MLInstance](../api/mlinstances.md) |
| Formation et évaluation | [Expérience](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Un moteur contient des algorithmes de machine learning et une logique pour résoudre des problèmes spécifiques. Le diagramme ci-dessous présente une visualisation du workflow de l’API dans [!DNL Data Science Workspace]. Ce tutoriel se concentre sur la création d’un moteur, le cerveau d’un modèle de machine learning.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Prise en main

Ce tutoriel nécessite un fichier de recette empaqueté sous la forme d’une URL Docker. Suivez le tutoriel [Former une recette empaquetée à partir de fichiers sources](./package-source-files-recipe.md) pour savoir comment créer un fichier de recette empaquetée ou fournir votre fichier.

- `{DOCKER_URL}` : adresse URL d’une image Docker d’un service intelligent.

Pour suivre ce tutoriel, vous devez avoir terminé le tutoriel [Authentification à Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) afin d’effectuer avec succès des appels vers les API [!DNL Experience Platform]. Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `{ACCESS_TOKEN}` : votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{ORG_ID}` : informations d’identification de votre organisation, qui se trouvent dans votre intégration Adobe Experience Platform unique.
- `{API_KEY}` : valeur de clé API spécifique, qui se trouve dans votre intégration unique d’Adobe Experience Platform.

## Création d’un moteur

Les moteurs peuvent être créés en adressant une requête POST au point d’entrée /engine. Le moteur créé est configuré en fonction de la forme du fichier de recette empaqueté qui doit être inclus dans la requête API.

### Création d’un moteur avec une URL Docker {#create-an-engine-with-a-docker-url}

Pour créer un moteur avec un fichier de recette empaquetée stocké dans un conteneur Docker, vous devez fournir l’URL Docker au fichier de recette empaquetée.

>[!CAUTION]
>
> Si vous utilisez [!DNL Python] ou R, utilisez la requête ci-dessous. Si vous utilisez PySpark ou Scala, utilisez l’exemple de requête PySpark/Scala situé sous l’exemple Python/R.

**Format d’API**

```http
POST /engines
```

**Requête Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `engine.name` | Nom souhaité pour le moteur. La recette correspondant à ce moteur hérite de cette valeur pour s’afficher dans [!DNL Data Science Workspace]’interface utilisateur en tant que nom de la recette. |
| `engine.description` | Description facultative du moteur. La recette correspondant à ce moteur hérite de cette valeur pour s’afficher dans [!DNL Data Science Workspace]’interface utilisateur en tant que description de la recette. Ne supprimez pas cette propriété, laissez une chaîne vide pour cette valeur si vous choisissez de ne pas fournir de description. |
| `engine.type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est développée. Lorsqu’une URL Docker est fournie pour créer un moteur, `type` est `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |
| `artifacts.default.image.location` | Votre `{DOCKER_URL}` va ici. Une URL Docker complète présente la structure suivante : `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Nom supplémentaire pour le fichier image Docker. Ne supprimez pas cette propriété, laissez une chaîne vide pour cette valeur si vous choisissez de ne pas fournir de nom de fichier image Docker supplémentaire. |
| `artifacts.default.image.executionType` | Type d&#39;exécution de ce moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est développée. Lorsqu’une URL Docker est fournie pour créer un moteur, `executionType` est `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |

**Demander PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée sur « PySpark ». |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l’image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée sur « Spark ». |

**Requête Scala**

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
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée sur « Spark ». |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l’image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est créée sur « Spark ». |

**Réponse**

Une réponse réussie renvoie une payload contenant les détails du moteur nouvellement créé, y compris son identifiant unique (`id`). L’exemple de réponse suivant concerne un moteur [!DNL Python]. Les clés `executionType` et `type` changent en fonction de l’instruction POST fournie.

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
