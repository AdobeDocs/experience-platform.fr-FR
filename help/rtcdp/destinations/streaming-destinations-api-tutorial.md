---
keywords: Experience Platform;home;popular topics; API tutorials; streaming destinations API; Real-time CDP
solution: Experience Platform
title: Se connecter aux destinations de diffusion en continu et activer les données
topic: tutorial
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 2%

---


# Connectez-vous aux destinations de diffusion en continu et activez les données dans la plate-forme de données client en temps réel d’Adobe à l’aide d’API.

>[!NOTE]
>
>Les [!DNL Amazon Kinesis] destinations et les [!DNL Azure Event Hubs] destinations dans le CDP en temps réel d’Adobe sont actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Ce didacticiel explique comment utiliser les appels d’API pour se connecter à vos données Adobe Experience Platform, créer une connexion à une destination d’enregistrement de cloud de flux continu ([Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) ou [Azure Événement Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md)), créer un flux de données vers votre nouvelle destination créée et activer les données vers votre nouvelle destination créée.

Ce didacticiel utilise la [!DNL Amazon Kinesis] destination dans tous les exemples, mais les étapes sont identiques pour [!DNL Azure Event Hubs].

![Présentation : étapes de création d’une destination de diffusion en continu et d’activation de segments](/help/rtcdp/destinations/assets/flow-prelim.png)

Si vous préférez utiliser l’interface utilisateur du CDP en temps réel d’Adobe pour vous connecter à une destination et activer des données, consultez les didacticiels [Connexion d’une destination](../../rtcdp/destinations/connect-destination.md) et [Activation de profils et de segments à une destination](../../rtcdp/destinations/activate-destinations.md) .

## Prise en main

Ce guide nécessite une bonne compréhension des composants suivants d’Adobe Experience Platform :

* [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
* [Service](../../catalog/home.md)de catalogue : Le catalogue est le système d’enregistrement pour l’emplacement et le lignage des données dans la plate-forme d’expérience.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour activer les données vers les destinations de diffusion en flux continu dans Adobe CDP en temps réel.

### Collecte des informations d’identification requises

Pour suivre les étapes de ce didacticiel, vous devez disposer des informations d’identification suivantes, en fonction du type de destinations vers lesquelles vous connectez et activez les segments.

* Pour [!DNL Amazon Kinesis] les connexions : `accessKeyId`, `secretKey``region` ou `connectionUrl`
* Pour [!DNL Azure Event Hubs] les connexions : `sasKeyName`, `sasKey`, `namespace`

### Lecture des exemples d’appels d’API {#reading-sample-api-calls}

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes obligatoires et facultatifs {#gather-values}

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](/help/tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Les ressources de la plate-forme d’expérience peuvent être isolées dans des sandbox virtuels spécifiques. Dans les demandes aux API de plateforme, vous pouvez spécifier le nom et l’ID du sandbox dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name : `{SANDBOX_NAME}`

>[!Note] :
>Pour plus d’informations sur les sandbox dans Experience Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête de type de support supplémentaire :

* Content-Type : `application/json`

### Documentation Swagger {#swagger-docs}

Vous trouverez dans ce didacticiel de Swagger la documentation de référence correspondante pour tous les appels d’API. Voir https://platform.adobe.io/data/foundation/flowservice/swagger#/. Nous vous recommandons d’utiliser ce didacticiel et la page de documentation Swagger en parallèle.

## Obtenir la liste des destinations de diffusion en continu disponibles {#get-the-list-of-available-streaming-destinations}

![Etapes de destination - Présentation de l’étape 1](/help/rtcdp/destinations/assets/step1-create-streaming-destination-api.png)

Dans un premier temps, vous devez choisir la destination de diffusion en continu à laquelle activer les données. Pour commencer, effectuez un appel pour demander une liste de destinations disponibles à laquelle vous pouvez connecter et activer des segments. Effectuez la requête GET suivante sur le point de `connectionSpecs` terminaison pour renvoyer une liste de destinations disponibles :

**Format d’API**

```http
GET /connectionSpecs
```

**Requête**

```
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Réponse**

Une réponse réussie contient une liste de destinations disponibles et leurs identifiants uniques (`id`). Stockez la valeur de la destination que vous prévoyez d’utiliser, car elle sera nécessaire dans d’autres étapes. Par exemple, si vous souhaitez établir une connexion et diffuser des segments sur [!DNL Amazon Kinesis] ou [!DNL Azure Event Hubs], recherchez le fragment de code suivant dans la réponse :

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

## Se connecter à vos données de plateforme d’expérience {#connect-to-your-experience-platform-data}

![Etape de présentation des étapes de destination 2](/help/rtcdp/destinations/assets/step2-create-streaming-destination-api.png)

Ensuite, vous devez vous connecter à vos données de plateforme d’expérience afin de pouvoir exporter des données de profil et les activer dans votre destination préférée. Il s&#39;agit de deux étapes décrites ci-dessous.

1. Tout d’abord, vous devez effectuer un appel pour autoriser l’accès à vos données dans la plate-forme d’expérience, en configurant une connexion de base.
2. Ensuite, à l’aide de l’ID de connexion de base, vous effectuerez un autre appel au cours duquel vous créez une connexion source, qui établit la connexion aux données de votre plateforme d’expérience.


### Autoriser l’accès à vos données dans la plate-forme d’expérience

**Format d’API**

```http
POST /connections
```

**Requête**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME} \
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


* `{CONNECTION_SPEC_ID}`: Utilisez l&#39;identifiant de spécification de connexion pour Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie contient l&#39;identifiant unique (`id`) de la connexion de base. Conservez cette valeur comme elle est requise à l’étape suivante pour créer la connexion source.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Se connecter à vos données de plateforme d’expérience

**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Utilisez l’ID que vous avez obtenu à l’étape précédente.
* `{CONNECTION_SPEC_ID}`: Utilisez l&#39;identifiant de spécification de connexion pour Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Réponse**

Une réponse réussie renvoie l&#39;identifiant unique (`id`) de la nouvelle connexion source au service de Profil unifié. Ceci confirme que vous êtes connecté avec succès à vos données de plateforme d’expérience. Conservez cette valeur telle qu’elle est requise dans une étape ultérieure.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connect to streaming destination {#connect-to-streaming-destination}

![Etape de présentation des étapes de destination 3](/help/rtcdp/destinations/assets/step3-create-streaming-destination-api.png)

Au cours de cette étape, vous configurez une connexion à la destination de diffusion en continu de votre choix. Il s&#39;agit de deux étapes décrites ci-dessous.

1. Tout d’abord, vous devez effectuer un appel pour autoriser l’accès à la destination de diffusion en continu, en configurant une connexion de base.
2. Ensuite, à l’aide de l’ID de connexion de base, vous effectuerez un autre appel dans lequel vous créez une connexion de cible, qui spécifie l’emplacement dans votre compte d’enregistrement où les données exportées seront livrées, ainsi que le format des données qui seront exportées.

### Autoriser l’accès à la destination de diffusion en continu

**Format d’API**

```http
POST /connections
```

**Requête**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "your company's holiday campaign",
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

* `{CONNECTION_SPEC_ID}`: Utilisez l&#39;identifiant de spécification de connexion que vous avez obtenu lors de l&#39;étape [Obtenir la liste des destinations](#get-the-list-of-available-destinations)disponibles.
* `{AUTHENTICATION_CREDENTIALS}`: renseignez le nom de votre destination de diffusion en continu, par exemple : `Amazon Kinesis authentication credentials` ou `Azure Event Hubs authentication credentials`.
* `{ACCESS_ID}`: *Pour les connexions Amazon Kinesis.* Votre ID d’accès pour votre emplacement d’enregistrement Amazon Kinesis.
* `{SECRET_KEY}`: *Pour les connexions Amazon Kinesis.* Votre clé secrète pour l’emplacement de votre enregistrement Amazon Kinesis.
* `{REGION}`: *Pour les connexions Amazon Kinesis.* Région de votre compte Amazon Kinesis dans laquelle Adobe Real-time CDP diffusera vos données.
* `{SAS_KEY_NAME}`: *Pour les connexions Azure Événement Hubs.* Renseignez le nom de votre clé SAS. Découvrez comment vous authentifier à [!DNL Azure Event Hubs] l&#39;aide de clés SAS dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* `{SAS_KEY}`: *Pour les connexions Azure Événement Hubs.* Renseignez votre clé SAS. Découvrez comment vous authentifier à [!DNL Azure Event Hubs] l&#39;aide de clés SAS dans la documentation [](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Microsoft.
* `{EVENT_HUB_NAMESPACE}`: *Pour les connexions Azure Événement Hubs.* Renseignez l&#39;espace de nommage Azure Événement Hubs où Adobe Real-time CDP diffusera vos données. Pour plus d’informations, voir [Création d’un espace de nommage](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) Événement Hubs dans la documentation Microsoft.

**Réponse**

Une réponse réussie contient l&#39;identifiant unique (`id`) de la connexion de base. Conservez cette valeur comme elle est requise à l’étape suivante pour créer une connexion à une cible.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Définition de l’emplacement et du format des données de l’enregistrement

**Format d’API**

```http
POST /targetConnections
```

**Requête**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnection": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}",
        "namespace": "EVENT_HUB_NAMESPACE"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Utilisez l’ID de connexion de base que vous avez obtenu à l’étape ci-dessus.
* `{CONNECTION_SPEC_ID}`: Utilisez la spécification de connexion que vous avez obtenue lors de l&#39;étape [Obtenir la liste des destinations](#get-the-list-of-available-destinations)disponibles.
* `{NAME_OF_DATA_STREAM}`: *Pour les connexions Amazon Kinesis.* Indiquez le nom de votre flux de données existant dans votre compte Amazon Kinesis. Adobe Real-time CDP exportera les données dans ce flux.
* `{REGION}`: *Pour les connexions Amazon Kinesis.* Région de votre compte Amazon Kinesis dans laquelle Adobe Real-time CDP diffusera vos données.
* `{EVENT_HUB_NAME}`: *Pour les connexions Azure Événement Hubs.* Renseignez le nom Azure Événement Hub où Adobe Real-time CDP diffusera vos données. Pour plus d’informations, voir [Création d’un hub](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) de événement dans la documentation Microsoft.
* `{EVENT_HUB_NAMESPACE}`: *Pour les connexions Azure Événement Hubs.* Renseignez l&#39;espace de nommage Azure Événement Hubs où Adobe Real-time CDP diffusera vos données. Pour plus d’informations, voir [Création d’un espace de nommage](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) Événement Hubs dans la documentation Microsoft.

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion de cible à votre destination de diffusion en continu. Stocker cette valeur comme elle est requise dans les étapes ultérieures.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Création d’un flux de données

![Etapes de destination - présentation de l’étape 4](/help/rtcdp/destinations/assets/step4-create-streaming-destination-api.png)

A l’aide des identifiants que vous avez obtenus lors des étapes précédentes, vous pouvez maintenant créer un flux de données entre les données de votre plateforme d’expérience et la destination vers laquelle vous allez activer les données. Considérez cette étape comme la construction du pipeline, par lequel les données seront acheminées ultérieurement, entre la plateforme d’expérience et la destination souhaitée.

Pour créer un flux de données, exécutez une requête POST, comme illustré ci-dessous, tout en fournissant les valeurs mentionnées ci-dessous dans la charge utile.

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
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "Create dataflow to Amazon Kinesis/ Azure Event Hubs",
        "description": "This operation creates a dataflow to Amazon Kinesis/ Azure Event Hubs",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ]
    }
```

* `{FLOW_SPEC_ID}`: Utilisez le flux pour la destination de diffusion en continu à laquelle vous souhaitez vous connecter. Pour obtenir la spécification de flux, effectuez une opération GET sur le `flowspecs` point de terminaison. Voir la documentation de Swagger ici : https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. Dans la réponse, recherchez `upsTo` et copiez l’ID correspondant de la destination de diffusion en continu à laquelle vous souhaitez vous connecter.
* `{SOURCE_CONNECTION_ID}`: Utilisez l’ID de connexion source que vous avez obtenu à l’étape [Connexion à votre plateforme](#connect-to-your-experience-platform-data)d’expérience.
* `{TARGET_CONNECTION_ID}`: Utilisez l’ID de connexion à la cible que vous avez obtenu lors de l’étape [Connexion à la destination](#connect-to-streaming-destination)de diffusion en continu.

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé et un `etag`identifiant. Notez les deux valeurs. comme vous le ferez à l’étape suivante, pour activer les segments.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Activer les données vers votre nouvelle destination

![Etape de présentation des étapes de destination 5](/help/rtcdp/destinations/assets/step5-create-streaming-destination-api.png)

Après avoir créé toutes les connexions et le flux de données, vous pouvez désormais activer vos données de profil sur la plate-forme de diffusion en continu. Au cours de cette étape, vous sélectionnez les segments et les attributs de profil que vous envoyez à la destination et vous pouvez planifier et envoyer des données à la destination.

Pour activer des segments sur votre nouvelle destination, vous devez effectuer une opération JSON PATCH, comme dans l’exemple ci-dessous. Vous pouvez activer plusieurs segments et attributs de profil en un seul appel. Pour en savoir plus sur JSON PATCH, consultez la spécification [](https://tools.ietf.org/html/rfc6902)RFC.

**Format d’API**

```http
PATCH /flows
```

**Requête**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

* `{DATAFLOW_ID}`: Utilisez le flux de données que vous avez obtenu à l’étape précédente.
* `{ETAG}`: Utilisez la balise que vous avez obtenue à l’étape précédente.
* `{SEGMENT_ID}`: Indiquez l’ID de segment à exporter vers cette destination. Pour récupérer les ID de segment pour les segments que vous souhaitez activer, accédez à https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/, sélectionnez API **** Segmentation Service dans le menu de navigation de gauche et recherchez l’ `GET /segment/jobs` opération.
* `{PROFILE_ATTRIBUTE}`: Par exemple, `"person.lastName"`

**Réponse**

Recherchez une réponse 202 OK. Aucun corps de réponse n’est renvoyé. Pour vérifier que la requête était correcte, voir l’étape suivante, Valider le flux de données.

## Validation du flux de données

![Etape de présentation des étapes de destination 6](/help/rtcdp/destinations/assets/step6-create-streaming-destination-api.png)

En guise de dernière étape du didacticiel, vous devez vérifier que les segments et les attributs de profil ont bien été mappés au flux de données.

Pour valider ce paramètre, effectuez la requête GET suivante :

**Format d’API**

```http
GET /flows
```

**Requête**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Utilisez le flux de données de l’étape précédente.
* `{ETAG}`: Utilisez la balise de l’étape précédente.

**Réponse**

La réponse renvoyée doit inclure dans le `transformations` paramètre les segments et les attributs de profil que vous avez envoyés à l’étape précédente. Un exemple `transformations` de paramètre de la réponse peut se présenter comme suit :

```
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
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

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à connecter le CDP en temps réel à l’une de vos destinations de diffusion en continu préférées et à configurer un flux de données vers la destination correspondante. Les données sortantes peuvent désormais être utilisées dans la destination pour les analyses client ou toute autre opération de données que vous souhaitez peut-être effectuer. Consultez les pages suivantes pour plus de détails :

* [Présentation des destinations](../../rtcdp/destinations/destinations-overview.md)
* [Présentation du catalogue des destinations](../../rtcdp/destinations/destinations-catalog.md)