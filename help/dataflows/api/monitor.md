---
keywords: Experience Platform ; accueil ; rubriques populaires ; flux de données de surveillance ; api du service de flux ; service de flux
solution: Experience Platform
title: Surveillance des flux de données à l’aide de l’API du service de flux
topic-legacy: overview
type: Tutorial
description: Ce didacticiel décrit les étapes de surveillance des données d’exécution de flux afin de vérifier l’exhaustivité, les erreurs et les mesures à l’aide de l’API de service de flux.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 20%

---

# Surveillance des flux de données à l’aide de l’API du service de flux

Adobe Experience Platform permet l’assimilation de données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc. De plus, l&#39;Experience Platform permet l&#39;activation des données par des partenaires externes.

[!DNL Flow Service] est utilisée pour collecter et centraliser les données client provenant de diverses sources disparates à Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les sources et destinations prises en charge sont connectables.

Ce didacticiel décrit les étapes de surveillance des données d’exécution de flux afin de vérifier l’exhaustivité, les erreurs et les mesures à l’aide de [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Prise en main

Ce didacticiel nécessite que vous disposiez de la valeur ID d’un flux de données valide. Si vous ne disposez pas d’un ID de flux de données valide, sélectionnez le connecteur de votre choix dans le [aperçu des sources](../../sources/home.md) ou [aperçu des destinations](../../destinations/catalog/overview.md) et suivez les étapes décrites avant de tenter ce didacticiel.

Ce didacticiel nécessite également une bonne compréhension des composants suivants de Adobe Experience Platform :

- [Destinations](../../destinations/home.md) : Les destinations sont des intégrations préétablies avec les applications couramment utilisées qui permettent l’activation transparente des données de la plate-forme pour les campagnes marketing inter-canaux, les campagnes par courriel, la publicité ciblée et de nombreux autres cas d’utilisation.
- [Sources](../../sources/home.md) :  [!DNL Experience Platform] permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de  [!DNL Platform] services.
- [Sandbox](../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour surveiller les exécutions de flux à l&#39;aide de l&#39;API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

- `Content-Type: application/json`

## Exécutions du flux de surveillance

Une fois que vous avez effectué un flux de données, exécutez une demande de GET à l&#39;API [!DNL Flow Service].

**Format d’API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | Valeur `id` unique du flux de données à surveiller. |

**Requête**

La requête suivante récupère les spécifications d&#39;un flux de données existant.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des détails sur votre exécution de flux, y compris des informations sur sa date de création, ses connexions source et de cible, ainsi que l&#39;identifiant unique de l&#39;exécution de flux (`id`).

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `items` | Contient une charge utile unique de métadonnées associée à votre exécution de flux spécifique. |
| `metrics` | Caractéristiques des données dans l’exécution du flux. |
| `activities` | Indique comment les données sont transformées. |
| `durationSummary` | Début et heure de fin de l’exécution du flux. |
| `sizeSummary` | Volume des données en octets. |
| `recordSummary` | Nombre d’enregistrements des données. |
| `fileSummary` | Le fichier compte les données. |
| `fileSummary.extensions` | Contient des informations spécifiques à l’activité. Par exemple, `manifest` n&#39;est qu&#39;une partie de &quot;l&#39;Activité de promotion&quot; et est donc inclus avec l&#39;objet `extensions`. |
| `statusSummary` | Indique si l’exécution du flux est une réussite ou un échec. |

## Étapes suivantes

En suivant ce didacticiel, vous avez récupéré des mesures et des informations d’erreur sur votre flux de données à l’aide de l’API [!DNL Flow Service]. Vous pouvez maintenant continuer à surveiller votre flux de données, en fonction de votre calendrier d’assimilation, pour suivre son état et ses taux d’assimilation. Pour plus d&#39;informations sur la façon de surveiller les flux de données pour les sources, veuillez lire le [flux de données de surveillance pour les sources à l&#39;aide du didacticiel de l&#39;interface utilisateur](../ui/monitor-sources.md). Pour plus d&#39;informations sur la façon de surveiller les flux de données pour les destinations, consultez le [didacticiel de surveillance des flux de données pour les destinations à l&#39;aide de l&#39;interface utilisateur](../ui/monitor-destinations.md).
