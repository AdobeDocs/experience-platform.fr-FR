---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importer une recette (API) assemblée
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 1%

---


# Importer une recette (API) assemblée

Ce didacticiel utilise l&#39;API [d&#39;apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei pour créer un [moteur](../api/engines.md), également appelé Recette dans l&#39;interface utilisateur.

Avant de commencer, il est important de noter qu’Adobe Experience Platform Data Science Workspace utilise des termes différents pour faire référence à des éléments similaires dans l’API et l’interface utilisateur. Les termes API sont utilisés dans ce didacticiel et le tableau suivant décrit les termes corrélés :

| Terme de l’interface utilisateur | Terme de l’API |
| ---- | ---- |
| Recette | [Moteur](../api/engines.md) |
| Modèle | [Instance MLI](../api/mlinstances.md) |
| Formation et évaluation | [Expérience](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Un moteur contient des algorithmes d’apprentissage automatique et une logique permettant de résoudre des problèmes spécifiques. Le diagramme ci-dessous présente une visualisation présentant le processus des API dans Data Science Workspace. Ce tutoriel se concentre sur la création d&#39;un moteur, le cerveau d&#39;un modèle d&#39;apprentissage automatique.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Prise en main

Ce didacticiel nécessite un fichier de recette empaqueté sous la forme d&#39;un artefact binaire ou d&#39;une URL de Docker. Suivez les fichiers source du [package dans un didacticiel Recette](./package-source-files-recipe.md) pour créer un fichier de recette empaqueté ou pour fournir le vôtre.

- Artefact binaire (obsolète) : L&#39;artefact binaire (ex. JAR, EGG) utilisé pour créer un moteur.
- `{DOCKER_URL}`: Adresse URL d&#39;une image Docker d&#39;un service intelligent.

Ce didacticiel nécessite que vous ayez suivi le didacticiel [](../../tutorials/authentication.md) Authentication to Adobe Experience Platform (Authentification vers la plate-forme Adobe) pour pouvoir invoquer les API de plateforme. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- `{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique à Adobe Experience Platform.
- `{API_KEY}`: Votre valeur de clé d’API spécifique se trouve dans votre intégration unique d’Adobe Experience Platform.

## Création d’un moteur

Selon le formulaire du fichier de recette emballé à inclure dans la demande d&#39;API, un moteur est créé de l&#39;une des deux manières suivantes :

- [Création d’un moteur avec une URL de dossier](#create-an-engine-with-a-docker-url)
- [Création d’un moteur avec un artefact binaire (obsolète)](#create-an-engine-with-a-binary-artifact-deprecated)

### Création d’un moteur avec une URL de dossier {#create-an-engine-with-a-docker-url}

Pour créer un moteur avec un fichier de recette empaqueté stocké dans un conteneur Docker, vous devez fournir l&#39;URL Docker au fichier de recette empaqueté.

>[!CAUTION]
> Si vous utilisez Python ou R, utilisez la requête ci-dessous. Si vous utilisez PySpark ou Scala, utilisez l’exemple de demande PySpark/Scala situé sous l’exemple Python/R.

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
| `engine.name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur de l&#39;espace de travail des sciences de données en tant que nom de la Recette. |
| `engine.description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur de l&#39;espace de travail des sciences de données comme description de la Recette. Ne supprimez pas cette propriété, laissez cette valeur être une chaîne vide si vous choisissez de ne pas fournir de description. |
| `engine.type` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est développée. Lorsqu&#39;une URL de Docker est fournie pour créer un moteur, `type` est soit `Python`, `R`, `PySpark`, `Spark` (Scala), soit `Tensorflow`. |
| `artifacts.default.image.location` | Tu `{DOCKER_URL}` vas ici. Une URL Docker complète possède la structure suivante : `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Nom supplémentaire du fichier image Docker. Ne supprimez pas cette propriété, laissez cette valeur être une chaîne vide si vous choisissez de ne pas fournir un nom de fichier image Docker supplémentaire. |
| `artifacts.default.image.executionType` | Type d&#39;exécution de ce moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est développée. Lorsqu&#39;une URL de Docker est fournie pour créer un moteur, `executionType` est soit `Python`, `R`, `PySpark`, `Spark` (Scala), soit `Tensorflow`. |

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
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `type` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image Docker est construite sur &quot;PySpark&quot;. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l&#39;image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image du Docker est construite sur &quot;Spark&quot;. |

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
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `type` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image du Docker est construite sur &quot;Spark&quot;. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l&#39;image Docker à laquelle est liée une URL Docker. |
| `artifacts.default.image.executionType` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;image du Docker est construite sur &quot;Spark&quot;. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du nouveau moteur, y compris son identifiant unique (`id`). L&#39;exemple de réponse suivant est pour un moteur Python. Les `executionType` clés et `type` les clés changent en fonction de la POST fournie.

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

Une réponse réussie affiche une charge JSON contenant des informations sur le nouveau moteur créé. La `id` clé représente l&#39;identifiant unique du moteur et est requise dans le didacticiel suivant pour créer une instance MLInstance. Assurez-vous que l&#39;identifiant du moteur est enregistré avant de passer aux étapes suivantes.

## Étapes suivantes {#next-steps}

Vous avez créé un moteur à l&#39;aide de l&#39;API et un identifiant de moteur unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de moteur dans le didacticiel suivant lorsque vous apprendrez à [créer, former et évaluer un modèle à l&#39;aide de l&#39;API](./train-evaluate-model-api.md).

### Création d’un moteur avec un artefact binaire (obsolète) {#create-an-engine-with-a-binary-artifact-deprecated}

<!-- Will need to remove binary artifact documentation once the old flags are turned off -->

>[!CAUTION]
> Les artefacts binaires sont utilisés dans les anciennes recettes PySpark et Spark. Data Science Workspace prend désormais en charge les URL Docker pour toutes les recettes. Avec cette mise à jour, tous les moteurs sont désormais créés à l&#39;aide d&#39;une URL Docker. Consultez la section [URL du](#create-an-engine-with-a-docker-url) Docker de ce document. Les artefacts binaires sont définis pour être supprimés dans une version ultérieure.

Pour créer un moteur à l&#39;aide d&#39;un artefact `.jar` `.egg` binaire ou assemblé localement, vous devez indiquer le chemin d&#39;accès absolu au fichier d&#39;artefact binaire dans votre système de fichiers local. Pensez à naviguer jusqu&#39;au répertoire contenant l&#39;artefact binaire dans un environnement Terminal, puis exécutez la commande `pwd` Unix pour obtenir le chemin d&#39;accès absolu.

L’appel suivant crée un moteur avec un artefact binaire :

**Format d’API**

```http
POST /engines
```

**Requête**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

| Propriété | Description |
| -------  | ----------- |
| `engine.name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur de l&#39;espace de travail des sciences de données en tant que nom de la Recette. |
| `engine.description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur de l&#39;espace de travail des sciences de données comme description de la Recette. Ne supprimez pas cette propriété, laissez cette valeur être une chaîne vide si vous choisissez de ne pas fournir de description. |
| `engine.type` | Type d&#39;exécution du moteur. Cette valeur correspond à la langue dans laquelle l&#39;artefact binaire a été développé. Lorsque vous téléchargez un artefact binaire pour créer un moteur, `type` est soit `Spark` soit `PySpark`. |
| `defaultArtifact` | Chemin d’accès absolu au fichier d’artefact binaire utilisé pour créer le moteur. Veillez à inclure `@` avant le chemin d’accès au fichier. |

**Réponse**

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

Une réponse réussie affiche une charge JSON contenant des informations sur le nouveau moteur créé. La `id` clé représente l&#39;identifiant unique du moteur et est requise dans le didacticiel suivant pour créer une instance MLInstance. Assurez-vous que l&#39;identifiant du moteur est enregistré avant de passer aux étapes [](#next-steps)suivantes.