---
keywords: Experience Platform;accueil;rubriques les plus consultées;accès aux données;sdk python;sdk spark;api d’accès aux données;exportation;exportation
solution: Experience Platform
title: Guide de l’API Data Access
description: L’API Data Access prend en charge Adobe Experience Platform en fournissant aux développeurs une interface RESTful axée sur la découverte et l’accessibilité des jeux de données ingérés dans Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 804eeb4ec976cf41fdd450bd8f307499c3ebae03
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 41%

---

# Guide de l’API Data Access

>[!IMPORTANT]
>
>L’API Data Access est désormais **obsolète**. Il est conseillé d’utiliser des destinations pour exporter des données à partir de Adobe Experience Platform. Pour plus d’informations, reportez-vous à la [documentation sur les destinations d’exportation de jeux de données](../destinations/destination-types.md#dataset-export-destinations).

L’API Data Access prend en charge Adobe Experience Platform en fournissant aux utilisateurs une interface RESTful axée sur la découverte et l’accessibilité des jeux de données ingérés dans [!DNL Experience Platform].

![Schéma de la manière dont l’accès aux données facilite la découverte et l’accessibilité des jeux de données ingérés dans Experience Platform.](images/Data_Access_Experience_Platform.png)

## Référence de spécification API

Reportez-vous à la [documentation de référence OpenAPI d’accès aux données](https://developer.adobe.com/experience-platform-apis/references/data-access/) pour afficher un format normalisé et lisible par ordinateur afin de faciliter l’intégration, le test et l’exploration.

## Terminologie {#terminology}

Le tableau fournit une description de certains termes couramment utilisés dans ce document.

| Terme | Description |
| ----- | ------------ |
| Jeu de données | Collection de données qui comprend un schéma et des champs. |
| Lot | Un ensemble de données collectées sur une période donnée et traitées ensemble comme une seule unité. |

## Récupération de la liste de fichiers au sein d’un lot {#retrieve-list-of-files-in-a-batch}

Pour récupérer une liste des fichiers appartenant à un lot spécifique, utilisez l’identifiant de lot (batchID) avec l’API Data Access.

**Format d’API**

```http
GET /batches/{BATCH_ID}/files
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot spécifié. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

Le tableau `"data"` contient une liste de tous les fichiers au sein d’un lot spécifique. Chaque fichier renvoyé possède son propre ID unique (`{FILE_ID}`) contenu dans le champ `"dataSetFileId"`. Vous pouvez utiliser cet identifiant unique pour accéder au fichier ou le télécharger.

| Propriété | Description |
| -------- | ----------- |
| `data.dataSetFileId` | L’identifiant de fichier de chaque fichier du lot renseigné. |
| `data._links.self.href` | L’URL d’accès au fichier. |

## Accès et téléchargement de fichiers au sein d’un lot

Pour accéder aux détails spécifiques d’un fichier, utilisez un identifiant de fichier (`{FILE_ID}`) avec l’API Data Access, notamment son nom, sa taille en octets et un lien à télécharger.

La réponse contient un tableau de données. Selon que le fichier désigné par l’identifiant est un fichier individuel ou un répertoire, le tableau de données renvoyé peut contenir une seule entrée ou une liste de fichiers appartenant à ce répertoire. Chaque élément de fichier inclut les détails du fichier.

**Format d’API**

```http
GET /files/{FILE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | Est égal à `"dataSetFileId"`, l’identifiant du fichier auquel vous essayez d’accéder. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse de fichier unique**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

| Propriété | Description |
| -------- | ----------- |
| `data.name` | Nom du fichier (par exemple, `profiles.csv`). |
| `data.length` | Taille du fichier (en octets). |
| `data._links.self.href` | L’URL de téléchargement du fichier. |

**Réponse du répertoire**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    }
  ],
  "_page": {
    "limit": 100,
    "count": 2
  }
}
```

Lorsqu’un répertoire est renvoyé, il contient un tableau de tous les fichiers se trouvant dans le répertoire.

| Propriété | Description |
| -------- | ----------- |
| `data.name` | Nom du fichier (par exemple, `profiles.csv`). |
| `data._links.self.href` | L’URL de téléchargement du fichier. |

## Accès aux contenus d’un fichier {#access-file-contents}

Vous pouvez également utiliser l’API [!DNL Data Access] pour accéder au contenu d’un fichier. Vous pouvez ensuite télécharger le contenu vers une source externe.

**Format d’API**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_NAME}` | Le nom du fichier auquel vous essayez d’accéder. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | L’identifiant du fichier au sein d’un jeu de données. |
| `{FILE_NAME}` | Nom complet du fichier (par exemple, `profiles.csv`). |

**Réponse**

`Contents of the file`

## Exemples de code supplémentaires

Pour d’autres exemples, reportez-vous au [ tutoriel sur l’accès aux données](tutorials/dataset-data.md).

## Abonnement aux événements d’ingestion de données {#subscribe-to-data-ingestion-events}

Vous pouvez vous abonner à des événements à valeur élevée spécifiques par le biais de [Adobe Developer Console](https://developer.adobe.com/console/). Par exemple, vous pouvez vous abonner aux événements d’ingestion de données pour être informé des retards et des échecs potentiels. Pour plus d’informations, consultez le tutoriel sur l’ [abonnement aux notifications d’événement d’Adobe](../observability/alerts/subscribe.md) .
