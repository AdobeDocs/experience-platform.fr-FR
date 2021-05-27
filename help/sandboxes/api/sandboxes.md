---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide de développement des environnements de test
solution: Experience Platform
title: Point de terminaison de l’API de gestion des environnements de test
topic-legacy: developer guide
description: Le point de terminaison /sandbox dans l’API Sandbox vous permet de gérer par programmation les environnements de test dans Adobe Experience Platform.
source-git-commit: f84898a87a8a86783220af7f74e17f464a780918
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 53%

---

# Point d’entrée de gestion des environnements de test

Les environnements de test d’Adobe Experience Platform fournissent des environnements de développement isolés qui vous permettent de tester des fonctionnalités, d’exécuter des opérations et de créer des configurations personnalisées sans affecter votre environnement de production. Le point de terminaison `/sandboxes` de l’API [!DNL Sandbox] vous permet de gérer par programmation les environnements de test dans Platform.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼAPI [[!DNL Sandbox] ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml). Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture d’exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir les appels à une API Experience Platform.

## Récupération d’une liste d’environnements de test {#list}

Vous pouvez répertorier tous les environnements de test appartenant à votre organisation IMS (principal ou non) en effectuant une requête GET sur le point de terminaison `/sandboxes` .

**Format d’API**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| Paramètre | Description |
| --------- | ----------- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs en fonction desquels filtrer les résultats. Voir la section [Paramètres de requête](./appendix.md#query) pour plus d’informations. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie une liste d’environnements de test appartenant à votre organisation, y compris des détails tels que `name`, `title`, `state` et `type`.

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
| `name` | Le nom de l’environnement de test. Cette propriété est utilisée à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage de l’environnement de test. |
| `state` | L’état de traitement actuel de l’environnement de test. Un environnement de test peut avoir l’un des états suivants : <br/><ul><li>`creating`: L’environnement de test a été créé, mais le système continue de le configurer.</li><li>`active`: L’environnement de test est créé et principal.</li><li>`failed`: En raison d’une erreur, le système n’a pas pu configurer l’environnement de test et est désactivé.</li><li>`deleted`: L’environnement de test a été désactivé manuellement.</li></ul> |
| `type` | Type d’environnement de test. Les types d’environnements de test actuellement pris en charge sont `development` et `production`. |
| `isDefault` | Une propriété booléenne indiquant si cet environnement de test est l’environnement de test de production par défaut pour l’organisation. |
| `eTag` | L’identifiant d’une version spécifique de l’environnement de test. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que l’environnement de test est modifié. |

## Recherche d’un environnement de test {#lookup}

Vous pouvez rechercher un environnement de test individuel en effectuant une requête GET comprenant la propriété `name` de l’environnement de test dans le chemin de requête.

**Format d’API**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` de l’environnement de test que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère un environnement de test nommé « dev-2 ».

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une réponse réussie renvoie les détails de l’environnement de test, y compris son `name`, `title`, `state` et `type`.

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
| `name` | Le nom de l’environnement de test. Cette propriété est utilisée à des fins de recherche dans les appels API. |
| `title` | Le nom d’affichage de l’environnement de test. |
| `state` | L’état de traitement actuel de l’environnement de test. L’état d’un environnement de test peut correspondre à l’un des suivants : <ul><li>**création** : l’environnement de test a été créé, mais le système continue de le configurer.</li><li>**actif** : l’environnement de test est créé et actif.</li><li>**échec** : en raison d’une erreur, le système n’a pas pu configurer l’environnement de test et a été désactivé.</li><li>**supprimé** : l’environnement de test a été désactivé manuellement.</li></ul> |
| `type` | Type d’environnement de test. Les types d’environnements de test actuellement pris en charge sont les suivants : `development` et `production`. |
| `isDefault` | Une propriété booléenne indiquant s’il s’agit de l’environnement de test par défaut de l’organisation. Il s’agit généralement de l’environnement de test de production. |
| `eTag` | L’identifiant d’une version spécifique de l’environnement de test. Utilisée pour le contrôle des versions et une mise en cache efficace, cette valeur est mise à jour chaque fois que l’environnement de test est modifié. |

## Création d’un environnement de test {#create}

Vous pouvez créer un environnement de test de développement ou de production en envoyant une requête de POST au point de terminaison `/sandboxes` .

### Création d’un environnement de test de développement

Pour créer un environnement de test de développement, vous devez fournir un attribut `type` avec la valeur `development` dans le payload de la requête.

**Format d’API**

```http
POST /sandboxes
```

**Requête**

La requête suivante crée un nouvel environnement de test de développement nommé &quot;acme-dev&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| Propriété | Description |
| --- | --- |
| `name` | Identifiant qui sera utilisé pour accéder à l’environnement de test lors de futures requêtes. Cette valeur doit être unique, et il est recommandé de la décrire le plus précisément possible. Cette valeur ne peut pas contenir d’espaces ni de caractères spéciaux. |
| `title` | Nom compréhensible utilisé à des fins d’affichage dans l’interface utilisateur de Platform. |
| `type` | Type d’environnement de test à créer. Pour un environnement de test hors production, cette valeur doit être `development`. |

**Réponse**

Une réponse réussie renvoie les détails du nouvel environnement de test, indiquant que son `state` est « création ».

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
>Les environnements de test prennent environ 30 secondes pour être configurés par le système, après quoi leur `state` deviendra &quot;principal&quot; ou &quot;échec&quot;.

### Création d’un environnement de test de production

Pour créer un environnement de test de production, vous devez fournir un attribut `type` avec la valeur `production` dans le payload de la requête.

**Format d’API**

```http
POST /sandboxes
```

**Requête**

La requête suivante crée un nouvel environnement de test de production nommé &quot;acme&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Identifiant qui sera utilisé pour accéder à l’environnement de test lors de futures requêtes. Cette valeur doit être unique, et il est recommandé de la décrire le plus précisément possible. Cette valeur ne peut pas contenir d’espaces ni de caractères spéciaux. |
| `title` | Nom compréhensible utilisé à des fins d’affichage dans l’interface utilisateur de Platform. |
| `type` | Type d’environnement de test à créer. Pour un environnement de test de production, cette valeur doit être `production`. |

**Réponse**

Une réponse réussie renvoie les détails du nouvel environnement de test, indiquant que son `state` est « création ».

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
>Les environnements de test prennent environ 30 secondes pour être configurés par le système, après quoi leur `state` deviendra &quot;principal&quot; ou &quot;échec&quot;.

## Mise à jour d’un environnement de test {#put}

Vous pouvez mettre à jour un ou plusieurs champs d’un environnement de test en effectuant une requête PATCH incluant le `name` de l’environnement de test dans le chemin de requête et la propriété à mettre à jour dans le payload de la requête.

>[!NOTE]
>
>Actuellement, seule la propriété `title` d’un environnement de test peut être mise à jour.

**Format d’API**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` de l’environnement de test que vous souhaitez mettre à jour. |

**Requête**

La requête suivante met à jour la propriété `title` de l’environnement de test nommé &quot;acme&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 (OK) avec les détails de l’environnement de test mis à jour.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## Réinitialisation d’un environnement de test {#reset}

>[!IMPORTANT]
>
>L’environnement de test de production par défaut ne peut pas être réinitialisé si le graphique d’identités qui y est hébergé est également utilisé par Adobe Analytics pour la fonction [Analyses entre appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) ou si le graphique d’identités qui y est hébergé est également utilisé par Adobe Audience Manager pour la fonction [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).

Les environnements de test de développement disposent d’une fonctionnalité de réinitialisation supprimant toutes les ressources de l’environnement de test autres que celles par défaut. Vous pouvez réinitialiser un environnement de test en effectuant une requête PUT comprenant le `name` de l’environnement de test dans le chemin d’accès de la requête.

**Format d’API**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | La propriété `name` de l’environnement de test que vous souhaitez réinitialiser. |

**Requête**

La requête suivante réinitialise un environnement de test nommé &quot;acme-dev&quot;.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| Propriété | Description |
| --- | --- |
| `action` | Ce paramètre doit être fourni dans le payload de la requête avec une valeur « reset » pour réinitialiser l’environnement de test. |

**Réponse**

Une réponse réussie renvoie les détails de l’environnement de test mis à jour, indiquant que son `state` est « resetting ».

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

>[!NOTE]
>
>Une fois qu’un environnement de test est réinitialisé, il faut compter environ 30 secondes pour qu’il soit configuré par le système. Une fois la configuration effectuée, le `state` de l’environnement de test prend la valeur « active » ou « failed ».

Le tableau suivant contient des exceptions possibles qui peuvent empêcher la réinitialisation d’un environnement de test :

| Code erreur | Description |
| --- | --- |
| `2074-400` | Cet environnement de test ne peut pas être réinitialisé, car le graphique d’identités hébergé dans cet environnement de test est également utilisé par Adobe Analytics pour la fonctionnalité Analytics sur l’ensemble des appareils (CDA). |
| `2075-400` | Cet environnement de test ne peut pas être réinitialisé, car le graphique d’identités hébergé dans cet environnement de test est également utilisé par Adobe Audience Manager pour la fonctionnalité Destinations basées sur les personnes (PBD) . |
| `2076-400` | Cet environnement de test ne peut pas être réinitialisé, car le graphique d’identités hébergé dans cet environnement de test est également utilisé par Adobe Audience Manager pour la fonctionnalité Destinations basées sur les personnes (PBD) , ainsi que par Adobe Analytics pour la fonctionnalité Analyses entre appareils (CDA) . |
| `2077-400` | Avertissement : L’environnement de test `{SANDBOX_NAME}` est utilisé pour le partage bidirectionnel de segments avec Adobe Audience Manager ou le service principal Audience. |

## Suppression d’un environnement de test {#delete}

>[!IMPORTANT]
>
>L’environnement de test de production par défaut ne peut pas être supprimé.

Vous pouvez supprimer un environnement de test en effectuant une requête DELETE qui inclut le `name` de l’environnement de test dans le chemin de la requête.

>[!NOTE]
>
>L’appel de cette API met à jour la propriété `status` de l’environnement de test sur « supprimé » et la désactive. Les requêtes GET peuvent toujours récupérer les détails de l’environnement de test après sa suppression.

**Format d’API**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| Paramètre | Description |
| --- | --- |
| `{SANDBOX_NAME}` | `name` de l’environnement de test que vous souhaitez supprimer. |

**Requête**

La requête suivante supprime un environnement de test nommé &quot;acme-dev&quot;.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Une réponse réussie renvoie les détails mis à jour de l’environnement de test, indiquant que son `state` est « supprimé ».

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
