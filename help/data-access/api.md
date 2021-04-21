---
keywords: Experience Platform ; accueil ; rubriques populaires ; accès aux données ; sdk python ; sdk spark ; api d’accès aux données ; exportation ; Exporter
solution: Experience Platform
title: Guide de l'API d'accès aux données
topic-legacy: developer guide
description: L'API d'accès aux données prend en charge Adobe Experience Platform en fournissant aux développeurs une interface RESTful axée sur la détectabilité et l'accessibilité des jeux de données assimilés dans l'Experience Platform.
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 78%

---

# Guide de l’API d’accès aux données

L&#39;API d&#39;accès aux données prend en charge Adobe Experience Platform en fournissant aux utilisateurs une interface RESTful axée sur la détectabilité et l&#39;accessibilité des jeux de données assimilés dans [!DNL Experience Platform].

![Data Access sur Experience Platform](images/Data_Access_Experience_Platform.png)

## Référence de spécification API

Vous trouverez [ici](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) la documentation de référence de l’API Swagger.

## Terminologie

Une description de certains des termes utilisés couramment tout au long de ce document.

| Terme | Description |
| ----- | ------------ |
| Jeu de données | Un ensemble de données qui inclut des schémas et des champs. |
| Lot | Un ensemble de données collectées sur une période donnée et traitées ensemble comme une seule unité. |

## Récupération de la liste de fichiers au sein d’un lot

En utilisant un identifiant de lot (batchID), l’API Data Access peut récupérer une liste des fichiers appartenant à un lot spécifique.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Le tableau `"data"` contient une liste de tous les fichiers au sein d’un lot spécifique. Chaque fichier renvoyé possède son propre ID unique (`{FILE_ID}`) contenu dans le champ `"dataSetFileId"`. Vous pouvez ensuite utiliser cet ID unique pour accéder au fichier ou le télécharger.

| Propriété | Description |
| -------- | ----------- |
| `data.dataSetFileId` | L’identifiant de fichier de chaque fichier du lot renseigné. |
| `data._links.self.href` | L’URL d’accès au fichier. |

## Accès et téléchargement de fichiers au sein d’un lot

En utilisant un identifiant de fichier (`{FILE_ID}`), l’API Data Access permet d’accéder aux détails spécifiques d’un fichier, notamment son nom, sa taille et un lien de téléchargement.

La réponse contiendra un tableau de données. Selon que le fichier désigné par l’identifiant est un fichier individuel ou un répertoire, le tableau de données renvoyé peut contenir une seule entrée ou une liste de fichiers appartenant à ce répertoire. Chaque élément du fichier inclura les détails du fichier.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data.name` | Nom du fichier (par ex. : profiles.csv). |
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
| `data.name` | Nom du fichier (par ex. : profiles.csv). |
| `data._links.self.href` | L’URL de téléchargement du fichier. |

## Accès aux contenus d’un fichier

L&#39;API [!DNL Data Access] peut également être utilisée pour accéder au contenu d&#39;un fichier. Vous pouvez ensuite l’utiliser pour télécharger les contenus vers une source externe.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | L’identifiant du fichier au sein d’un jeu de données. |
| `{FILE_NAME}` | Le nom complet du fichier (par ex. : profiles.csv). |

**Réponse**

`Contents of the file`

## Exemples de code supplémentaires

Pour consulter d’autres exemples, veuillez vous reporter au [tutoriel d’accès aux données](tutorials/dataset-data.md).

## Abonnement aux événements d’ingestion de données

[!DNL Platform] rend des événements spécifiques à forte valeur ajoutée disponibles pour l&#39;abonnement via la Console  [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr). Par exemple, vous pouvez vous abonner aux événements d’ingestion de données pour être informé des retards et des échecs potentiels. Pour plus d&#39;informations, consultez le didacticiel sur [l&#39;abonnement aux notifications d&#39;assimilation de données](../ingestion/quality/subscribe-events.md).
