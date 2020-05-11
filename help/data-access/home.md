---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’accès aux données
topic: overview
translation-type: tm+mt
source-git-commit: d9aa21a7439a6c40f6f51dfbdf5c7b3690c4593a
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 4%

---


# Présentation de l’accès aux données

L’API d’accès aux données prend en charge Adobe Experience Platform en fournissant aux utilisateurs une interface RESTful axée sur la détectabilité et l’accessibilité des jeux de données imbriqués dans Experience Platform.

![Accès aux données sur la plateforme d’expérience](images/Data_Access_Experience_Platform.png)

## Référence de spécification d&#39;API

La documentation de référence de l’API Swagger se trouve [ici](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminologie

Description de certains termes couramment utilisés dans ce document.

| Terme | Description |
| ----- | ------------ |
| Jeu de données | Collection de données comprenant des schémas et des champs. |
| Lot | Ensemble de données collectées sur une période donnée et traitées ensemble en une seule unité. |

## Récupération de la liste des fichiers dans un lot

En utilisant un identifiant de lot (batchID), l&#39;API d&#39;accès aux données peut récupérer une liste de fichiers appartenant à ce lot particulier.

**Format d’API**

```http
GET /batches/{BATCH_ID}/files
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot spécifié. |

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

Le `"data"` tableau contient une liste de tous les fichiers du lot spécifié. Chaque fichier renvoyé comporte son propre identifiant (`{FILE_ID}`) unique contenu dans le `"dataSetFileId"` champ. Cet identifiant unique peut ensuite être utilisé pour accéder au fichier ou le télécharger.

| Propriété | Description |
| -------- | ----------- |
| `data.dataSetFileId` | ID de fichier pour chaque fichier du lot spécifié. |
| `data._links.self.href` | URL d’accès au fichier. |

## Accès et téléchargement de fichiers au sein d’un lot

En utilisant un identifiant de fichier (`{FILE_ID}`), l&#39;API d&#39;accès aux données permet d&#39;accéder aux détails spécifiques d&#39;un fichier, notamment son nom, sa taille en octets et un lien à télécharger.

La réponse contient un tableau de données. Selon que le fichier pointé par l&#39;ID est un fichier individuel ou un répertoire, le tableau de données renvoyé peut contenir une entrée unique ou une liste de fichiers appartenant à ce répertoire. Chaque élément de fichier inclut les détails du fichier.

**Format d’API**

```http
GET /files/{FILE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | Est égal à `"dataSetFileId"`, l’identifiant du fichier à accéder. |

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
| `data.name` | Nom du fichier (par exemple, profils.csv). |
| `data.length` | Taille du fichier (en octets). |
| `data._links.self.href` | URL de téléchargement du fichier. |

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

Lorsqu’un répertoire est renvoyé, il contient un tableau de tous les fichiers qu’il contient.

| Propriété | Description |
| -------- | ----------- |
| `data.name` | Nom du fichier (par exemple, profils.csv). |
| `data._links.self.href` | URL de téléchargement du fichier. |

## Accès au contenu d’un fichier

L&#39;API d&#39;accès aux données permet également d&#39;accéder au contenu d&#39;un fichier. Vous pouvez ensuite l’utiliser pour télécharger le contenu vers une source externe.

**Format d’API**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_NAME}` | Nom du fichier auquel vous tentez d’accéder. |

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
| `{FILE_ID}` | ID du fichier dans un jeu de données. |
| `{FILE_NAME}` | Nom complet du fichier (par exemple, profils.csv). |

**Réponse**

```
Contents of the file
```

## Exemples de code supplémentaires

Pour d&#39;autres exemples, reportez-vous au didacticiel [sur l&#39;accès aux](tutorials/dataset-data.md)données.

## S&#39;abonner aux événements d&#39;assimilation de données

La plate-forme met à disposition des événements spécifiques à forte valeur ajoutée pour l’abonnement via la console [de développement](https://www.adobe.com/go/devs_console_ui)Adobe. Par exemple, vous pouvez vous abonner à des événements d&#39;assimilation de données pour être averti des retards et des échecs potentiels. Pour plus d&#39;informations, consultez le didacticiel sur l&#39; [abonnement aux notifications](../ingestion/quality/subscribe-events.md) d&#39;assimilation de données.