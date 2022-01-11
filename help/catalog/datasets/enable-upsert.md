---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;activer un jeu de données
title: Activation d’un jeu de données pour les mises à jour de profil à l’aide d’API
type: Tutorial
description: Ce tutoriel vous explique comment utiliser les API Adobe Experience Platform pour activer un jeu de données avec des fonctionnalités "d’insertion" afin d’effectuer des mises à jour des données de Real-time Customer Profile.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: d463dabbb9dc099394081b803df619129c0cb416
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 35%

---

# Activation d’un jeu de données pour les mises à jour de profil à l’aide d’API

Ce tutoriel décrit le processus d’activation d’un jeu de données avec des fonctionnalités &quot;d’insertion&quot; afin d’effectuer des mises à jour des données de Real-time Customer Profile. Cela inclut les étapes de création d’un nouveau jeu de données et de configuration d’un jeu de données existant.

## Prise en main

Ce tutoriel nécessite une compréhension pratique de plusieurs services Adobe Experience Platform impliqués dans la gestion des jeux de données activés pour Profile. Avant de commencer ce tutoriel, veuillez consulter la documentation relative à ces [!DNL Platform] services :

- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [[!DNL Catalog Service]](../../catalog/home.md): Une API RESTful qui vous permet de créer des jeux de données et de les configurer pour [!DNL Real-time Customer Profile] et [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
- [Ingestion par lots](../../ingestion/batch-ingestion/overview.md)

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Toutes les requêtes contenant un payload (POST, PUT, PATCH) nécessitent une `Content-Type` en-tête . La valeur correcte de cet en-tête s’affiche dans les exemples de requêtes, le cas échéant.

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées à [!DNL Platform] Les API requièrent une `x-sandbox-name` qui spécifie le nom de l’environnement de test dans lequel l’opération aura lieu. Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

## Création d’un jeu de données activé pour les mises à jour de profil

Lors de la création d’un jeu de données, vous pouvez activer ce jeu de données pour Profile et activer les fonctionnalités de mise à jour au moment de la création.

>[!NOTE]
>
>Pour créer un jeu de données activé par Profile, vous devez connaître l’identifiant d’un schéma XDM existant activé pour Profile. Pour plus d’informations sur la recherche ou la création d’un schéma activé pour Profile, reportez-vous au tutoriel sur la [création d’un schéma à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md).

Pour créer un jeu de données activé pour Profile et les mises à jour, utilisez une requête de POST au `/dataSets` point de terminaison .

**Format d’API**

```http
POST /dataSets
```

**Requête**

En incluant `unifiedProfile` under `tags` dans le corps de la requête, le jeu de données sera activé pour [!DNL Profile] lors de la création. Dans le `unifiedProfile` tableau, ajout `isUpsert:true` ajoutera la possibilité pour le jeu de données de prendre en charge les mises à jour.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "fields":[],
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
          "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| Propriété | Description |
|---|---|
| `schemaRef.id` | L’identifiant de la variable [!DNL Profile]schéma activé sur lequel le jeu de données sera basé. |
| `{TENANT_ID}` | L’espace de noms dans la variable [!DNL Schema Registry] qui contient des ressources appartenant à votre organisation IMS. Voir [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) de la section [!DNL Schema Registry] guide de développement pour plus d’informations. |

**Réponse**

Une réponse réussie affiche un tableau contenant l’identifiant du jeu de données nouvellement créé sous la forme d’un `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configuration d’un jeu de données existant {#configure-an-existing-dataset}

Les étapes suivantes expliquent comment configurer un jeu de données activé par Profile existant pour la fonctionnalité de mise à jour (&quot;upsert&quot;).

>[!NOTE]
>
>Pour configurer un jeu de données activé par Profile existant en vue de l’&quot;insertion&quot;, vous devez d’abord désactiver le jeu de données pour Profile, puis le réactiver avec le `isUpsert` balise . Si le jeu de données existant n’est pas activé pour Profile, vous pouvez passer directement aux étapes de [activation du jeu de données pour Profile et upsert](#enable-the-dataset). Si vous n’êtes pas sûr, les étapes suivantes vous montrent comment vérifier si le jeu de données est déjà activé.

### Vérifiez si le jeu de données est activé pour Profile.

En utilisant la variable [!DNL Catalog] API, vous pouvez examiner un jeu de données existant pour déterminer s’il est activé pour une utilisation dans [!DNL Real-time Customer Profile]. L’appel suivant récupère les détails d’un jeu de données via son identifiant.

**Format d’API**

```http
GET /dataSets/{DATASET_ID}
```

| Paramètre | Description |
|---|---|
| `{DATASET_ID}` | Identifiant du jeu de données à examiner. |

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Sous , `tags` , vous pouvez voir que `unifiedProfile` est présent avec la valeur `enabled:true`. Par conséquent, [!DNL Real-time Customer Profile] est activé pour ce jeu de données.

### Désactivation du jeu de données pour Profile

Pour configurer un jeu de données activé par Profile pour les mises à jour, vous devez d’abord désactiver la variable `unifiedProfile` puis réactivez-la à côté de la balise `isUpsert` balise . Cette opération s’effectue à l’aide de deux demandes de PATCH, une pour la désactivation et une pour la réactivation.

>[!WARNING]
>
>Les données ingérées dans le jeu de données alors qu’il est désactivé ne seront pas ingérées dans le magasin de profils. Il est recommandé d’éviter d’ingérer des données dans le jeu de données jusqu’à ce qu’il ait été réactivé pour Profile.

**Format d’API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Paramètre | Description |
|---|---|
| `{DATASET_ID}` | Identifiant du jeu de données à mettre à jour. |

**Requête**

Le premier corps de requête de PATCH comprend une `path` to `unifiedProfile` définition de la variable `value` to `enabled:false` afin de désactiver la balise.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

**Réponse**
Une requête PATCH réussie renvoie un état HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. Le `unifiedProfile` a été désactivé.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Activation du jeu de données pour Profile et la publication {#enable-the-dataset}

Un jeu de données existant peut être activé pour les mises à jour de profil et d’attribut à l’aide d’une seule requête de PATCH.

**Format d’API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Paramètre | Description |
|---|---|
| `{DATASET_ID}` | Identifiant du jeu de données à mettre à jour. |

**Requête**

Le corps de la requête comprend un `path` to `unifiedProfile` définition de la variable `value` pour inclure la variable `enabled` et `isUpsert` balises, toutes deux définies sur `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

**Réponse**
Une requête PATCH réussie renvoie un état HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. Le `unifiedProfile` a été activée et configurée pour les mises à jour d’attributs.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Étapes suivantes

Votre profil et votre jeu de données activé pour le service peuvent désormais être utilisés par les workflows d’ingestion par lots et par flux pour mettre à jour les données de profil. Pour en savoir plus sur l’ingestion de données dans Adobe Experience Platform, commencez par lire le [présentation de l’ingestion des données](../../ingestion/home.md).
