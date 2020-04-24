---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importer une recette assemblée (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Importer une recette assemblée (API)

Ce didacticiel utilise l’API [d’apprentissage automatique](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei pour créer un [moteur](../api/engines.md), également appelé Recette dans l’interface utilisateur.

Avant de commencer, il est important de noter que l’espace de travail Data Science Workspace d’Adobe Experience Platform utilise des termes différents pour faire référence à des éléments similaires dans l’API et l’interface utilisateur. Les termes de l’API sont utilisés dans ce didacticiel et le tableau suivant décrit les termes corrélés :

| Terme de l’interface utilisateur | Terme de l’API |
| ---- | ---- |
| Recette | [Moteur](../api/engines.md) |
| Modèle | [MLInstance](../api/mlinstances.md) |
| Formation et évaluation | [Expérience](../api/experiments.md) |
| Service | [MLService](../api/mlservices.md) |

Un moteur contient des algorithmes d’apprentissage automatique et une logique pour résoudre des problèmes spécifiques. Le diagramme ci-dessous présente une visualisation montrant le flux de travail API dans Data Science Workspace. Ce didacticiel se concentre sur la création d&#39;un moteur, le cerveau d&#39;un modèle d&#39;apprentissage automatique.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Prise en main

Ce didacticiel nécessite un fichier de recette empaqueté sous la forme d’un artefact binaire ou d’une URL de Docker. Suivez les fichiers source du [package dans un didacticiel de recette](./package-source-files-recipe.md) pour créer un fichier de recette empaqueté ou fournir le vôtre.

- Artefact binaire (obsolète) : L&#39;artefact binaire (ex. JAR, EGG) utilisé pour créer un moteur.
- `{DOCKER_URL}`: Adresse URL d’une image Docker d’un service intelligent.

Ce didacticiel nécessite que vous ayez suivi le didacticiel [](../../tutorials/authentication.md) Authentication to Adobe Experience Platform (Authentification vers Adobe Experience Platform) afin d’effectuer des appels aux API de plateforme. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- `{ACCESS_TOKEN}`: Votre valeur de jeton porteur spécifique fournie après l’authentification.
- `{IMS_ORG}`: Vos informations d’identification d’organisation IMS se trouvent dans votre intégration unique d’Adobe Experience Platform.
- `{API_KEY}`: Votre valeur de clé d’API spécifique a été trouvée dans votre intégration unique d’Adobe Experience Platform.

## Création d’un moteur

Selon le formulaire du fichier de recette compressé à inclure dans la demande d’API, un moteur est créé de l’une des deux manières suivantes :

- [Création d’un moteur avec une URL de Docker](#create-an-engine-with-a-docker-url)
- [Création d’un moteur avec un artefact binaire (obsolète)](#create-an-engine-with-a-binary-artifact-deprecated)

### Création d’un moteur avec une URL de Docker {#create-an-engine-with-a-docker-url}

Pour créer un moteur avec un fichier de recette compressé stocké dans un  Docker, vous devez indiquer l&#39;URL du Docker au fichier de recette compressé.

>[!CAUTION]
> Si vous utilisez Python ou R, utilisez la requête ci-dessous. Si vous utilisez PySpark ou Scala, utilisez l’exemple de requête PySpark/Scala situé sous l’exemple Python/R.

**Format API**

```http
POST /engines
```

**Demander Python/R**

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
| `engine.name` | Nom souhaité pour le moteur. La recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l’interface utilisateur de l’espace de travail des sciences de données comme nom de la recette. |
| `engine.description` | Description facultative du moteur. La recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l&#39;interface utilisateur de l&#39;espace de travail des sciences de données comme description de la recette. Ne supprimez pas cette propriété, laissez cette valeur être une chaîne vide si vous choisissez de ne pas fournir de description. |
| `engine.type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image du Docker est développée. Lorsqu’une URL de Docker est fournie pour créer un moteur, `type` est `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |
| `artifacts.default.image.location` | Tu `{DOCKER_URL}` vas ici. Une URL Docker complète possède la structure suivante : `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Nom supplémentaire du fichier image Docker. Ne supprimez pas cette propriété, laissez cette valeur être une chaîne vide si vous choisissez de ne pas fournir un nom de fichier image de Docker supplémentaire. |
| `artifacts.default.image.executionType` | Type d&#39;exécution de ce moteur. Cette valeur correspond à la langue dans laquelle l’image du Docker est développée. Lorsqu’une URL de Docker est fournie pour créer un moteur, `executionType` est `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |

**Demander PySpark**

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
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image Docker est construite sur &quot;PySpark&quot;. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l&#39;image du Docker à laquelle est liée une URL du Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image du Docker est construite sur &quot;Spark&quot;. |

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
| `name` | Nom souhaité pour le moteur. La Recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l&#39;interface utilisateur comme nom de la Recette. |
| `description` | Description facultative du moteur. La Recette correspondant à ce moteur héritera de cette valeur à afficher dans l&#39;interface utilisateur comme description de la Recette. Cette propriété est obligatoire. Si vous ne souhaitez pas fournir de description, définissez sa valeur sur une chaîne vide. |
| `type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image du Docker est construite sur &quot;Spark&quot;. |
| `mlLibrary` | Champ obligatoire lors de la création de moteurs pour les recettes PySpark et Scala. |
| `artifacts.default.image.location` | Emplacement de l&#39;image du Docker à laquelle est liée une URL du Docker. |
| `artifacts.default.image.executionType` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’image du Docker est construite sur &quot;Spark&quot;. |

**Réponse**

Une réponse réussie renvoie une charge utile contenant les détails du nouveau moteur, y compris son identifiant unique (`id`). L&#39;exemple de réponse suivant est pour un moteur Python. Les `executionType` clés et `type` les clés changent en fonction du POST fourni.

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

Une réponse réussie affiche une charge JSON contenant des informations sur le nouveau moteur créé. La `id` clé représente l&#39;identifiant unique du moteur et est requise dans le didacticiel suivant pour créer une instance MLInstance. Assurez-vous que l’identifiant du moteur est enregistré avant de passer aux étapes suivantes.

## Étapes suivantes {#next-steps}

Vous avez créé un moteur à l’aide de l’API et un identifiant de moteur unique a été obtenu dans le corps de la réponse. Vous pouvez utiliser cet identifiant de moteur dans le didacticiel suivant lorsque vous apprendrez à [créer, à former et à évaluer un modèle à l’aide de l’API](./train-evaluate-model-api.md).

### Création d’un moteur avec un artefact binaire (obsolète) {#create-an-engine-with-a-binary-artifact-deprecated}

<!-- Will need to remove binary artifact documentation once the old flags are turned off -->

>[!CAUTION]
> Les artefacts binaires sont utilisés dans les anciennes recettes PySpark et Spark. Data Science Workspace prend désormais en charge les URL du Docker pour toutes les recettes. Avec cette mise à jour, tous les moteurs sont désormais créés à l’aide d’une URL de Docker. Consultez la section [URL du](#create-an-engine-with-a-docker-url) Docker de ce. Les artefacts binaires sont définis pour être supprimés dans une version ultérieure.

Pour créer un moteur à l&#39;aide d&#39;un objet assemblé local `.jar` ou `.egg` binaire, vous devez indiquer le chemin d&#39;accès absolu au fichier d&#39;artefact binaire dans votre système de fichiers local. Pensez à accéder au répertoire contenant l&#39;artefact binaire dans un Terminal  et exécutez la commande `pwd` Unix pour le chemin absolu.

L’appel suivant crée un moteur avec un artefact binaire :

**Format API**

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
| `engine.name` | Nom souhaité pour le moteur. La recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l’interface utilisateur de l’espace de travail des sciences de données comme nom de la recette. |
| `engine.description` | Description facultative du moteur. La recette correspondant à ce moteur héritera de cette valeur pour être affichée dans l&#39;interface utilisateur de l&#39;espace de travail des sciences de données comme description de la recette. Ne supprimez pas cette propriété, laissez cette valeur être une chaîne vide si vous choisissez de ne pas fournir de description. |
| `engine.type` | Type d’exécution du moteur. Cette valeur correspond à la langue dans laquelle l’artefact binaire a été développé. Lorsque vous téléchargez un artefact binaire pour créer un moteur, `type` est soit `Spark` , soit `PySpark`. |
| `defaultArtifact` | Chemin d’accès absolu au fichier d’artefact binaire utilisé pour créer le moteur. Veillez à inclure `@` avant le chemin du fichier. |

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