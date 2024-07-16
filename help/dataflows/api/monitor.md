---
keywords: Experience Platform;accueil;rubriques les plus consultées;flux de données de surveillance;api de service de flux;service de flux
solution: Experience Platform
title: Surveiller les flux de données à l’aide de l’API Flow Service
type: Tutorial
description: Ce tutoriel décrit les étapes de surveillance de l’exhaustivité, des erreurs et des mesures relatives aux données d’exécution de flux à l’aide de l’API Flow Service.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 57%

---

# Surveiller les flux de données à l’aide de l’API Flow Service

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données à partir de diverses sources telles que des applications d’Adobe, du stockage dans le cloud, des bases de données, etc. En outre, Experience Platform permet l’activation des données auprès de partenaires externes.

[!DNL Flow Service] est utilisé pour collecter et centraliser des données client à partir de diverses sources disparates dans Adobe Experience Platform. Le service fournit une interface utilisateur et une API RESTful à partir desquelles toutes les sources et destinations prises en charge sont connectables.

Ce tutoriel décrit les étapes de surveillance des données d’exécution de flux pour l’exhaustivité, les erreurs et les mesures à l’aide de [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Commencer

Ce tutoriel nécessite que vous disposiez de la valeur d’identifiant d’un flux de données valide. Si vous ne disposez pas d’un identifiant de flux de données valide, sélectionnez votre connecteur de votre choix dans la [présentation des sources](../../sources/home.md) ou la [présentation des destinations](../../destinations/catalog/overview.md) et suivez les étapes décrites avant de lancer ce tutoriel.

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Destinations](../../destinations/home.md) : les destinations sont des intégrations préconfigurées des applications courantes qui permettent l’activation transparente des données de Platform pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
- [Sources ](../../sources/home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
- [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour surveiller les exécutions de flux à l’aide de l’API [!DNL Flow Service].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources qui se trouvent dans [!DNL Experience Platform], y compris celles liées à la [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

- `Content-Type: application/json`

## Surveiller les exécutions de flux

Une fois que vous avez créé un flux de données, effectuez une demande de GET à l’API [!DNL Flow Service].

**Format d’API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | Valeur unique `id` pour le flux de données que vous souhaitez surveiller. |

**Requête**

La requête suivante récupère les spécifications d’un flux de données existant.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des informations concernant votre exécution de flux, notamment : la date de création, les connexions source et cible ainsi que l’identifiant unique de l’exécution de flux (`id`).

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
            "imsOrgId": "{ORG_ID}",
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
| `items` | Contient une seule payload de métadonnées associée à votre exécution de flux spécifique. |
| `metrics` | Caractéristiques des données dans l’exécution du flux. |
| `activities` | Affiche la manière dont les données sont transformées. |
| `durationSummary` | Les heures de début et de fin de l’exécution du flux. |
| `sizeSummary` | Volume des données en octets. |
| `recordSummary` | Nombre d’enregistrements des données. |
| `fileSummary` | Le fichier compte les données. |
| `fileSummary.extensions` | Contient des informations spécifiques à l’activité. Par exemple, `manifest` ne fait partie que de l’&quot;activité de promotion&quot; et est donc inclus dans l’objet `extensions` . |
| `statusSummary` | Indique si l’exécution du flux est une réussite ou un échec. |

## Étapes suivantes

En suivant ce tutoriel, vous avez récupéré des mesures et des informations relatives aux erreurs sur votre flux de données à l’aide de l’API [!DNL Flow Service]. Vous pouvez maintenant continuer à surveiller votre flux de données, en fonction de votre planning d’ingestion, pour suivre son statut et ses taux d’ingestion. Pour plus d’informations sur la façon de surveiller les flux de données pour les sources, consultez le tutoriel [surveillance des flux de données pour les sources à l’aide de l’interface utilisateur](../ui/monitor-sources.md) . Pour plus d’informations sur la manière de surveiller les flux de données pour les destinations, consultez le tutoriel [surveillance des flux de données pour les destinations à l’aide de l’interface utilisateur](../ui/monitor-destinations.md) .
