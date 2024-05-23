---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion de données;lot;activer le jeu de données;présentation de l’ingestion par lots;présentation de l’ingestion par lots;présentation de l’ingestion par lots
solution: Experience Platform
title: Présentation de l’API Batch Ingestion
description: L’API Batch Ingestion de Adobe Experience Platform vous permet d’ingérer des données dans Platform sous forme de fichiers de lot. Les données en cours d’ingestion peuvent être les données de profil d’un fichier plat dans un système CRM (par exemple un fichier Parquet) ou les données conformes à un schéma connu dans le registre Experience Data Model (XDM).
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
source-git-commit: 6cd4bff07d042401d4ebc90d6fc2e70a1f8a7cb0
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 65%

---

# Présentation de l’API d’ingestion par lots

L’API Batch Ingestion de Adobe Experience Platform vous permet d’ingérer des données dans Platform sous forme de fichiers de lot. Les données en cours d’ingestion peuvent être des données de profil provenant d’un fichier plat (un fichier Parquet, par exemple) ou des données conformes à un schéma connu dans la variable [!DNL Experience Data Model] Registre (XDM).

La variable [Référence de l’API Batch Ingestion](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) fournit des informations supplémentaires sur ces appels API.

Le diagramme suivant décrit le processus d’ingestion par lots :

![](../images/batch-ingestion/overview/batch_ingestion.png)

## Commencer

Les points de terminaison d’API utilisés dans ce guide font partie du [API Batch Ingestion](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

### Conditions préalables de [!DNL Data Ingestion]

- Les données à charger doivent être au format Parquet ou JSON.
- Un jeu de données créé dans la variable [[!DNL Catalog services]](../../catalog/home.md).
- Le contenu du fichier Parquet doit correspondre à un sous-ensemble du schéma du jeu de données dans lequel il est chargé.
- Obtenez votre jeton d’accès unique après l’authentification.

### Bonnes pratiques d’ingestion par lots

- La taille du lot recommandée est comprise entre 256 Mo et 100 Go.
- Chaque lot doit contenir au maximum 1 500 fichiers.

### Contraintes d’ingestion par lots

L’ingestion de données par lots présente certaines contraintes :

- Nombre maximal de fichiers par lot : 1 500
- Taille maximale du lot : 100 Go
- Nombre maximal de propriétés ou de champs par ligne : 10 000
- Nombre maximal de lots par minute sur le lac de données, par utilisateur : 138

>[!NOTE]
>
>Pour charger un fichier de plus de 512 Mo, vous devez le diviser en petits blocs. Les instructions de chargement d’un fichier volumineux sont présentées dans la section [section de chargement de fichiers volumineux de ce document](#large-file-upload---create-file).

### Types

Lors de l’ingestion de données, il est important de comprendre comment [!DNL Experience Data Model] Les schémas (XDM) fonctionnent. Pour plus d’informations sur la façon dont les types de champs XDM sont associés à différents formats, reportez-vous au [guide de développement du registre des schémas](../../xdm/api/getting-started.md).

L’ingestion de données offre une certaine flexibilité : si un type ne correspond pas à ce qui se trouve dans le schéma cible, les données sont converties vers le type cible exprimé. Si cette conversion est impossible, le lot échouera avec `TypeCompatibilityException`.

Par exemple, ni JSON ni CSV ne comportent de `date` ou `date-time` type. Par conséquent, ces valeurs sont exprimées à l’aide de [Chaînes formatées ISO 8601](https://www.iso.org/fr/iso-8601-date-and-time-format.html) (&quot;2018-07-10T15:05:59.000-08:00&quot;) ou heure Unix formatée en millisecondes (1531263959000) et convertie au moment de l’ingestion vers le type XDM cible.

Le tableau ci-dessous illustre les conversions prises en charge lors de l’ingestion de données.

| Entrant (ligne) / Cible (colonne) | Chaîne | Octet | Court | Entier | Long | Double | Date | Date et heure | Objet | Map |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Chaîne | X | X | X | X | X | X | X | X |   |   |
| Octet | X | X | X | X | X | X |   |   |   |   |
| Court | X | X | X | X | X | X |   |   |   |   |
| Entier | X | X | X | X | X | X |   |   |   |   |
| Long | X | X | X | X | X | X | X | X |   |   |
| Double | X | X | X | X | X | X |   |   |   |   |
| Date |   |   |   |   |   |   | X |   |   |   |
| Date et heure |   |   |   |   |   |   |   | X |   |   |
| Objet |   |   |   |   |   |   |   |   | X | X |
| Map |   |   |   |   |   |   |   |   | X | X |

>[!NOTE]
>
>Les booléens et les tableaux ne peuvent pas être convertis en d’autres types.

## Utilisation de l’API

La variable [!DNL Data Ingestion] L’API vous permet d’ingérer des données sous forme de lots (une unité de données composée d’un ou de plusieurs fichiers à ingérer en une seule unité) dans [!DNL Experience Platform] en trois étapes de base :

1. Création d’un nouveau filtre.
2. Chargez des fichiers vers un jeu de données spécifique qui correspond au schéma XDM des données.
3. Signale la fin du lot.

## Création d’un lot

Avant de pouvoir ajouter des données à un jeu de données, elles doivent être liées à un lot, qui sera ensuite chargé dans un jeu de données spécifié.

```http
POST /batches
```

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `datasetId` | Identifiant du jeu de données dans lequel charger les fichiers. |

**Réponse**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{ORG_ID}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| Propriété | Description |
| -------- | ----------- |
| `id` | Identifiant du lot qui vient d’être créé (utilisé dans les demandes ultérieures). |
| `relatedObjects.id` | Identifiant du jeu de données dans lequel charger les fichiers. |

## Chargement des fichiers

Une fois le nouveau lot créé avec succès pour le chargement, les fichiers peuvent désormais être chargés dans le jeu de données spécifique.

Vous pouvez charger des fichiers à l’aide de l’API Small File Upload. Cependant, si vos fichiers sont trop volumineux et que la limite de la passerelle est dépassée (par exemple, délais d’expiration étendus, demandes de taille de corps dépassés et autres contraintes), vous pouvez passer à l’API Large File Upload. Cette API charge le fichier par blocs et assemble les données à l’aide de l’appel de l’API Large File Upload Complete .

>[!NOTE]
>
>L’ingestion par lots peut être utilisée pour mettre à jour progressivement les données dans la banque de profils. Pour plus d’informations, voir la section sur [mise à jour d’un lot](#patch-a-batch) dans le [guide de développement de l’ingestion par lots](api-overview.md).

>[!INFO]
>
>Les exemples ci-dessous utilisent la méthode [Apache Parquet](https://parquet.apache.org/docs/) format de fichier. Vous trouverez un exemple d’utilisation du format de fichier JSON dans le [guide de développement de l’ingestion par lots](api-overview.md).

### Chargement de petits fichiers

Une fois un lot créé, les données peuvent être chargées vers un jeu de données préexistant.  Le fichier en cours de chargement doit correspondre à son schéma XDM référencé.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot. |
| `{DATASET_ID}` | Identifiant du jeu de données dans lequel charger les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin et nom du fichier à charger dans le jeu de données. |

**Réponse**

```JSON
#Status 200 OK, with empty response body
```

### Chargement de fichiers volumineux - création d’un fichier

Pour charger un fichier volumineux, le fichier doit être divisé en petits blocs qui seront chargés un par un.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot. |
| `{DATASET_ID}` | Identifiant du jeu de données qui ingère les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

```JSON
#Status 201 CREATED, with empty response body
```

### Chargement de fichiers volumineux - chargement des parties suivantes

Une fois le fichier créé, tous les blocs suivants peuvent être chargés en exécutant des requêtes PATCH répétées, une pour chaque section du fichier.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot. |
| `{DATASET_ID}` | Identifiant du jeu de données dans lequel charger les fichiers. |
| `{FILE_NAME}` | Nom du fichier tel qu’il sera affiché dans le jeu de données. |

**Requête**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | Chemin et nom du fichier à charger dans le jeu de données. |

**Réponse**

```JSON
#Status 200 OK, with empty response
```

## Signalement de la fin du lot

Une fois que tous les fichiers ont été chargés dans le lot, il peut être marqué comme étant terminé. En procédant comme suit, la variable [!DNL Catalog] Les entrées DataSetFile sont créées pour les fichiers terminés et associées au lot généré ci-dessus. Le lot de [!DNL Catalog] est marqué comme réussi, ce qui déclenche les flux en aval afin d’ingérer les données disponibles.

**Requête**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot à charger dans le jeu de données. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Réponse**

```JSON
#Status 200 OK, with empty response
```

## Vérifier l’état du lot

En attendant que les fichiers soient chargés dans le lot, vous pouvez vérifier l’état du lot pour voir sa progression.

**Format d’API**

```http
GET /batch/{BATCH_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | Identifiant du lot en cours d’analyse. |

**Requête**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{ORG_ID}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `{USER_ID}` | Identifiant de l’utilisateur qui a créé ou mis à jour le lot. |

Le champ `"status"` indique l’état actuel du lot demandé. Les lots peuvent avoir l’un des états suivants :

## États de l’ingestion par lot

| État | Description |
| ------ | ----------- |
| Abandonné | Le lot ne s’est pas terminé dans le délai prévu. |
| Interrompu | Une opération pour interrompre l’opération a été **explicitement** appelée (via l’API Batch Ingest) pour le lot spécifié. Une fois que le lot est à l’état &quot;Chargé&quot;, il ne peut pas être abandonné. |
| Actif | Le lot a été converti avec succès et est disponible pour la consommation en aval. Cet état peut être interchangeable avec &quot;Succès&quot;. |
| Supprimé | Les données du lot ont été entièrement supprimées. |
| Échoué | État final résultant d’une configuration incorrecte et/ou de mauvaises données. Les données d’un lot qui a échoué **ne s’affichent pas**. Cet état peut être utilisé de manière interchangeable avec &quot;Échec&quot;. |
| Inactif | La conversion du lot a réussi, mais a été annulée ou a expiré. Le lot n’est plus disponible pour la consommation en aval. |
| Chargé | Les données du lot sont transférées et le lot est prêt pour la promotion. |
| Chargement | Les données de ce lot sont en cours de chargement et le lot **n’est actuellement pas** prêt à être converti. |
| Nouvelle tentative | Les données de ce lot sont en cours de traitement. Cependant, en raison d’une erreur système ou transitoire, le lot a échoué. Par conséquent, une nouvelle tentative pour ce lot est en cours. |
| Évalué | La phase d’évaluation du processus de promotion d’un lot est terminée et la tâche d’ingestion a été exécutée. |
| Évaluation | Les données du lot sont en cours de traitement. |
| Bloqué | Les données du lot sont en cours de traitement. Toutefois, la promotion par lot est bloquée après un certain nombre de tentatives. |
