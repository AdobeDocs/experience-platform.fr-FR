---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Récupérer les lots ayant échoué
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Récupération des lots ayant échoué à l’aide de l’API

Adobe Experience Platform fournit deux méthodes pour télécharger et assimiler des données. Vous pouvez utiliser l’assimilation par lot, qui vous permet d’insérer leurs données à l’aide de différents types de fichiers (tels que les fichiers CSV), ou l’assimilation en flux continu, qui vous permet d’insérer leurs données dans la plate-forme à l’aide de points de fin de flux continu en temps réel.

Ce didacticiel décrit les étapes à suivre pour récupérer des informations sur un lot en échec à l’aide des API d’assimilation des données.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
- [Ingestion](../home.md)des données : Méthodes par lesquelles les données peuvent être envoyées à la plateforme d’expérience.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au Registre des  d’, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : `application/json`

### Exemple de lot échoué

Ce didacticiel utilisera des données d’exemple avec un horodatage mal formaté qui définit la valeur du mois sur **00**, comme illustré ci-dessous :

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

La charge ci-dessus ne sera pas correctement validée par rapport au XDM en raison d’un horodatage incorrect.

## Récupérer le lot ayant échoué

**Format API**

```http
GET /batches/{BATCH_ID}/failed
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot que vous recherchez. |

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Cache-Control: no-cache" \
  -H "Content-Type: application/json" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}
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

Avec la réponse ci-dessus, vous pouvez voir quels segments du lot ont réussi et échoué. À partir de cette réponse, vous pouvez voir que le fichier `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contient le lot ayant échoué.

## Téléchargement du lot en échec

Une fois que vous connaissez le fichier du lot qui a échoué, vous pouvez télécharger le fichier en échec et voir quel est le message d’erreur.

**Format API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot contenant le fichier en échec. |
| `{FAILED_FILE}` | Nom du fichier dont le formatage a échoué. |

**Requête**

La requête suivante vous permet de télécharger le fichier contenant des erreurs d’assimilation.

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Le lot assimilé précédent ayant une date et une heure incorrectes, l&#39;erreur de validation suivante s&#39;affiche.

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

Après avoir lu ce didacticiel, vous avez appris à récupérer des erreurs à partir de lots ayant échoué. Pour plus d&#39;informations sur l&#39;assimilation de lots, consultez le guide [du développeur sur l&#39;assimilation de](../batch-ingestion/overview.md)lots. Pour plus d’informations sur l’assimilation en flux continu, consultez le didacticiel [Création d’une connexion en flux continu](../tutorials/create-streaming-connection.md).

## Annexe

Cette section contient des informations sur d&#39;autres types d&#39;erreur d&#39;assimilation qui peuvent se produire.

### XDM mal formaté

Comme l’erreur d’horodatage de l’exemple précédent, ces erreurs sont dues à un format XDM incorrect. Ces messages d’erreur varient selon la nature du problème. Par conséquent, aucun exemple d’erreur spécifique ne peut être affiché.

### ID d&#39;organisation IMS manquant ou non valide

Cette erreur s’affiche si l’ID d’organisation IMS est absent de la charge utile.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

###  XDM manquante

Cette erreur s’affiche si le `schemaRef` pour `xdmMeta` est manquant.

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{IMS_ORG}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### Nom source manquant

Cette erreur s’affiche si l’en-tête `source` de l’en-tête manque `name`.

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

### Entité XDM manquante

Cette erreur s’affiche s’il n’y a pas de `xdmEntity` présence.

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```
