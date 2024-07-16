---
title: Modèle de documentation en libre-service pour l’API du SDK de diffusion en continu
description: Découvrez comment importer des données en continu d’une source vers Adobe Experience Platform à l’aide de l’API Flow Service.
exl-id: a06384a2-cd99-456d-9f00-babcf3f7b7d9
badge: Version bêta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 43%

---

# Créez une connexion source et un flux de données pour diffuser des données *YOURSOURCE* à l’aide de l’API [!DNL Flow Service].

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Ignorez toutes les instances de DNL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

## Vue d’ensemble

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Insérez un lien vers la page d’accueil de la documentation du produit pour une lecture plus approfondie.*

>[!IMPORTANT]
>
>Ce connecteur source et cette page de documentation sont créés et conservés par l’équipe *YOURSOURCE*. Pour toute demande de mise à jour ou de demande de mise à jour, contactez-les directement à l&#39;adresse *Ajouter un lien ou une adresse email où vous pouvez accéder pour les mises à jour*.

## Conditions préalables

*Ajoutez dans cette section des informations sur tout ce dont les clients doivent tenir compte avant de commencer à configurer la source dans l’interface utilisateur de Adobe Experience Platform. Il peut s’agir de :*

* *à ajouter à une liste autorisée*
* *Conditions requises pour le hachage des emails*
* *toutes les caractéristiques de compte de votre côté*
* *Comment obtenir une clé API pour se connecter à votre plateforme*

### Collecter les informations d’identification requises

Pour connecter *YOURSOURCE* à Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| *identifiant one* | *Ajoutez une brève description aux informations d’identification d’authentification de votre source ici* | *Ajoutez ici un exemple d&#39;informations d&#39;identification d&#39;authentification de votre source* |
| *credential two* | *Ajoutez une brève description aux informations d’identification d’authentification de votre source ici* | *Ajoutez ici un exemple d&#39;informations d&#39;identification d&#39;authentification de votre source* |
| *credential trois* | *Ajoutez une brève description aux informations d’identification d’authentification de votre source ici* | *Ajoutez ici un exemple d&#39;informations d&#39;identification d&#39;authentification de votre source* |

Pour plus d’informations sur ces informations d’identification, consultez la documentation d’authentification *YOURSOURCE*. *Ajoutez un lien vers la documentation d’authentification de votre plateforme ici*.

### Intégrer *YOURSOURCE* à votre webhook

*Le SDK de diffusion en continu nécessite que votre source puisse prendre en charge les webhooks pour communiquer avec un Experience Platform. Dans cette section, vous devez indiquer les étapes que vos utilisateurs devront suivre pour intégrer VOTRE SOURCE à un webhook.*

## Connectez *YOURSOURCE* à Platform à l’aide de l’API [!DNL Flow Service]

Le tutoriel suivant vous guide tout au long des étapes pour créer une connexion source *YOURSOURCE* et créer un flux de données pour importer des données *YOURSOURCE* vers Platform à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Créer une connexion source {#source-connection}

Créez une connexion source en adressant une requête de POST à l’API [!DNL Flow Service], tout en fournissant l’identifiant de spécification de connexion de votre source, des détails tels que le nom et la description, et le format de vos données.

**Format d’API**

```https
POST /sourceConnections
```

**Requête**

La requête suivante crée une connexion source pour *YOURSOURCE* :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for a Streaming SDK source",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de votre connexion source. Assurez-vous que le nom de votre connexion source est descriptif, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion source. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion source. |
| `connectionSpec.id` | Identifiant de spécification de connexion correspondant à votre source. |
| `data.format` | Format des données *YOURSOURCE* que vous souhaitez ingérer. Actuellement, le format de données `json` est le seul à être pris en charge. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Cet identifiant est requis lors d’une étape ultérieure pour créer un flux de données.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### Créer un schéma XDM cible {#target-schema}

Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Le schéma cible est ensuite utilisé pour créer un jeu de données Platform contenant les données sources.

Un schéma XDM cible peut être créé en adressant une requête POST à l’[API Schema Registry](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html#create).

### Créer un jeu de données cible {#target-dataset}

Un jeu de données cible peut être créé en adressant une requête POST à l’[API Catalog Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) et en fournissant l’identifiant du schéma cible dans la payload.

Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html).

### Créer une connexion cible {#target-connection}

Une connexion cible représente la connexion à la destination vers laquelle les données ingérées doivent être stockées. Pour créer une connexion cible, vous devez fournir l’identifiant de spécification de connexion fixe qui correspond au lac de données. Cet identifiant est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Vous disposez désormais des identifiants uniques d’un schéma cible d’un jeu de données cible et de l’identifiant de spécification de connexion au lac de données. À lʼaide de ces identifiants, vous pouvez créer une connexion cible à l’aide de l’API [!DNL Flow Service] pour spécifier le jeu de données qui contiendra les données source entrantes.

**Format d’API**

```https
POST /targetConnections
```

**Requête**

La requête suivante crée une connexion cible pour *YOURSOURCE* :


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Streaming SDK source",
      "description": "Streaming Target Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| Propriété | Description |
| -------- | ----------- |
| `name` | Nom de la connexion cible. Assurez-vous que le nom de votre connexion cible est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre connexion cible. |
| `description` | Valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre connexion cible. |
| `connectionSpec.id` | L’identifiant de spécification de connexion qui correspond au lac de données. Cet ID fixe est `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Format des données *YOURSOURCE* que vous souhaitez importer dans Platform. |
| `params.dataSetId` | Identifiant du jeu de données cible récupéré lors d’une étape précédente. |


**Réponse**

Une réponse réussie renvoie l’identifiant unique de la nouvelle connexion cible (`id`). Cet identifiant est requis aux étapes suivantes.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Créer un mappage {#mapping}

Pour que les données sources soient ingérées dans un jeu de données cible, elles doivent d’abord être mappées au schéma cible auquel le jeu de données cible se rattache. Pour ce faire, effectuez une requête de POST vers [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) avec des mappages de données définis dans le payload de la requête.

**Format d’API**

```http
POST /conversion/mappingSets
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| Propriété | Description |
| --- | --- |
| `xdmSchema` | Identifiant du [schéma XDM cible](#target-schema) généré lors d’une étape précédente. |
| `mappings.destinationXdmPath` | Chemin XDM de destination vers lequel l’attribut source est mappé. |
| `mappings.sourceAttribute` | Attribut source qui doit être mappé à un chemin XDM de destination. |
| `mappings.identity` | Valeur booléenne qui indique si le jeu de mappage sera marqué pour [!DNL Identity Service]. |

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

### Créer un flux {#flow}

La dernière étape pour apporter des données de *YOURSOURCE* à Platform consiste à créer un flux de données. Vous disposez à présent des valeurs requises suivantes :

* [ID de connexion source](#source-connection)
* [ID de connexion cible](#target-connection)
* [Identifiant de mappage](#mapping)

Un flux de données est chargé de planifier et de collecter les données provenant d’une source. Vous pouvez créer un flux de données en exécutant une requête POST et en fournissant les valeurs mentionnées précédemment dans la payload.

**Format d’API**

```http
POST /flows
```

**Requête**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
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
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom du flux de données. Assurez-vous que le nom de votre flux de données est explicite, car vous pouvez l’utiliser pour rechercher des informations sur votre flux de données. |
| `description` | Une valeur facultative que vous pouvez inclure pour fournir plus d’informations sur votre flux de données. |
| `flowSpec.id` | Identifiant de spécification de flux requis pour créer un flux de données. Cet ID fixe est `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | Version correspondante de l’identifiant de spécification de flux. Cette valeur est définie par défaut sur `1.0`. |
| `sourceConnectionIds` | L’[identifiant de connexion source](#source-connection) généré lors d’une étape précédente. |
| `targetConnectionIds` | [Identifiant de connexion cible](#target-connection) généré lors d’une étape précédente. |
| `transformations` | Cette propriété contient les différentes transformations qui doivent être appliquées à vos données. Cette propriété est requise lors de l’importation de données non conformes à XDM dans Platform. |
| `transformations.name` | Nom attribué à la transformation. |
| `transformations.params.mappingId` | [Identifiant de mappage](#mapping) généré lors d’une étape précédente. |
| `transformations.params.mappingVersion` | Version correspondante de l’identifiant de mappage. Ce paramètre est défini par défaut sur `0`. |

**Réponse**

Une réponse réussie renvoie l’identifiant (`id`) du flux de données nouvellement créé. Vous pouvez utiliser cet identifiant pour surveiller, mettre à jour ou supprimer votre flux de données.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### Obtention de l’URL de votre point de terminaison de diffusion

Une fois votre flux de données créé, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu. Vous utiliserez cette URL de point de terminaison pour abonner votre source à un webhook, ce qui vous permettra de communiquer avec votre Experience Platform.

Pour récupérer l’URL de votre point de terminaison de diffusion en continu, envoyez une requête GET au point de terminaison `/flows` et fournissez l’identifiant de votre flux de données.

**Format d’API**

```http
GET /flows/{FLOW_ID}
```

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des informations sur votre flux de données, y compris votre URL de point d’entrée, marquée comme `inletUrl`.

```json
{
  "items": [
    {
      "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
        "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
        "version": "1.0"
      },
      "state": "enabled",
      "version": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "etag": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "sourceConnectionIds": [
        "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
        "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "inheritedAttributes": {
        "properties": {
          "isSourceFlow": true
        },
        "sourceConnections": [
          {
            "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
            "connectionSpec": {
              "id": "bdb5b792-451b-42de-acf8-15f3195821de",
              "version": "1.0"
            }
          }
        ],
        "targetConnections": [
          {
            "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
            "connectionSpec": {
              "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
              "version": "1.0"
            }
          }
        ]
      },
      "options": {
        "errorDiagnosticsEnabled": true,
        "inletUrl": "https://dcs-int.adobedc.net/collection/ab65636c31778fb0455c439ffb48a5433a34d443f4c83c4b5beda9c5688797c5"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingVersion": 0,
            "mappingId": "bf5286a9c1ad4266baca76ba3adc9366"
          }
        }
      ],
      "runs": "/runs?property=flowId==e1514b79-f031-43b4-aab5-381a42f86ad4",
      "providerRefId": "c9809ab5-71e0-4c7f-887b-61c95e4e20b5",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "enable"
      }
    }
  ]
}
```

## Annexe

La section suivante fournit des informations sur les étapes de surveillance, de mise à jour et de suppression de votre flux de données.

### Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les exécutions du flux, le statut d’achèvement et les erreurs. Pour obtenir des exemples complets d’API, consultez le guide sur la [surveillance des flux de données de sources à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### Mettre à jour votre flux de données

Mettez à jour les détails de votre flux de données, tels que son nom et sa description, ainsi que son planning d’exécution et les ensembles de mappages associés, en envoyant une requête de PATCH au point de terminaison `/flows` de l’API [!DNL Flow Service], tout en fournissant l’identifiant de votre flux de données. Lors de l’exécution d’une requête de PATCH, vous devez fournir l’unique `etag` de votre flux de données dans l’en-tête `If-Match`. Pour consulter des exemples complets d’API, consultez le guide sur la [mise à jour des flux de données de sources à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### Mettre à jour votre compte

Mettez à jour le nom, la description et les informations d’identification de votre compte source en adressant une requête de PATCH à l’API [!DNL Flow Service] tout en fournissant votre identifiant de connexion de base en tant que paramètre de requête. Lors de l’exécution d’une requête de PATCH, vous devez fournir l’unique `etag` de votre compte source dans l’en-tête `If-Match`. Pour obtenir des exemples complets d’API, lisez le guide sur la [mise à jour de votre compte source à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### Supprimer le flux de données

Supprimez votre flux de données en adressant une requête de DELETE à l’API [!DNL Flow Service] tout en fournissant l’identifiant du flux de données que vous souhaitez supprimer dans le cadre du paramètre de requête . Pour obtenir des exemples complets d’API, lisez le guide sur la [suppression de vos flux de données à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### Suppression de votre compte

Supprimez votre compte en adressant une requête de DELETE à l’API [!DNL Flow Service] tout en fournissant l’identifiant de connexion de base du compte que vous souhaitez supprimer. Pour obtenir des exemples complets d’API, lisez le guide sur la [suppression de votre compte source à l’aide de l’API](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).
