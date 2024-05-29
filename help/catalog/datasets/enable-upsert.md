---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;activer un jeu de données
title: Activer un jeu de données pour les mises à jour de profil à l’aide d’API
type: Tutorial
description: Ce tutoriel vous explique comment utiliser les API Adobe Experience Platform pour activer un jeu de données avec des fonctionnalités "d’insertion" afin d’effectuer des mises à jour des données Real-time Customer Profile.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 90%

---

# Activer un jeu de données pour les mises à jour de profil à l’aide d’API

Ce tutoriel décrit le processus d’activation d’un jeu de données avec des fonctionnalités &quot;d’insertion&quot; afin d’effectuer des mises à jour des données de Real-time Customer Profile. Ceci inclut les étapes de création d’un nouveau jeu de données et la configuration d’un jeu de données existant.

>[!NOTE]
>
>Le workflow décrit dans ce tutoriel ne fonctionne que pour l’ingestion par lots. Pour les upserts d’ingestion par flux, consultez le guide sur [Envoi de mises à jour de lignes partielles à Real-time Customer Profile à l’aide de la préparation de données](../../data-prep/upserts.md).

## Prise en main

Ce tutoriel nécessite une connaissance pratique des différents services Adobe Experience Platform impliqués dans la gestion des jeux de données activés pour Profil. Avant de commencer ce tutoriel, consultez la documentation relative à ces services [!DNL Platform] associés :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Catalog Service]](../../catalog/home.md) : une API RESTful qui vous permet de créer des jeux de données et de les configurer pour [!DNL Real-Time Customer Profile] et [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
- [Ingestion par lots](../../ingestion/batch-ingestion/overview.md) : l’API d’ingestion par lots vous permet d’ingérer des données dans Experience Platform sous forme de fichiers par lots.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des API Platform.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Toutes les requêtes contenant une payload (POST, PUT, PATCH) nécessitent un en-tête `Content-Type` supplémentaire : La valeur correcte de cet en-tête s’affiche dans les exemples de requêtes, le cas échéant.

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête `x-sandbox-name` spécifiant le nom du sandbox dans lequel l’opération sera effectuée. Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Créer un jeu de données activé pour les mises à jour de profil

Lors de la création d’un jeu de données, vous pouvez activer ce jeu de données pour le profil et activer les fonctionnalités de mise à jour.

>[!NOTE]
>
>Pour créer un nouveau jeu de données activé pour Profil, vous devez connaître l’identifiant d’un schéma XDM existant et activé pour Profil. Pour plus d’informations sur la recherche ou la création d’un schéma activé pour Profil, reportez-vous au tutoriel sur la [création d’un schéma à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md).

Pour créer un jeu de données activé pour le profil et les mises à jour, utilisez une requête POST au point d’entrée `/dataSets`.

**Format d’API**

```http
POST /dataSets
```

**Requête**

En incluant à la fois le `unifiedIdentity` et le `unifiedProfile` sous `tags` dans le corps de la requête, le jeu de données sera activé pour [!DNL Profile] à la création. Dans le tableau `unifiedProfile`, l’ajout de `isUpsert:true` permettra au jeu de données de prendre en charge les mises à jour.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| Propriété | Description |
| -------- | ----------- |
| `schemaRef.id` | L’ID du schéma activé pour [!DNL Profile] sur lequel le jeu de données sera basé. |
| `{TENANT_ID}` | L’espace de noms dans [!DNL Schema Registry] qui contient les ressources appartenant à votre organisation. Pour plus d’informations, consultez la section [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) du guide de développement [!DNL Schema Registry]. |

**Réponse**

Une réponse réussie affiche un tableau contenant l’identifiant du jeu de données nouvellement créé sous la forme d’un `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## Configurer un jeu de données existant {#configure-an-existing-dataset}

Les étapes suivantes expliquent comment configurer un jeu de données existant activé pour un profil pour permettre une mise à jour (upsert).

>[!NOTE]
>
>Pour configurer un jeu de données existant activé pour un profil en vue de sa mise à jour, vous devez d’abord désactiver le jeu de données pour le profil puis le réactiver avec la balise `isUpsert`. Si le jeu de données existant n’est pas activé pour le profil, vous pouvez passer directement aux étapes d’[activation du jeu de données pour le profil et l’upsert](#enable-the-dataset). Si vous n’êtes pas sûr, les étapes suivantes vous montrent comment vérifier si le jeu de données est déjà activé.

### Vérifier si le jeu de données est activé pour le profil

En utilisant l’API [!DNL Catalog], vous pouvez examiner un jeu de données existant et déterminer s’il est activé pour une utilisation dans [!DNL Real-Time Customer Profile]. L’appel suivant récupère les détails d’un jeu de données via son identifiant.

**Format d’API**

```http
GET /dataSets/{DATASET_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | Identifiant du jeu de données à examiner. |

**Requête**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSetFiles?dataSetId=5b020a27e7040801dedbf46e",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

Sous la propriété `tags`, vous pouvez voir que `unifiedProfile` est présent avec la valeur `enabled:true`. Par conséquent, [!DNL Real-Time Customer Profile] est activé pour ce jeu de données.

### Désactiver le jeu de données pour Profil

Pour configurer un jeu de données activé pour le profil pour les mises à jour, vous devez d’abord désactiver les balises `unifiedProfile` et `unifiedIdentity` puis les réactiver avec la balise `isUpsert`. Cette opération s’effectue à l’aide de deux requêtes PATCH, une pour la désactivation et une pour la réactivation.

>[!WARNING]
>
>Les données ingérées dans le jeu de données alors qu’il est désactivé ne seront pas ingérées dans la banque de données Profile. Vous devez éviter d’ingérer des données dans le jeu de données jusqu’à ce qu’il ait été réactivé pour Profil.

**Format d’API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | Identifiant du jeu de données à mettre à jour. |

**Requête**

Le premier corps de requête PATCH comprend un `path` vers `unifiedProfile` et un `path` vers `unifiedIdentity`, qui définissent `value` sur `enabled:false` pour ces deux chemins afin de désactiver les balises.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**Réponse**

Une requête PATCH réussie renvoie un statut HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. Les balises `unifiedProfile` et `unifiedIdentity` ont désormais été désactivées.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### Activer le jeu de données pour Profil et upsert {#enable-the-dataset}

Un jeu de données existant peut être activé pour les mises à jour de Profil et d’attribut à l’aide d’une seule requête PATCH.

>[!IMPORTANT]
>
>Lors de l’activation de votre jeu de données pour Profil, assurez-vous que le schéma auquel le jeu de données est associé est **également** activé pour Profil. Si le schéma n’est pas activé pour Profil, le jeu de données n’apparaîtra **pas** en tant qu’activé pour Profil dans l’interface utilisateur de Platform.

**Format d’API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATASET_ID}` | Identifiant du jeu de données à mettre à jour. |

**Requête**

Le corps de la requête comprend un `path` vers `unifiedProfile` qui définit `value` pour inclure les balises `enabled` et `isUpsert`, toutes deux définies sur `true`, et un `path` vers `unifiedIdentity` qui définit `value` pour inclure la balise `enabled` définie sur `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**Réponse**

Une requête PATCH réussie renvoie un statut HTTP 200 (OK) et un tableau contenant l’identifiant du jeu de données mis à jour. Cet identifiant doit correspondre à celui envoyé dans la requête PATCH. Les balises `unifiedProfile` et `unifiedIdentity` ont maintenant été activées et configurées pour les mises à jour d’attributs.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## Étapes suivantes

Votre jeu de données activé pour Profil et upsert peut désormais être utilisé par les workflows d’ingestion par lots pour mettre à jour les données de profil. Pour en savoir plus sur l’ingestion de données dans Adobe Experience Platform, commencez par lire la [présentation de l’ingestion des données](../../ingestion/home.md).
