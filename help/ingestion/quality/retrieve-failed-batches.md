---
keywords: Experience Platform;accueil;rubriques les plus consultées;récupérer les lots en échec;lots en échec;ingestion par lots;ingestion par lots;lots en échec;Obtenir les lots en échec;obtenir les lots en échec;Télécharger les lots en échec;télécharger les lots en échec;télécharger les lots en échec;télécharger les lots en échec
solution: Experience Platform
title: Récupération de lots en échec à l’aide de l’API Data Access
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour récupérer des informations sur un lot en échec à l’aide des API Data Ingestion.
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 79%

---

# Récupération des lots en échec à l’aide de l’API Data Access

Adobe Experience Platform propose deux méthodes de chargement et d’ingestion de données. Vous pouvez utiliser soit l’ingestion par lots, qui vous permet d’insérer leurs données à l’aide de différents types de fichiers (tels que les fichiers CSV), soit l’ingestion par flux, qui vous permet d’insérer leurs données vers [!DNL Platform] à l’aide de points de terminaison en continu en temps réel.

Ce tutoriel décrit les étapes à suivre pour récupérer des informations sur un lot en échec à l’aide des API [!DNL Data Ingestion].

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Data Ingestion]](../home.md) : méthodes par lesquelles les données peuvent être envoyées à [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Schema Registry], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- `Content-Type: application/json`

### Échantillon de lot en échec

Ce tutoriel utilisera des données d’exemple avec un horodatage mal formaté qui définit la valeur du mois sur **00**, comme illustré ci-dessous :

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

Le payload ci-dessus ne sera pas correctement validé par rapport au schéma XDM en raison de l’horodatage incorrect.

## Récupération du lot en échec

**Format d’API**

```http
GET /batches/{BATCH_ID}/failed
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot que vous recherchez. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
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

Grâce à la réponse ci-dessus, vous pouvez voir quels blocs du lot ont réussi et quels blocs ont échoué. À partir de cette réponse, vous pouvez voir que le fichier `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contient le lot en échec.

## Téléchargement du lot en échec

Une fois que vous connaissez le fichier du lot qui a échoué, vous pouvez télécharger le fichier en échec et consulter le message d’erreur.

**Format d’API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | L’identifiant du lot contenant le fichier en échec. |
| `{FAILED_FILE}` | Le nom du fichier dont le formatage a échoué. |

**Requête**

La requête suivante vous permet de télécharger le fichier contenant des erreurs d’ingestion.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La date et l’heure du lot ingéré précédent étant incorrectes, l’erreur de validation suivante s’affichera.

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## Étapes suivantes

Après avoir lu ce tutoriel, vous avez appris à récupérer des erreurs à partir de lots en échec. Pour plus d’informations sur l’ingestion par lot, consultez le [guide de développement de l’ingestion par lots](../batch-ingestion/overview.md). Pour plus d’informations sur l’ingestion par flux, consultez le [tutoriel de création d’une connexion en continu](../tutorials/create-streaming-connection.md).

## Annexe

Cette section contient des informations sur d’autres types d’erreurs d’ingestion pouvant se produire.

### XDM mal formaté

Comme l’erreur d’horodatage de l’exemple précédent, ces erreurs sont dues à un XDM mal formaté. Ces messages d’erreur varient selon la nature du problème. Par conséquent, aucun exemple d’erreur spécifique ne peut être affiché.

### ID d’organisation absent ou non valide

Cette erreur s’affiche si l’ID d’organisation est absent de la charge utile n’est pas valide.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### Schéma XDM absent

Cette erreur s’affiche si le `schemaRef` pour `xdmMeta` est absent.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Nom de la source absent

Cette erreur s’affiche si le `source` de l’en-tête n’a pas de `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### Entité XDM absente

Cette erreur s’affiche si aucune `xdmEntity` n’est renseignée.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
