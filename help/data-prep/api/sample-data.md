---
keywords: Experience Platform;accueil;rubriques les plus consultées;préparation de données;guide d’api;données d’exemple;
solution: Experience Platform
title: Exemple de point d’entrée de l’API Data
description: Vous pouvez utiliser le point d’entrée `/samples` dans l’API Adobe Experience Platform pour récupérer, créer, mettre à jour et valider par programmation les donnée d’exemple de mappage.
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 91%

---


# Exemple de point d’entrée de données

Des exemples de données peuvent être utilisés lors de la création d’un schéma pour votre jeu de mappages. Vous pouvez utiliser le point d’entrée `/samples` dans l’API Data Prep pour récupérer, créer et mettre à jour des données d’exemple par programmation.

## Liste des données d’exemple

Vous pouvez récupérer une liste de toutes les données d’exemple de mappage pour votre organisation en envoyant une requête de GET au point de terminaison `/samples`.

**Format d’API**

Le point d’entrée `/samples` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Actuellement, vous devez inclure les paramètres `start` et `limit` dans votre requête.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Paramètre | Description |
| --------- | ----------- |
| `{LIMIT}` | **Obligatoire**. Indique le nombre de données d’exemple de mappage renvoyées. |
| `{START}` | **Obligatoire**. Indique le décalage des pages de résultats. Pour obtenir la première page de résultats, définissez la valeur sur `start=0`. |

**Requête**

La requête suivante récupère les deux dernières données d’exemple de mappage au sein de votre organisation.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur les deux derniers objets des données d’exemple de mappage.

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| Propriété | Description |
| -------- | ----------- |
| `sampleData` | |
| `sampleType` | |

## Création de données d’exemples

Vous pouvez créer des données d’exemple en effectuant une requête POST sur le point d’entrée `/samples`.

```http
POST /samples
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur les données d’exemples que vous venez de créer.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Création de données d’exemple en chargeant un fichier

Vous pouvez créer des données d’exemple à l’aide d’un fichier en effectuant une requête POST sur le point d’entrée `/samples/upload`.

**Format d’API**

```http
POST /samples/upload
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur les données d’exemples que vous venez de créer.

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Recherche d’un objet de données d’exemple spécifique

Vous pouvez rechercher un objet spécifique de données d’exemple en fournissant son identifiant dans le chemin d’une requête GET vers le point d’entrée `/samples`.

**Format d’API**

```http
GET /samples/{SAMPLE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SAMPLE_ID}` | L’identifiant de l’objet de données d’exemple que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec les informations de l’objet de données d’exemple que vous souhaitez récupérer.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## Mise à jour des données d’exemple

Vous pouvez mettre à jour un objet spécifique de données d’exemple en fournissant son identifiant dans le chemin d’une requête PUT vers le point d’entrée `/samples`.

**Format d’API**

```http
PUT /samples/{SAMPLE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SAMPLE_ID}` | L’identifiant de l’objet de données d’exemple que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les données d’exemple spécifiées. Plus précisément, elle modifie le nom « Smith » en « Lee ».

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec des informations sur les données d’exemples mises à jour.

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
