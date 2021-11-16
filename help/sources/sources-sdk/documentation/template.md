---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Modèle de libre-service de documentation
topic-legacy: tutorial
description: Découvrez comment connecter Adobe Experience Platform à YOURSOURCE à l’aide de l’API Flow Service.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '2300'
ht-degree: 7%

---

# Créez un *VOTRE SOURCE* connexion à l’aide de l’API Flow Service

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Ignorez toutes les instances de DNL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

## Présentation

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Pour plus d’informations, insérez un lien vers la page d’accueil de la documentation du produit.*

>[!IMPORTANT]
>
>Cette page de documentation a été créée par la fonction *VOTRE SOURCE* l&#39;équipe. Pour toute demande de mise à jour ou de renseignements, contactez-les directement à l’adresse *Ajouter un lien ou une adresse électronique permettant d’accéder aux mises à jour*.

## Conditions préalables

*Ajoutez dans cette section des informations sur tout ce dont les clients doivent tenir compte avant de commencer à configurer la source dans l’interface utilisateur de Adobe Experience Platform. Il peut s’agir :*

* *à ajouter à une liste autorisée*
* *conditions requises pour le hachage des emails*
* *toute spécification de compte de votre côté ;*
* *Comment obtenir une clé API pour se connecter à votre plateforme*

## Connexion *VOTRE SOURCE* vers Platform à l’aide de [!DNL Flow Service] API

Le tutoriel suivant vous guide tout au long des étapes de création d’un *VOTRE SOURCE* connexion source et créer un flux de données à importer *VOTRE SOURCE* données vers Platform à l’aide de la fonction [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Création d’une connexion de base {#base-connection}

Une connexion de base conserve les informations entre votre source et Platform, y compris les informations d’authentification de votre source, l’état actuel de la connexion et votre identifiant de connexion de base unique. L’identifiant de connexion de base vous permet d’explorer et de parcourir des fichiers à partir de votre source et d’identifier les éléments spécifiques que vous souhaitez ingérer, y compris des informations concernant leurs types et formats de données.

Pour créer un identifiant de connexion de base, envoyez une requête de POST au `/connections` point de terminaison lors de la fourniture de *VOTRE SOURCE* informations d’identification d’authentification dans le corps de la requête.

**Format d’API**

```https
POST /connections
```

**Requête**

La requête suivante crée une connexion de base pour *VOTRE SOURCE* :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} base connection",
        "description": "{YOURSOURCE} base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth generic-rest-connector",
            "params": {
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}",
                "expirationDate": "{EXPIRATION_DATE}"
            }
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion de base. Assurez-vous que le nom de votre connexion de base est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion de base. |
| `description` | Une valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion de base. |
| `connectionSpec.id` | L’identifiant de spécification de connexion de votre source. Cet identifiant peut être récupéré une fois que votre source est enregistrée et approuvée par le biais de la variable [!DNL Flow Service] API. |
| `auth.specName` | Type d’authentification que vous utilisez pour authentifier votre source sur Platform. |
| `auth.params.` | Contient les informations d’identification requises pour authentifier votre source. |

**Réponse**

Une réponse réussie renvoie la nouvelle connexion de base, y compris son identifiant de connexion unique (`id`). Cet identifiant est nécessaire pour explorer la structure de fichiers et le contenu de votre source à l’étape suivante.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Exploration de la source {#explore}

À l’aide de l’identifiant de connexion de base que vous avez généré à l’étape précédente, vous pouvez explorer les fichiers et répertoires en exécutant des requêtes GET.
Utilisez les appels suivants pour trouver le chemin d’accès au fichier que vous souhaitez importer. [!DNL Platform]:

**Format d&#39;API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Lors de l’exécution de requêtes GET pour explorer la structure et le contenu des fichiers de votre source, vous devez inclure les paramètres de requête répertoriés dans le tableau ci-dessous :


| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Identifiant de connexion de base généré à l’étape précédente. |
| `objectType=rest` | Type d’objet que vous souhaitez explorer. Actuellement, cette valeur est toujours définie sur `rest`. |
| `{OBJECT}` | Ce paramètre est requis uniquement lors de l’affichage d’un répertoire spécifique. Sa valeur représente le chemin du répertoire que vous souhaitez explorer. |
| `fileType=json` | Type de fichier du fichier que vous souhaitez importer dans Platform. Actuellement, `json` est le seul type de fichier pris en charge. |
| `{PREVIEW}` | Une valeur boolean qui définit si le contenu de la connexion prend en charge l’aperçu. |
| `{SOURCE_PARAMS}` | Définit les paramètres du fichier source que vous souhaitez importer dans Platform. Pour récupérer le type de format accepté pour `{SOURCE_PARAMS}`, vous devez coder l’intégralité de la variable `list_id` chaîne en base64. Dans l’exemple ci-dessous, `"list_id": "10c097ca71"` encodé en base64 équivaut à `eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=`. |


**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du fichier interrogé.

```json
{
  "data": [
    {
      "members": [
        {
          "id": "cff65fb4c5f5828666ad846443720efd",
          "email_address": "roykent@gmail.com",
          "unique_email_id": "72c758cbf1",
          "full_name": "Roy Kent",
          "web_id": 547094062,
          "email_type": "html",
          "status": "subscribed",
          "merge_fields": {
            "FNAME": "Roy",
            "LNAME": "Kent",
            "ADDRESS": {
              "addr1": "",
              "addr2": "",
              "city": "Richmond",
              "state": "Virginia",
              "zip": "",
              "country": "US"
            },
            "PHONE": "",
            "BIRTHDAY": ""
          },
          "stats": {
            "avg_open_rate": 0,
            "avg_click_rate": 0
          },
          "ip_signup": "",
          "timestamp_signup": "",
          "ip_opt": "103.43.112.97",
          "timestamp_opt": "2021-06-01T15:31:36+00:00",
          "member_rating": 2,
          "last_changed": "2021-06-01T15:31:36+00:00",
          "language": "",
          "vip": false,
          "email_client": "",
          "location": {
            "latitude": 0,
            "longitude": 0,
            "gmtoff": 0,
            "dstoff": 0,
            "country_code": "",
            "timezone": ""
          },
          "source": "Admin Add",
          "tags_count": 0,
          "tags": [
             
          ],
          "list_id": "10c097ca71"
        }
      ],
      "list_id": "10c097ca71",
      "total_items": 2,
      "_links": [
        {
          "rel": "self",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/CollectionResponse.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Paths/Lists/Members/Collection.json"
        },
        {
          "rel": "parent",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71",
          "method": "GET",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json"
        },
        {
          "rel": "create",
          "href": "https://us6.api.mailchimp.com/3.0/lists/10c097ca71/members",
          "method": "POST",
          "targetSchema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/Response.json",
          "schema": "https://us6.api.mailchimp.com/schema/3.0/Definitions/Lists/Members/POST.json"
        }
      ]
    }
  ]
}
```

### Création d’une connexion source {#source-connection}

Vous pouvez créer une connexion source en envoyant une requête de POST au [!DNL Flow Service] API. Une connexion source se compose d’un identifiant de connexion, d’un chemin d’accès au fichier de données source et d’un identifiant de spécification de connexion.

**Format d’API**

```https
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source pour *VOTRE SOURCE* :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Source Connection",
        "description": "{YOURSOURCE} Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "server": "us6",
            "listId": "10c097ca71"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Une valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion source. |
| `baseConnectionId` | L’identifiant de connexion de base de *VOTRE SOURCE*. Cet identifiant a été généré lors d’une étape précédente. |
| `connectionSpec.id` | L’identifiant de spécification de connexion qui correspond à votre source. |
| `data.format` | Le format de la variable *VOTRE SOURCE* données que vous souhaitez ingérer. Actuellement, le seul format de données pris en charge est `json`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Création d’un schéma XDM cible {#target-schema}

Pour que les données source soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données source en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform dans lequel les données source sont contenues.

Un schéma XDM cible peut être créé en adressant une requête de POST au [API Schema Registry](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, consultez le tutoriel sur [création d’un schéma à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### Création d’un jeu de données cible {#target-dataset}

Un jeu de données cible peut être créé en adressant une requête de POST au [API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), fournissant l’identifiant du schéma cible dans la payload.

Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, consultez le tutoriel sur [création d’un jeu de données à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### Créer une connexion cible {#target-connection}

Une connexion cible représente la connexion à la destination vers laquelle les données ingérées doivent être stockées. Pour créer une connexion cible, vous devez fournir l&#39;identifiant fixe de spécification de connexion qui correspond à la variable [!DNL Data Lake]. Cet identifiant est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma cible d’un jeu de données cible et de l’identifiant de spécification de connexion à la variable [!DNL Data Lake]. A l&#39;aide de ces identifiants, vous pouvez créer une connexion cible à l&#39;aide de la fonction [!DNL Flow Service] API pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```https
POST /targetConnections
```

**Requête**

La requête suivante crée une connexion cible pour *VOTRE SOURCE* :

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} Target Connection",
        "description": "{YOURSOURCE} Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom de la connexion cible. Assurez-vous que le nom de votre connexion cible est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion cible. |
| `description` | Une valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion cible. |
| `connectionSpec.id` | L’identifiant de spécification de connexion qui correspond à [!DNL Data Lake]. Cet ID fixe est : `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Le format de la variable *VOTRE SOURCE* données que vous souhaitez apporter à Platform. |
| `params.dataSetId` | Identifiant du jeu de données cible récupéré lors d’une étape précédente. |


**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cet identifiant est requis aux étapes suivantes.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Création d’un mappage {#mapping}

Pour que les données source soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible adhère. Pour ce faire, il vous suffit d’adresser une requête de POST à [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) avec des mappages de données définis dans le payload de la requête.

**Format d’API**

```http
POST /conversion/mappingSets
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| Propriété | Description |
| --- | --- |
| `xdmSchema` | L’identifiant de la variable [schéma XDM cible](#target-schema) généré lors d’une étape précédente. |
| `mappings.destinationXdmPath` | Chemin XDM de destination vers lequel l’attribut source est mappé. |
| `mappings.sourceAttribute` | L’attribut source qui doit être mappé à un chemin XDM de destination. |
| `mappings.identity` | Une valeur boolean qui indique si le jeu de mappages sera marqué pour [!DNL Identity Service]. |

**Réponse**

Une réponse réussie renvoie les détails du mappage nouvellement créé, y compris son identifiant unique (`id`). Cette valeur est requise lors d’une étape ultérieure pour créer un flux de données.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### Création d’un flux {#flow}

La dernière étape pour obtenir des données de *VOTRE SOURCE* à Platform consiste à créer un flux de données. À l’heure actuelle, les valeurs requises suivantes sont préparées :

* [ID de connexion source](#source-connection)
* [Identifiant de connexion Target](#target-connection)
* [ID de mappage](#mapping)

Un flux de données est chargé de planifier et de collecter les données d’une source. Vous pouvez créer un flux de données en exécutant une requête de POST tout en fournissant les valeurs mentionnées précédemment dans le payload.

Pour planifier une ingestion, vous devez d’abord définir la valeur de l’heure de début sur la durée en secondes. Vous devez ensuite définir la valeur de fréquence sur l’une des cinq options suivantes : `once`, `minute`, `hour`, `day`ou `week`. La valeur interval désigne toutefois la période entre deux ingestion consécutives, la création d’une ingestion unique ne nécessite pas de définition d’un intervalle. Pour toutes les autres fréquences, la valeur de l’intervalle doit être égale ou supérieure à `15`.


**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{YOURSOURCE} dataflow",
        "description": "{YOURSOURCE} dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre flux de données. Assurez-vous que le nom de votre flux de données est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre flux de données. |
| `description` | Une valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre flux de données. |
| `flowSpec.id` | Identifiant de spécification de flux requis pour créer un flux de données. Cet ID fixe est : `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | La version correspondante de l’identifiant de spécification de flux. Cette valeur est définie par défaut sur `1.0`. |
| `sourceConnectionIds` | Le [ID de connexion source](#source-connection) généré lors d’une étape précédente. |
| `targetConnectionIds` | Le [identifiant de connexion cible](#target-connection) généré lors d’une étape précédente. |
| `transformations` | Cette propriété contient les différentes transformations qui doivent être appliquées à vos données. Cette propriété est requise lors de l’introduction de données non conformes à XDM dans Platform. |
| `transformations.name` | Nom attribué à la transformation. |
| `transformations.params.mappingId` | Le [ID de mappage](#mapping) généré lors d’une étape précédente. |
| `transformations.params.mappingVersion` | La version correspondante de l’ID de mappage. Cette valeur est définie par défaut sur `0`. |
| `scheduleParams.startTime` | Cette propriété contient des informations sur la planification de l’ingestion du flux de données. |
| `scheduleParams.frequency` | Fréquence à laquelle le flux de données collectera les données. Les valeurs possibles sont les suivantes : `once`, `minute`, `hour`, `day`ou `week`. |
| `scheduleParams.interval` | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul. L’intervalle n’est pas requis lorsque la fréquence est définie sur `once` et doit être supérieur ou égal à `15` pour d’autres valeurs de fréquence. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du nouveau flux de données. Vous pouvez utiliser cet identifiant pour surveiller, mettre à jour ou supprimer votre flux de données.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les exécutions de flux, l’état d’achèvement et les erreurs.

**Format d’API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

**Requête**

La requête suivante récupère les spécifications d’un flux de données existant.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des détails sur votre exécution de flux, y compris des informations sur sa date de création, les connexions source et cible, ainsi que l’identifiant unique de l’exécution de flux (`id`).

```json
{
    "items": [
        {
            "createdAt": 1596656079576,
            "updatedAt": 1596656113526,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": "prod",
            "id": "9830305a-985f-47d0-b030-5a985fd7d004",
            "flowId": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
            "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1596656058198,
                    "completedAtUTC": 1596656113306
                },
                "sizeSummary": {
                    "inputBytes": 24012,
                    "outputBytes": 17128
                },
                "recordSummary": {
                    "inputRecordCount": 100,
                    "outputRecordCount": 99,
                    "failedRecordCount": 1
                },
                "fileSummary": {
                    "inputFileCount": 1,
                    "outputFileCount": 1,
                    "activityRefs": [
                        "promotionActivity"
                    ]
                },
                "statusSummary": {
                    "status": "success",
                    "errors": [
                        {
                            "code": "CONNECTOR-2001-500",
                            "message": "Error occurred at promotion activity."
                        }
                    ],
                    "activityRefs": [
                        "promotionActivity"
                    ]
                }
            },
            "activities": [
                {
                    "id": "copyActivity",
                    "updatedAtUTC": 1596656095088,
                    "durationSummary": {
                        "startedAtUTC": 1596656058198,
                        "completedAtUTC": 1596656089650,
                        "extensions": {
                            "windowStart": 1596653708000,
                            "windowEnd": 1596655508000
                        }
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 24012
                    },
                    "recordSummary": {},
                    "fileSummary": {
                        "inputFileCount": 1,
                        "outputFileCount": 1
                    },
                    "statusSummary": {
                        "status": "success",
                        "extensions": {
                            "type": "one-time"
                        }
                    },
                    "sourceInfo": [
                        {
                            "id": "c0e18602-f9ea-44f9-a186-02f9ea64f9ac",
                            "type": "SourceConnection",
                            "reference": {
                                "type": "AdfRunId",
                                "ids": [
                                    "8a8eb0cc-e283-4605-ac70-65a5adb1baef"
                                ]
                            }
                        }
                    ]
                },
                {
                    "id": "promotionActivity",
                    "updatedAtUTC": 1596656113485,
                    "durationSummary": {
                        "startedAtUTC": 1596656095333,
                        "completedAtUTC": 1596656113306
                    },
                    "sizeSummary": {
                        "inputBytes": 24012,
                        "outputBytes": 17128
                    },
                    "recordSummary": {
                        "inputRecordCount": 100,
                        "outputRecordCount": 99,
                        "failedRecordCount": 1
                    },
                    "fileSummary": {
                        "inputFileCount": 2,
                        "outputFileCount": 1,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=input_files"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success",
                        "errors": [
                            {
                                "code": "CONNECTOR-2001-500",
                                "message": "Error occurred at promotion activity."
                            }
                        ],
                        "extensions": {
                            "manifest": {
                                "failedRecords": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_errors",
                                "sampleErrors": "https://platform.adobe.io/data/foundation/export/batches/01EF01X41KJD82Y9ZX6ET54PCZ/meta?path=row_error_samples.json"
                            },
                            "errors": [
                                {
                                    "code": "INGEST-1212-400",
                                    "message": "Encountered 1 errors in the data. Successfully ingested 99 rows. Review the associated diagnostic files for additional details."
                                },
                                {
                                    "code": "MAPPER-3700-400",
                                    "recordCount": 1,
                                    "message": "Mapper Transform Error"
                                }
                            ]
                        }
                    },
                    "targetInfo": [
                        {
                            "id": "47166b83-01c7-4b65-966b-8301c70b6562",
                            "type": "TargetConnection",
                            "reference": {
                                "type": "Batch",
                                "ids": [
                                    "01EF01X41KJD82Y9ZX6ET54PCZ"
                                ]
                            }
                        }
                    ]
                }
            ]
        }
    ],
    "_links": {}
}
```

| Propriété | Description |
| -------- | ----------- |
| `items` | Contient un seul payload de métadonnées associé à votre exécution de flux spécifique. |
| `metrics` | Définit les caractéristiques des données dans l’exécution du flux. |
| `activities` | Définit la manière dont les données sont transformées. |
| `durationSummary` | Définit les heures de début et de fin de l’exécution du flux. |
| `sizeSummary` | Définit le volume des données en octets. |
| `recordSummary` | Définit le nombre d’enregistrements des données. |
| `fileSummary` | Définit le nombre de fichiers des données. |
| `statusSummary` | Définit si l’exécution du flux est une réussite ou un échec. |

### Mise à jour de votre flux de données

Pour mettre à jour le planning d’exécution, le nom et la description de votre flux de données, envoyez une requête de PATCH au [!DNL Flow Service] API lors de la fourniture de votre ID de flux, de votre version et du nouveau planning que vous souhaitez utiliser.

>[!IMPORTANT]
>
>Le `If-Match` est requis lors de l’exécution d’une requête de PATCH. La valeur de cet en-tête est l’etag unique du flux de données que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

La requête suivante met à jour votre planning d’exécution de flux, ainsi que le nom et la description de votre flux de données.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "New dataflow name"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Updated dataflow description"
            }
        ]'
```

| Paramètre | Description |
| --------- | ----------- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour le flux de données. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d&#39;accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à la variable [!DNL Flow Service] de l’API, tout en fournissant votre ID de flux.

```json
{
    "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

### Suppression de votre flux de données

Avec un identifiant de flux existant, vous pouvez supprimer un flux de données en adressant une requête de DELETE au [!DNL Flow Service] API.

**Format d’API**

```http
DELETE /flows/{FLOW_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{FLOW_ID}` | L’unique `id` pour le flux de données que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide. Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) au flux de données. L’API renvoie une erreur HTTP 404 (Introuvable), indiquant que le flux de données a été supprimé.

### Mettre à jour votre connexion

Pour mettre à jour le nom, la description et les informations d’identification de votre connexion, envoyez une requête de PATCH au [!DNL Flow Service] API lors de la fourniture de votre ID de connexion de base, de votre version et des nouvelles informations que vous souhaitez utiliser.

>[!IMPORTANT]
>
>Le `If-Match` est requis lors de l’exécution d’une requête de PATCH. La valeur de cet en-tête est la version unique de la connexion que vous souhaitez mettre à jour.

**Format d’API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | L’unique `id` pour la connexion que vous souhaitez mettre à jour. |

**Requête**

La requête suivante fournit un nouveau nom et une nouvelle description, ainsi qu’un nouveau jeu d’informations d’identification, avec lequel mettre à jour votre connexion.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Paramètre | Description |
| --------- | ----------- |
| `op` | Appel d&#39;opération utilisé pour définir l&#39;action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Chemin d&#39;accès du paramètre à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre paramètre. |

**Réponse**

Une réponse réussie renvoie votre identifiant de connexion de base et une balise mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à la variable [!DNL Flow Service] de l’API, tout en fournissant votre identifiant de connexion.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

### Supprimer votre connexion

Une fois que vous disposez d’un identifiant de connexion de base existant, effectuez une requête de DELETE à la variable [!DNL Flow Service] API.

**Format d’API**

```http
DELETE /connections/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | L’unique `id` pour la connexion de base que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/connections/dd3631cd-d0ea-4fea-b631-cdd0ea6fea21' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Vous pouvez confirmer la suppression en tentant d’adresser une requête de recherche (GET) à la connexion.
