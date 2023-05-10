---
keywords: Experience Platform;accueil;rubriques les plus consultées ; Tutoriels sur les API ; API des destinations de diffusion en continu ; Plateforme
solution: Experience Platform
title: Connexion aux destinations en continu et activation des données à l’aide de l’API Flow Service dans Adobe Experience Platform
description: Ce document couvre la création de destinations de diffusion en continu à l’aide de l’API Adobe Experience Platform.
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 57%

---

# Se connecter aux destinations de diffusion en continu et activer les données à l’aide de l’API Flow Service

>[!IMPORTANT]
> 
>Pour vous connecter à une destination, vous devez disposer de l’**[!UICONTROL autorisation de contrôle d’accès]** [Gérer les destinations](/help/access-control/home.md#permissions).
>
>Pour activer les données, vous avez besoin des **[!UICONTROL autorisations de contrôle d’accès]** pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et [Afficher les segments](/help/access-control/home.md#permissions).
>
>Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Ce tutoriel explique comment utiliser les appels API pour se connecter à vos données Adobe Experience Platform et créer une connexion à une destination de stockage dans le cloud en continu ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) ou [Centre d’événements Azure](../catalog/cloud-storage/azure-event-hubs.md)), créez un flux de données vers la nouvelle destination créée et activez les données vers la nouvelle destination créée.

Ce tutoriel utilise la méthode [!DNL Amazon Kinesis] destination dans tous les exemples, mais les étapes sont identiques pour [!DNL Azure Event Hubs].

![Présentation : étapes de création d’une destination de diffusion en continu et d’activation des segments](../assets/api/streaming-destination/overview.png)

Si vous préférez utiliser l’interface utilisateur de Platform pour vous connecter à une destination et activer des données, reportez-vous à la section [Connexion à une destination](../ui/connect-destination.md) et [Activation des données d’audience vers des destinations d’exportation de segments par flux](../ui/activate-segment-streaming-destinations.md) tutoriels.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] est le système d’enregistrement de l’emplacement et de la traçabilité des données dans Experience Platform.
* [Sandbox](../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour activer les données vers les destinations de diffusion en continu dans Platform.

### Collecte des informations d’identification requises

Pour suivre les étapes de ce tutoriel, vous devez disposer des informations d’identification suivantes, selon le type de destinations auxquelles vous vous connectez et activez des segments.

* Pour [!DNL Amazon Kinesis] connections : `accessKeyId`, `secretKey`, `region` ou `connectionUrl`
* Pour [!DNL Azure Event Hubs] connections : `sasKeyName`, `sasKey`, `namespace`

### Lecture d’exemples d’appels API {#reading-sample-api-calls}

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte de valeurs pour les en-têtes requis et facultatifs {#gather-values}

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Les ressources d’Experience Platform peuvent être isolées dans des sandbox virtuels spécifiques. Dans les requêtes aux API Platform, vous pouvez spécifier le nom et l’identifiant du sandbox dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Experience Platform, consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

### Documentation Swagger {#swagger-docs}

Ce tutoriel vous permet de trouver dans Swagger la documentation de référence relative à tous les appels API. Voir [Documentation de l’API Flow Service sur Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). Nous vous recommandons de consulter ce tutoriel et la page de documentation de Swagger en parallèle.

## Obtention de la liste des destinations de diffusion en continu disponibles {#get-the-list-of-available-streaming-destinations}

![Présentation des étapes de la destination : étape 1](../assets/api/streaming-destination/step1.png)

Dans un premier temps, vous devez décider vers quelle destination de diffusion en continu activer les données. Pour commencer, effectuez un appel pour demander une liste des destinations disponibles auxquelles vous pouvez vous connecter et activer des segments. Effectuez la requête GET suivante auprès du point d’entrée `connectionSpecs` pour obtenir une liste des destinations disponibles :

**Format d’API**

```http
GET /connectionSpecs
```

**Requête**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Réponse**

Une réponse réussie contient une liste des destinations disponibles et leurs identifiants uniques (`id`). Conservez la valeur de la destination que vous prévoyez d’utiliser, car elle sera requise dans les étapes suivantes. Par exemple, si vous souhaitez vous connecter et diffuser des segments vers [!DNL Amazon Kinesis] ou [!DNL Azure Event Hubs], recherchez le fragment de code suivant dans la réponse :

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Connexion à vos données Experience Platform {#connect-to-your-experience-platform-data}

![Présentation des étapes de la destination : étape 2](../assets/api/streaming-destination/step2.png)

Ensuite, vous devez vous connecter à vos données Experience Platform afin de pouvoir exporter des données de profil et les activer dans votre destination préférée. Il s’agit de deux sous-étapes présentées ci-dessous.

1. Tout d’abord, vous devez effectuer un appel pour autoriser l’accès à vos données dans Experience Platform, en établissant une connexion de base.
2. Ensuite, à l’aide de l’identifiant de connexion de base, vous passerez un autre appel au cours duquel vous créerez une connexion source, qui établira la connexion avec vos données Experience Platform.


### Autorisation d’accès à vos données dans Experience Platform

**Format d’API**

```http
POST /connections
```

**Requête**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: Utilisation de l’identifiant de spécification de connexion pour Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie contient l’identifiant unique de la connexion de base (`id`). Conservez cette valeur car elle est nécessaire à l’étape suivante pour créer la connexion source.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Connexion à vos données Experience Platform {#connect-to-platform-data}

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}` : utilisez l’identifiant que vous avez obtenu à l’étape précédente.
* `{CONNECTION_SPEC_ID}`: Utilisation de l’identifiant de spécification de connexion pour Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) pour la nouvelle connexion source au service de profil. Cela confirme que vous avez réussi à vous connecter à vos données Experience Platform. Conservez cette valeur car elle sera nécessaire lors d’une prochaine étape.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connexion à la destination de diffusion en continu {#connect-to-streaming-destination}

![Présentation des étapes de la destination : étape 3](../assets/api/streaming-destination/step3.png)

Au cours de cette étape, vous configurez une connexion à la destination de diffusion en continu de votre choix. Il s’agit de deux sous-étapes présentées ci-dessous.

1. Tout d’abord, vous devez effectuer un appel pour autoriser l’accès à la destination de diffusion en continu, en configurant une connexion de base.
2. Ensuite, à l’aide de l’identifiant de connexion de base, vous passerez un autre appel au cours duquel vous créerez une connexion cible, qui spécifie l’emplacement de votre compte de stockage où les données exportées seront transmises, ainsi que le format des données qui seront exportées.

### Autoriser l’accès à la destination de diffusion en continu

**Format d’API**

```http
POST /connections
```

**Requête**

>[!IMPORTANT]
>
>L’exemple ci-dessous comprend des commentaires de code précédés du préfixe `//`. Ces commentaires indiquent où différentes valeurs doivent être utilisées pour différentes destinations de diffusion en continu. Supprimez les commentaires avant d’utiliser le fragment de code.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}` : utilisez l’identifiant de spécification de connexion que vous avez obtenu lors de l’étape [Obtention de la liste des destinations disponibles](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: renseignez le nom de votre destination de diffusion en continu : `Aws Kinesis authentication credentials` ou `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *Pour [!DNL Amazon Kinesis] connexions.* Votre ID d’accès pour votre emplacement de stockage Amazon Kinesis.
* `{SECRET_KEY}`: *Pour [!DNL Amazon Kinesis] connexions.* Votre clé secrète pour votre emplacement de stockage Amazon Kinesis.
* `{REGION}`: *Pour [!DNL Amazon Kinesis] connexions.* La région de votre [!DNL Amazon Kinesis] compte où Platform diffusera vos données.
* `{SAS_KEY_NAME}`: *Pour [!DNL Azure Event Hubs] connexions.* Renseignez le nom de votre clé SAS. En savoir plus sur l’authentification à [!DNL Azure Event Hubs] avec les clés SAS dans [Documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *Pour [!DNL Azure Event Hubs] connexions.* Renseignez votre clé SAS. En savoir plus sur l’authentification à [!DNL Azure Event Hubs] avec les clés SAS dans [Documentation Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *Pour [!DNL Azure Event Hubs] connexions.* Renseignez les [!DNL Azure Event Hubs] Espace de noms dans lequel Platform diffusera vos données. Pour plus d’informations, voir [Création d’un espace de noms Event Hubs](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) dans le [!DNL Microsoft] documentation.

**Réponse**

Une réponse réussie contient l’identifiant unique de la connexion de base (`id`). Conservez cette valeur car elle est nécessaire à l’étape suivante pour créer une connexion cible.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Indication de l’emplacement de stockage et du format des données

**Format d’API**

```http
POST /targetConnections
```

**Requête**

>[!IMPORTANT]
>
>L’exemple ci-dessous comprend des commentaires de code précédés du préfixe `//`. Ces commentaires indiquent où différentes valeurs doivent être utilisées pour différentes destinations de diffusion en continu. Supprimez les commentaires avant d’utiliser le fragment de code.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}` : utilisez l’identifiant de connexion de base que vous avez obtenu à l’étape ci-dessus.
* `{CONNECTION_SPEC_ID}` : utilisez la spécification de connexion que vous avez obtenue lors de l’étape [Obtention de la liste des destinations disponibles](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *Pour [!DNL Amazon Kinesis] connexions.* Indiquez le nom de votre flux de données existant dans votre [!DNL Amazon Kinesis] compte . Platform exportera les données vers ce flux.
* `{REGION}`: *Pour [!DNL Amazon Kinesis] connexions.* La région de votre compte Kinesis Amazon dans laquelle Platform diffusera vos données.
* `{EVENT_HUB_NAME}`: *Pour [!DNL Azure Event Hubs] connexions.* Renseignez les [!DNL Azure Event Hub] Nom où Platform diffusera vos données. Pour plus d’informations, voir [Création d’un hub d’événements](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) dans le [!DNL Microsoft] documentation.

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) pour la nouvelle connexion cible à votre destination de diffusion en continu. Conservez cette valeur car elle sera nécessaire lors de prochaines étapes.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Création d’un flux de données

![Présentation des étapes de la destination : étape 4](../assets/api/streaming-destination/step4.png)

À l’aide des identifiants obtenus lors des étapes précédentes, vous pouvez maintenant créer un flux de données entre vos données Experience Platform et la destination vers laquelle vous activerez les données. Considérez cette étape comme la création du pipeline, par lequel les données seront ensuite acheminées, entre Experience Platform et la destination souhaitée.

Pour créer un flux de données, effectuez une requête POST, comme indiqué ci-après, tout en fournissant les valeurs mentionnées ci-dessous dans le payload.

Effectuez la requête POST suivante pour créer un flux de données.

**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`: L’identifiant de spécification de flux pour les destinations basées sur les profils est : `71471eba-b620-49e4-90fd-23f1fa0174d8`. Utilisez cette valeur dans l’appel .
* `{SOURCE_CONNECTION_ID}` : utilisez l’identifiant de connexion source obtenu à l’étape [Connexion à Experience Platform](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: Utilisez l’identifiant de connexion cible obtenu à l’étape [Connexion à la destination de diffusion en continu](#connect-to-streaming-destination).

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du nouveau flux de données et un `etag`. Notez les deux valeurs car vous en aurez besoin à l’étape suivante pour activer les segments.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Activation des données vers votre nouvelle destination {#activate-data}

![Présentation des étapes de la destination : étape 5](../assets/api/streaming-destination/step5.png)

Après avoir créé toutes les connexions et le flux de données, vous pouvez désormais activer vos données de profil vers la plateforme de diffusion en continu. Au cours de cette étape, vous sélectionnez les segments et les attributs de profil que vous envoyez à la destination et vous pouvez planifier et envoyer des données à la destination.

Pour activer les segments vers votre nouvelle destination, vous devez effectuer une opération JSON PATCH, comme dans l’exemple ci-dessous. Vous pouvez activer plusieurs segments et attributs de profil lors d’un seul appel. Pour en savoir plus sur le JSON PATCH, consultez la [spécification RFC](https://tools.ietf.org/html/rfc6902).

**Format d’API**

```http
PATCH /flows
```

**Requête**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/transformations/0/params/segmentSelectors/selectors/-",
    "value": {
      "type": "PLATFORM_SEGMENT",
      "value": {
        "name": "Name of the segment that you are activating",
        "description": "Description of the segment that you are activating",
        "id": "{SEGMENT_ID}"
      }
    }
  },
  {
    "op": "add",
    "path": "/transformations/0/params/profileSelectors/selectors/-",
    "value": {
      "type": "JSON_PATH",
      "value": {
        "operator": "EXISTS",
        "path": "{PROFILE_ATTRIBUTE}"
      }
    }
  }
]
```

| Propriété | Description |
| --------- | ----------- |
| `{DATAFLOW_ID}` | Dans l’URL, utilisez l’identifiant du flux de données que vous avez créé à l’étape précédente. |
| `{ETAG}` | Obtenez la variable `{ETAG}` de la réponse de l’étape précédente, [Création d’un flux de données](#create-dataflow). Le format de réponse de l’étape précédente comporte des guillemets d’échappement. Vous devez utiliser les valeurs sans séquence d’échappement dans l’en-tête de la requête. Voir l’exemple ci-dessous: <br> <ul><li>Exemple de réponse : `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Valeur à utiliser dans votre requête : `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> La valeur de la balise dʼentité est mise à jour à chaque mise à jour réussie d’un flux de données. |
| `{SEGMENT_ID}` | Indiquez l’identifiant du segment que vous souhaitez exporter vers cette destination. Pour récupérer les identifiants des segments que vous souhaitez activer, voir [récupérer une définition de segment](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) dans la référence de l’API Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Par exemple : `"person.lastName"` |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. Pour ajouter un segment à un flux de données, utilisez l’opération `add`. |
| `path` | Définit la partie du flux à mettre à jour. Lors de l’ajout d’un segment à un flux de données, utilisez le chemin spécifié dans l’exemple. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |
| `id` | Indiquez l’identifiant du segment que vous ajoutez au flux de données de destination. |
| `name` | *Facultatif*. Indiquez le nom du segment que vous ajoutez au flux de données de destination. Notez que ce champ n’est pas obligatoire et que vous pouvez ajouter un segment au flux de données de destination sans indiquer son nom. |

**Réponse**

Recherchez une réponse 202 OK. Aucun corps de réponse n’est renvoyé. Pour vérifier que la requête était correcte, reportez-vous à l’étape suivante : validation du flux de données.

## Validation du flux de données

![Présentation des étapes de la destination : étape 6](../assets/api/streaming-destination/step6.png)

La dernière étape du tutoriel consiste à vérifier que les segments et les attributs de profil ont été correctement mappés au flux de données.

Pour ce faire, effectuez la requête GET suivante :

**Format d’API**

```http
GET /flows
```

**Requête**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}` : utilisez le flux de données de l’étape précédente.
* `{ETAG}` : utilisez l’etag de l’étape précédente.

**Réponse**

La réponse renvoyée doit inclure dans le paramètre `transformations` les segments et les attributs de profil que vous avez envoyés à l’étape précédente. Voici un exemple de paramètre `transformations` dans la réponse :

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**Données exportées**

>[!IMPORTANT]
>
> Outre les attributs de profil et les segments à l’étape [Activation des données vers votre nouvelle destination](#activate-data), les données exportées dans [!DNL AWS Kinesis] et [!DNL Azure Event Hubs] inclura également des informations sur la carte des identités. Ceci représente les identités des profils exportés (par exemple [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), ID mobile, Google ID, adresse électronique, etc.). Voir un exemple ci-dessous.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Utilisation [!DNL Postman] collections pour se connecter aux destinations de diffusion en continu  {#collections}

Pour vous connecter aux destinations de diffusion en continu décrites dans ce tutoriel de manière plus rationnelle, vous pouvez utiliser [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] est un outil que vous pouvez utiliser pour effectuer des appels API et gérer les bibliothèques d’appels et d’environnements prédéfinis.

Pour ce tutoriel spécifique, les éléments suivants [!DNL Postman] des collections ont été jointes :

* [!DNL AWS Kinesis] [!DNL Postman] collection
* [!DNL Azure Event Hubs] [!DNL Postman] collection

Cliquez sur [here](../assets/api/streaming-destination/DestinationPostmanCollection.zip) pour télécharger l’archive de collections.

Chaque collection comprend les requêtes et variables d’environnement nécessaires, pour [!DNL AWS Kinesis], et [!DNL Azure Event Hub], respectivement.

### Comment utiliser la variable [!DNL Postman] collections {#how-to-use-postman-collections}

Pour vous connecter avec succès aux destinations à l’aide de la [!DNL Postman] collections, procédez comme suit :

* Télécharger et installer [!DNL Postman];
* [Télécharger](../assets/api/streaming-destination/DestinationPostmanCollection.zip) et décompressez les collections jointes ;
* Importez les collections de leurs dossiers correspondants dans [!DNL Postman];
* Renseignez les variables d’environnement conformément aux instructions de cet article.
* Exécutez la variable [!DNL API] de [!DNL Postman], en fonction des instructions de cet article.

## Gestion des erreurs d’API {#api-error-handling}

Les points de terminaison d’API de ce tutoriel suivent les principes généraux des messages d’erreur de l’API Experience Platform. Voir [Codes d’état d’API](/help/landing/troubleshooting.md#api-status-codes) et [erreurs d’en-tête de requête](/help/landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform pour plus d’informations sur l’interprétation des réponses d’erreur.

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez réussi à connecter Platform à l’une de vos destinations de diffusion en continu préférées et à configurer un flux de données vers la destination correspondante. Les données sortantes peuvent désormais être utilisées dans la destination pour les analyses client ou toute autre opération de données que vous souhaitez peut-être effectuer. Pour plus d’informations, consultez les pages suivantes :

* [Présentation des destinations](../home.md)
* [Présentation du catalogue des destinations](../catalog/overview.md)
