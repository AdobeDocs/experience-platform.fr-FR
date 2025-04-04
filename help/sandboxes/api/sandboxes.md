---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des sandbox
solution: Experience Platform
title: Point d’entrée de l’API Sandbox Management
description: Le point d’entrée /sandbox de l’API Sandbox vous permet de gérer les sandbox par programmation dans Adobe Experience Platform.
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 49%

---

# Point d’entrée de la gestion des sandbox

Les sandbox de Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre environnement de production. Le point d’entrée `/sandboxes` de l’API [!DNL Sandbox] vous permet de gérer les sandbox par programmation dans Experience Platform.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de sandbox {#list}

Vous pouvez répertorier tous les sandbox appartenant à votre organisation (actifs ou non) en envoyant une requête GET au point d’entrée `/sandboxes`.

**Format d’API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Paramètre | Description |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pour le filtrage des résultats. Pour plus d’informations, consultez la section sur les [paramètres de requête](./appendix.md#query). |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Réponse**

Une réponse réussie renvoie une liste de sandbox appartenant à votre organisation, y compris des détails tels que `name`, `title`, `state` et `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| Propriété | Description |
| --- | --- |
| `name` | Le nom du sandbox. Cette propriété est utilisée à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage du sandbox. |
| `state` | L’état de traitement actuel du sandbox. Un sandbox peut avoir l’un des états suivants : <br/><ul><li>`creating` : le sandbox a été créé, mais est toujours en cours d’approvisionnement par le système.</li><li>`active` : le sandbox est créé et actif.</li><li>`failed` : en raison d’une erreur, le sandbox n’a pas pu être configuré par le système et est désactivé.</li><li>`deleted` : le sandbox a été désactivé manuellement.</li></ul> |
| `type` | Type de sandbox. Les types de sandbox actuellement pris en charge sont les `development` et les `production`. |
| `isDefault` | Propriété booléenne indiquant si ce sandbox est le sandbox de production par défaut de l’organisation. |
| `eTag` | L’identifiant d’une version spécifique du sandbox. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que le sandbox est modifié. |

## Recherche d’un sandbox {#lookup}

Vous pouvez rechercher un sandbox individuel en effectuant une requête GET comprenant la propriété `name` du sandbox dans le chemin de requête.

**Format d’API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` du sandbox que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère un sandbox nommé « dev-2 ».

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Réponse**

Une réponse réussie renvoie les détails du sandbox, y compris son `name`, `title`, `state` et `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Propriété | Description |
| --- | --- |
| `name` | Le nom du sandbox. Cette propriété est utilisée à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage du sandbox. |
| `state` | L’état de traitement actuel du sandbox. Un sandbox peut avoir l’un des états suivants : <ul><li>**création** : le sandbox a été créé, mais le système continue de le configurer.</li><li>**actif **: le sandbox est créé et actif.</li><li>**échec** : en raison d’une erreur, le système n’a pas pu configurer le sandbox et ce dernier a été désactivé.</li><li>**supprimé** : le sandbox a été désactivé manuellement.</li></ul> |
| `type` | Type de sandbox. Les types de sandbox actuellement pris en charge sont les suivants : `development` et `production`. |
| `isDefault` | Une propriété booléenne indiquant s’il s’agit du sandbox par défaut de l’organisation. Il s’agit généralement du sandbox de production. |
| `eTag` | L’identifiant d’une version spécifique du sandbox. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que le sandbox est modifié. |

## Créer un sandbox {#create}

>[!NOTE]
>
>Lorsqu’un nouveau sandbox est créé, vous devez d’abord l’ajouter à votre profil de produit dans [Adobe Admin Console](https://adminconsole.adobe.com/) avant de commencer à utiliser le nouveau sandbox. Consultez la documentation relative à la [gestion des autorisations pour un profil de produit](../../access-control/ui/permissions.md) pour plus d’informations sur la configuration d’un sandbox en fonction d’un profil de produit.

Vous pouvez créer un nouveau sandbox de développement ou de production en effectuant une requête POST vers le point d’entrée `/sandboxes`.

### Créer une sandbox de développement

Pour créer un sandbox de développement, vous devez fournir un attribut `type` avec une valeur de `development` dans la payload de requête.

**Format d’API**

```http
POST /sandboxes
```

**Requête**

La requête suivante crée un sandbox de développement nommé « acme-dev ».

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant qui sera utilisé pour accéder au sandbox lors de futures requêtes. Cette valeur doit être unique, et il est recommandé de la décrire le plus précisément possible. Cette valeur ne peut pas contenir d’espaces ni de caractères spéciaux. |
| `title` | Nom lisible par l’utilisateur utilisé à des fins d’affichage dans l’interface utilisateur d’Experience Platform. |
| `type` | Type de sandbox à créer. Pour un sandbox hors production, cette valeur doit être `development`. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau sandbox, indiquant que son `state` est « création ».

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Il faut environ 30 secondes pour que les sandbox soient configurés par le système, après quoi leur `state` deviendra « actif » ou « en échec ».

### Création d’un sandbox de production

Pour créer un sandbox de production, vous devez fournir un attribut `type` avec une valeur de `production` dans la payload de la requête.

**Format d’API**

```http
POST /sandboxes
```

**Requête**

La requête suivante crée un sandbox de production nommé « acme ».

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant qui sera utilisé pour accéder au sandbox lors de futures requêtes. Cette valeur doit être unique, et il est recommandé de la décrire le plus précisément possible. Cette valeur ne peut pas contenir d’espaces ni de caractères spéciaux. |
| `title` | Nom lisible par l’utilisateur utilisé à des fins d’affichage dans l’interface utilisateur d’Experience Platform. |
| `type` | Type de sandbox à créer. Pour un sandbox de production, cette valeur doit être `production`. |

**Réponse**

Une réponse réussie renvoie les détails du nouveau sandbox, indiquant que son `state` est « création ».

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>Il faut environ 30 secondes pour que les sandbox soient configurés par le système, après quoi leur `state` deviendra « actif » ou « en échec ».

## Mise à jour d’un sandbox {#put}

Vous pouvez mettre à jour un ou plusieurs champs d’un sandbox en effectuant une requête PATCH incluant le `name` du sandbox dans le chemin de requête et la propriété à mettre à jour dans le payload de la requête.

>[!NOTE]
>
>Actuellement, seule la propriété `title` d’un sandbox peut être mise à jour.

**Format d’API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` du sandbox que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour la propriété `title` du sandbox nommé « acme ».

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) avec les détails du sandbox mis à jour.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Réinitialisation d’un sandbox {#reset}

Les sandbox disposent d’une fonctionnalité de « réinitialisation d’usine » qui supprime toutes les ressources autres que celles par défaut d’un sandbox. Vous pouvez réinitialiser un sandbox en effectuant une requête PUT comprenant le `name` du sandbox dans le chemin d’accès de la requête.

**Format d’API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` du sandbox que vous souhaitez réinitialiser. |
| `validationOnly` | Paramètre facultatif qui vous permet d’effectuer une vérification avant vol sur l’opération de réinitialisation du sandbox sans effectuer la requête réelle. Définissez ce paramètre sur `validationOnly=true` pour vérifier si le sandbox que vous êtes sur le point de réinitialiser contient des données Adobe Analytics, Adobe Audience Manager ou de partage de segment. |

**Requête**

La requête suivante réinitialise un sandbox nommé « acme-dev ».

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Propriété | Description |
| --- | --- |
| `action` | Ce paramètre doit être fourni dans le payload de la requête avec une valeur « reset » pour réinitialiser le sandbox. |

**Réponse**

>[!NOTE]
>
>Une fois qu’un sandbox est réinitialisé, il faut environ 30 secondes pour que le système l’approvisionne.

Une réponse réussie renvoie les détails du sandbox mis à jour, indiquant que son `state` est « resetting ».

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

Le sandbox de production par défaut et les sandbox de production créés par l’utilisateur ne peuvent pas être réinitialisés si le graphique d’identités qui y est hébergé est également utilisé par Adobe Analytics pour la fonctionnalité [Analyses entre appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=fr) ou si le graphique d’identités qui y est hébergé est également utilisé par Adobe Audience Manager pour la fonctionnalité [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr).

Voici une liste des exceptions possibles qui peuvent empêcher la réinitialisation d’un sandbox :

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

Vous pouvez procéder à la réinitialisation d’un sandbox de production utilisé pour le partage bidirectionnel de segments avec [!DNL Audience Manager] ou [!DNL Audience Core Service] en ajoutant le paramètre `ignoreWarnings` à votre requête.

**Format d’API**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` du sandbox que vous souhaitez réinitialiser. |
| `ignoreWarnings` | Paramètre facultatif qui vous permet d’ignorer la vérification de validation et de forcer la réinitialisation d’un sandbox de production utilisé pour le partage de segments bidirectionnel avec [!DNL Audience Manager] ou [!DNL Audience Core Service]. Ce paramètre ne peut pas être appliqué à un sandbox de production par défaut. |

**Requête**

La requête suivante réinitialise un sandbox de production nommé « acme ».

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**Réponse**

Une réponse réussie renvoie les détails du sandbox mis à jour, indiquant que son `state` est « resetting ».

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## Suppression d’un sandbox {#delete}

>[!IMPORTANT]
>
>Impossible de supprimer le sandbox de production par défaut.

Vous pouvez supprimer un sandbox en effectuant une requête DELETE qui inclut le `name` du sandbox dans le chemin de la requête.

>[!NOTE]
>
>L’exécution de cet appel API met à jour la propriété `status` du sandbox sur « supprimé » et la désactive. Les requêtes GET peuvent toujours récupérer les détails du sandbox après sa suppression.

**Format d’API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | `name` du sandbox que vous souhaitez supprimer. |
| `validationOnly` | Paramètre facultatif qui vous permet d’effectuer une vérification en amont sur l’opération de suppression de sandbox sans effectuer la requête réelle. Définissez ce paramètre sur `validationOnly=true` pour vérifier si le sandbox que vous êtes sur le point de réinitialiser contient des données Adobe Analytics, Adobe Audience Manager ou de partage de segment. |
| `ignoreWarnings` | Paramètre facultatif qui vous permet d’ignorer la vérification de validation et de forcer la suppression d’un sandbox de production créé par l’utilisateur ou l’utilisatrice qui est utilisé pour le partage de segments bidirectionnel avec [!DNL Audience Manager] ou [!DNL Audience Core Service]. Ce paramètre ne peut pas être appliqué à un sandbox de production par défaut. |

**Requête**

La requête suivante supprime un sandbox de production nommé « acme ».

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie les détails mis à jour du sandbox, indiquant que son `state` est « supprimé ».

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
