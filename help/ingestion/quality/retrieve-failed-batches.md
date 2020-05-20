---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Récupérer les lots ayant échoué
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---


# Récupération de lots ayant échoué à l’aide de l’API

Adobe Experience Platform fournit deux méthodes pour télécharger et ingérer des données. Vous pouvez utiliser l’assimilation par lot, qui vous permet d’insérer leurs données à l’aide de différents types de fichiers (tels que les fichiers CSV), ou l’assimilation par flux continu, qui vous permet d’insérer leurs données sur la plate-forme à l’aide de points de terminaison de flux continu en temps réel.

Ce didacticiel décrit les étapes à suivre pour récupérer des informations sur un lot en échec à l&#39;aide des API d&#39;importation de données.

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
- [Ingestion](../home.md)des données : Méthodes par lesquelles les données peuvent être envoyées à la plateforme d’expérience.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au Registre des Schémas, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : `application/json`

### Exemple de lot échoué

Ce didacticiel utilisera des données d’exemple avec un horodatage mal formaté qui définit la valeur du mois à **00**, comme indiqué ci-dessous :

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

La charge utile ci-dessus ne sera pas correctement validée par rapport au schéma XDM en raison d’un horodatage incorrect.

## Récupérer le lot en échec

**Format d’API**

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

Avec la réponse ci-dessus, vous pouvez voir quels segments du lot ont réussi et échoué. A partir de cette réponse, vous pouvez voir que le fichier `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` contient le lot qui a échoué.

## Téléchargement du lot en échec

Une fois que vous connaissez le fichier du lot qui a échoué, vous pouvez télécharger le fichier qui a échoué et voir quel est le message d’erreur.

**Format d’API**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| Propriété | Description |
| -------- | ----------- |
| `{BATCH_ID}` | ID du lot contenant le fichier en échec. |
| `{FAILED_FILE}` | Nom du fichier dont la mise en forme a échoué. |

**Requête**

La requête suivante vous permet de télécharger le fichier qui contient des erreurs d&#39;assimilation.

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

Comme le lot assimilé précédent avait une date/heure non valide, l&#39;erreur de validation suivante s&#39;affiche.

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

Après avoir lu ce didacticiel, vous avez appris à récupérer les erreurs des lots en échec. Pour plus d&#39;informations sur l&#39;assimilation de lots, consultez le guide [de développement sur l&#39;assimilation de](../batch-ingestion/overview.md)lots. Pour plus d’informations sur l’assimilation en flux continu, consultez le didacticiel [](../tutorials/create-streaming-connection.md)Création d’une connexion en flux continu.

## Annexe

Cette section contient des informations sur d&#39;autres types d&#39;erreur d&#39;assimilation qui peuvent se produire.

### XDM mal formaté

Comme pour l’erreur d’horodatage de l’exemple précédent, ces erreurs sont dues à un format XDM incorrect. Ces messages d&#39;erreur varient en fonction de la nature du problème. Par conséquent, aucun exemple d’erreur spécifique ne peut être affiché.

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

### schéma XDM manquant

Cette erreur s’affiche si le `schemaRef` pour le `xdmMeta` est manquant.

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
