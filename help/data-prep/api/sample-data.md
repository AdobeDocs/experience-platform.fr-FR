---
keywords: Experience Platform ; accueil ; rubriques populaires ; prép. de données ; guide d’api ; données d’exemple ;
solution: Experience Platform
title: Exemple de point de terminaison de l’API de données
topic-legacy: sample data
description: 'Vous pouvez utiliser le point de terminaison `/samples’ dans l’API Adobe Experience Platform pour récupérer, créer, mettre à jour et valider par programmation les données d’exemple de mappage. '
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 8%

---


# Exemple de point de terminaison de données

Des exemples de données peuvent être utilisés lors de la création d’un schéma pour votre jeu de mappages. Vous pouvez utiliser le point de terminaison `/samples` dans l’API d’aperçu des données pour récupérer, créer et mettre à jour par programmation des données d’exemple.

## Données d’exemple de liste

Vous pouvez récupérer une liste de toutes les données d’exemple de mappage pour votre organisation IMS en adressant une demande de GET au point de terminaison `/samples`.

**Format d’API**

Le point de terminaison `/samples` prend en charge plusieurs paramètres de requête pour vous aider à filtrer vos résultats. Actuellement, vous devez inclure les paramètres `start` et `limit` dans votre requête.

```http
GET /samples?limit={LIMIT}&start={START}
```

| Paramètre | Description |
| --------- | ----------- |
| `{LIMIT}` | **Obligatoire**. Indique le nombre de données d’exemple renvoyées par le mappage. |
| `{START}` | **Obligatoire**. Indique le décalage des pages de résultats. Pour obtenir la première page de résultats, définissez la valeur sur `start=0`. |

**Requête**

La requête suivante récupère les deux dernières données d&#39;exemple de mappage au sein de votre organisation IMS.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur les deux derniers objets de mappage des données d’exemple.

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
| `sampleData` |  |
| `sampleType` |  |

## Création de données d’exemple

Vous pouvez créer des données d’exemple en adressant une requête de POST au point de terminaison `/samples`.

```http
POST /samples
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur vos données d’exemple nouvellement créées.

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

## Créer des données d’exemple en téléchargeant un fichier

Vous pouvez créer des données d’exemple à l’aide d’un fichier en adressant une requête de POST au point de terminaison `/samples/upload`.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur vos données d’exemple nouvellement créées.

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

## Rechercher un objet de données d’exemple spécifique

Vous pouvez rechercher un objet spécifique de données d’exemple en fournissant son identifiant dans le chemin d’une demande de GET au point de terminaison `/samples`.

**Format d’API**

```http
GET /samples/{SAMPLE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SAMPLE_ID}` | ID de l’objet de données d’exemple que vous souhaitez récupérer. |

**Requête**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec les informations de l’exemple de données que vous souhaitez récupérer.

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

Vous pouvez mettre à jour un objet de données d’exemple spécifique en indiquant son identifiant dans le chemin d’une requête de PUT vers le point de terminaison `/samples`.

**Format d’API**

```http
PUT /samples/{SAMPLE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{SAMPLE_ID}` | ID de l’objet de données d’exemple que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour les données d’exemple spécifiées. Plus précisément, il met à jour le nom de famille de &quot;Smith&quot; en &quot;Lee&quot;.

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 200 avec des informations sur les données d’exemple mises à jour.

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
