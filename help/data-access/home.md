---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation de l’accès aux données
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Présentation de l’accès aux données

L’API d’accès aux données prend en charge Adobe Experience Platform en fournissant aux utilisateurs une interface RESTful axée sur la détectabilité et l’accessibilité des jeux de données assimilés dans Experience Platform.

![Accès aux données sur la plateforme d’expérience](images/Data_Access_Experience_Platform.png)

## Référence de spécification API

La documentation de référence de l’API Swagger se trouve [ici](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml).

## Terminologie

Description de certains termes couramment utilisés dans ce.

| Terme | Description |
| ----- | ------------ |
| Jeu de données | Collection de données comprenant des  et des champs. |
| Lot | Ensemble de données collectées sur une période donnée et traitées ensemble en une seule unité. |

## Récupération de  de fichiers dans un lot

En utilisant un identifiant de lot (batchID), l&#39;API d&#39;accès aux données peut récupérer un de fichiers appartenant à ce lot particulier.

**Format API**

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

Le `"data"` tableau contient un  de tous les fichiers du lot spécifié. Chaque fichier renvoyé a son propre ID unique (`{FILE_ID}`) contenu dans le `"dataSetFileId"` champ. Cet identifiant unique peut ensuite être utilisé pour accéder au fichier ou le télécharger.

| Propriété | Description |
| -------- | ----------- |
| `data.dataSetFileId` | ID de fichier pour chaque fichier du lot spécifié. |
| `data._links.self.href` | URL d’accès au fichier. |

## Accès et téléchargement de fichiers dans un lot

En utilisant un identifiant de fichier (`{FILE_ID}`), l&#39;API d&#39;accès aux données permet d&#39;accéder à des détails spécifiques d&#39;un fichier, notamment son nom, sa taille en octets et un lien à télécharger.

La réponse contient un tableau de données. Selon que le fichier pointé par l’ID est un fichier individuel ou un répertoire, le tableau de données renvoyé peut contenir une entrée unique ou un de fichiers appartenant à ce répertoire. Chaque élément de fichier inclut les détails du fichier.

**Format API**

```http
GET /files/{FILE_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_ID}` | Est égal à `"dataSetFileId"`, l’ID du fichier à accéder. |

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
| `data.name` | Nom du fichier (ex. :.csv). |
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
| `data.name` | Nom du fichier (ex. :.csv). |
| `data._links.self.href` | URL de téléchargement du fichier. |

## Accès au contenu d’un fichier

L’API d’accès aux données permet également d’accéder au contenu d’un fichier. Vous pouvez ensuite l’utiliser pour télécharger le contenu vers une source externe.

**Format API**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| Propriété | Description |
| -------- | ----------- |
| `{FILE_NAME}` | Nom du fichier auquel vous essayez d’accéder. |

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
| `{FILE_NAME}` | Nom complet du fichier (par ex..csv). |

**Réponse**

```
Contents of the file
```

## Exemples de code supplémentaires

Pour d&#39;autres exemples, reportez-vous au didacticiel [sur l&#39;accès aux](tutorials/dataset-data.md)données.


## S&#39;abonner au d&#39;assimilation de données 

La plate-forme met des  spécifiques à valeur élevée à la disposition des  par l’intermédiaire de la console [d’E/S](https://console.adobe.io/)Adobe. Par exemple, vous pouvez vous abonner au d’assimilation de données pour être averti des retards et des échecs potentiels. Pour plus d’informations sur l’utilisation des  d’E/S Adobe, reportez-vous au guide de [prise en main](https://www.adobe.io/apis/experienceplatform/events/docs.html).