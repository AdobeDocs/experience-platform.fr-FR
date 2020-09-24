---
keywords: Experience Platform;home;popular topics;manage decisioning;decisioning objects api;manage decisioning objects
solution: Experience Platform
title: Gestion des entités du service de prise de décision à l’aide d’API
topic: tutorial
type: Tutorial
description: 'Ce document fournit un tutoriel expliquant comment travailler avec les entités commerciales du service de prise de décision à l’aide des API d’Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '7239'
ht-degree: 95%

---


# Gestion des objets et des règles de prise de décision à l’aide d’API

This document provides a tutorial for working with the business entities of [!DNL Decisioning Service] using Adobe Experience Platform APIs.

Le tutoriel se décompose en deux parties :

- La [première partie](#managing-repository-entities-using-apis) présente les API de référentiel générique pour la gestion des objets commerciaux. Ces API sont génériques dans le sens où elles fournissent des fonctionnalités de création, de lecture, de mise à jour, de suppression et de recherche pour **tous** types d’objets commerciaux. Le modèle d’API général est décrit et la relation avec le langage d’application hypertexte (HAL) est expliquée.

- Sur la base des connaissances acquises sur les API de référentiel, la [deuxième partie](#creating-and-managing-offer-decisioning-entities-using-apis) se concentre sur les entités commerciales gérées via les API de référentiel. Puisque les mêmes API sont appliquées, les seules différences entre la gestion de deux entités différentes, telles qu’une activité et une règle commerciale, sont le payload de requête et de réponse, ainsi que les valeurs d’en-tête nécessaires pour indiquer le type d’objet géré.

## Prise en main

This tutorial requires a working understanding of the [!DNL Experience Platform] services and the API conventions. The [!DNL Platform] repository is a service used by several other [!DNL Platform] services to store business objects and various types of metadata. Il offre une méthode sécurisée et flexible pour gérer et interroger ces objets en vue de les utiliser dans plusieurs services d’exécution. Le [!DNL Decisioning Service] est l&#39;un de ceux-là. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux éléments suivants :

- [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
- [[ !Service de prise de décision DNL]](./../home.md): Explique les concepts et les composants utilisés pour la prise de décision d’expérience en général et la prise de décision d’Offre en particulier. Illustre les stratégies utilisées pour choisir la meilleure option à présenter lors de l’expérience client.
- [[ ! DNL Profil Requête Language (PQL)]](../../segmentation/pql/overview.md): PQL est un langage puissant pour écrire des expressions sur des instances XDM. Il est utilisé pour définir des règles de décision.

The following sections provide additional information that you will need to know in order to successfully make calls to the [!DNL Platform] APIs.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Conventions d’API de référentiel

[!DNL Decisioning Service] est contrôlée par un certain nombre d’objets commerciaux qui sont liés les uns aux autres. All business objects are stored in the [!DNL Platform’s] Business Object Repository. Une caractéristique clé de ce référentiel est que les API sont indépendantes du type d’objet commercial. Contrairement aux API POST, GET, PUT, PATCH ou DELETE indiquant le type de ressources au point de terminaison de l’API, les 6 points de terminaison génériques uniques existants acceptent ou renvoient un paramètre indiquant le type d’objet lorsque cette clarification est nécessaire. Le schéma doit être enregistré dans le référentiel, mais le référentiel peut être utilisé pour un ensemble non limité de types d’objets.

Outre les en-têtes répertoriés ci-dessus, les API destinées à créer, lire, mettre à jour, supprimer et interroger les objets du référentiel présentent les conventions suivantes :

- Le chemin d’accès des points de terminaison de toutes les API de référentiel commencent par `https://platform.adobe.io/data/core/xcore/`.

Les formats de payload d’API sont négociés avec un en-tête `Accept` ou `Content-Type`. Les formats de message dans l’en-tête `Accept` ou `Content-Type` sont indiqués par une valeur `application/vnd.adobe.platform.xcore.{FORMAT}+json` où {FORMAT} dépend du message de requête ou de réponse de l’API de référentiel spécifique, selon le tableau suivant.

| Variante de FORMAT | Description de l’entité de requête ou de réponse |
| --- | --- |
| HAL<br>suivi d’un paramètre `schema={schemaId}` | Le message contient une instance décrite par un schéma JSON indiqué par le schéma du paramètre de format. L’instance est enveloppée par une propriété JSON `_instance`. Les autres propriétés de niveau supérieur du payload de réponse spécifient les informations du référentiel disponibles pour toutes les ressources.  Les messages conformes au format HAL présentent une propriété `_links` qui contient des références au format HAL. |
| `patch.hal` | Le message contient un payload PATCH JSON, en supposant que l’instance à corriger soit conforme au HAL. Cela signifie que les propriétés d’instance et les liens HAL de l’instance peuvent être corrigés. Notez qu’il existe des restrictions quant aux propriétés qui peuvent être mises à jour par le client. |
| `home.hal` | Le message contient une représentation au format JSON d’une ressource de document d’origine pour le référentiel. |
| xdm.receipt | Le message contient une réponse au format JSON pour une opération de création, de mise à jour (complète ou avec correctif) ou de suppression. Les reçus contiennent des données de contrôle indiquant la révision de l’instance sous la forme d’un ETag. |

L’utilisation de chaque **variante de format** dépend de l’API spécifique :

| API | En-tête Content-Type | En-tête Accept |
| --- | --- | --- |
| Créer une instance <br/>Créer un conteneur | `hal`<br/>avec paramètre de schéma | `xdm.receipt` |
| Mettre à jour une instance<br/>Mettre à jour un conteneur | `hal`<br/>avec paramètre de schéma | `xdm.receipt` |
| Corriger une instance | `patch.hal` | `xdm.receipt` |
| Supprimer une instance<br/>Supprimer un conteneur | N/A | `xdm.receipt` |
| Lire une instance<br/>Lire un conteneur | N/A | `hal` avec paramètre `schema` |
| Lister des instances<br/>Lister des conteneurs | N/A | `hal` avec paramètre `schema` spécial `https://ns.adobe.com/experience/xcore/hal/results` |
| Rechercher des instances | N/A | HAL avec paramètre `schema` spécial `https://ns.adobe.com/experience/xcore/hal/results` |
| Lire la racine du référentiel | N/A | `home.hal` |

Pour les API de création, de mise à jour et de lecture de conteneur, le schéma de paramètre de format a la valeur `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` est le premier paramètre de chemin d’accès pour les API d’instance. Toutes les entités commerciales résident dans ce que l’on appelle un conteneur. Un conteneur est un mécanisme d’isolement qui permet de séparer différentes préoccupations. Le premier élément de chemin d’accès pour les API d’instance de référentiel suivant le point de terminaison général est `containerId`. L’identifiant est obtenu à partir de la liste des conteneurs accessibles par l’appelant. Par exemple, l’API permettant de créer une instance dans un conteneur est `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

La liste des conteneurs accessibles est obtenue en appelant le point de terminaison racine du référentiel « / » avec une requête HTTP GET utilisant les en-têtes standard.

## Gestion de l’accès aux conteneurs

Un administrateur peut regrouper des entités principales, des ressources et des autorisations d’accès similaires dans des profils. Cette méthode est compatible avec l’[interface utilisateur d’Adobe Admin Console](https://adminconsole.adobe.com) et permet de réduire la charge de gestion. Pour créer des profils et y affecter des utilisateurs, vous devez être un administrateur de produit pour Adobe Experience Platform.

Il suffit de créer des profils de produit qui correspondent à certaines autorisations en une seule étape, puis d’ajouter des utilisateurs à ces profils. Les profils agissent comme des groupes ayant reçu des autorisations, et chaque utilisateur réel ou technique de ce groupe hérite de ces autorisations.

### Liste des conteneurs accessibles aux utilisateurs et aux intégrations

Lorsque l’administrateur a autorisé les utilisateurs réguliers ou les intégrations à accéder aux conteneurs, ces derniers s’affichent dans la liste « Origine » du référentiel. La liste peut différer selon les utilisateurs et les intégrations, car il s’agit d’un sous-ensemble de tous les conteneurs accessibles pour l’appelant. La liste des conteneurs peut être filtrée selon leur association au contexte du produit. Le paramètre de filtre `product` peut être répété. Si plusieurs filtres contextuels de produit sont utilisés, ils renvoient l’union des conteneurs ayant des associations avec l’un des contextes de produit fournis. Notez qu’un même conteneur peut être associé à plusieurs contextes de produit.

Le contexte des [!DNL Platform][!DNL Decisioning Service] conteneurs est actuellement `dma_offers`en cours.

>[!NOTE]
>
>Le contexte [!DNL Platform Decisioning Containers] va bientôt changer `acp`. Le filtrage est facultatif, mais les filtres n’utilisant que `dma_offers` auront besoin d’une mise à jour dans une version ultérieure. Pour se préparer à ce changement, les clients peuvent soit n’utiliser aucun filtre, soit utiliser les deux contextes de produit comme filtres.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Réponse**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Notez que `instanceId` est listé dans les résultats. Il est utilisé comme paramètre `containerId` dans les API pour lire et manipuler les objets commerciaux standard.

La liste est déjà filtrée pour afficher les utilisateurs en fonction de leurs privilèges d’accès, mais elle peut être filtrée davantage à l’aide d’une requête de propriété.

## API génériques pour gérer les entités

### Création d’instances

L’API permettant de créer une instance dans le référentiel utilise un paramètre de chemin d’accès `containerId` et identifie le type de l’instance dans l’en-tête `Content-Type` à l’aide du paramètre de schéma.

Les propriétés de l’instance sont données dans le payload enveloppé par la propriété `_instance`. Les propriétés de l’instance doivent être conformes au schéma JSON portant l’identifiant de schéma donné.

La propriété HAL `_links` doit être présente, mais elle peut être vide. Cela signifie qu’aucun lien personnalisé n’est défini pour cette instance.

**Requête**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Réponse**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

La réponse contient l’instanceId de l’objet qui vient d’être créé. Cet instanceId est inaltérable, toujours attribué par le référentiel et globalement unique. La valeur sert d’identifiant physique.

En outre, un URI (Universal Resource Identifier) est renvoyé dans la propriété `@id` du payload de réponse si le schéma possède cette propriété. Chaque instance doit avoir une propriété qui sert d’URI et de clé primaire à l’instance. Cet identifiant est utilisé par une autre instance pour créer des relations avec la nouvelle instance, y compris entre différents types. Dans la version actuelle, les URI sont générés par le référentiel et sont contenus dans la propriété `@id`. Les futures versions pourront assouplir cette règle et permettre aux clients de gérer leurs propres valeurs URI et de nommer la propriété qui les contient.

Notez que ces URI ne sont pas des URL et ne permettent pas de récupérer directement la ressource. Pour indiquer cet aspect, l’URI est précédé d’un modèle URI qui ne spécifie aucun protocole de récupération. Toutefois, les URI peuvent être utilisés pour rechercher l’instance à l’aide d’une requête.

La réponse REST comporte un en-tête d’emplacement contenant un composant URL qui peut être utilisé pour récupérer l’instance qui vient d’être créée. Ce composant est une référence URI relative et doit être appliqué à l’URI de base du référentiel. L’URI de base est renvoyé dans l’en-tête `Content-Base`.

La propriété `repo:etag` spécifie la révision de l’instance. Cette valeur peut être utilisée dans les opérations de mise à jour pour assurer la cohérence. L’en-tête HTTP `If-Match` peut être utilisé pour ajouter une condition à un appel API PUT ou PATCH, ce qui garantit qu’aucune autre modification de l’instance n’est accidentellement écrasée. La valeur `repo:etag` est renvoyée à chaque appel de création, de lecture, de mise à jour, de suppression ou d’interrogation. La valeur est utilisée comme valeur dans l’en-tête ` If-Match`, conformément à [la section 3.1 du protocole RFC7232](https://tools.ietf.org/html/rfc7232#section-3.1).

Les autres propriétés indiquent le compte et la clé d’API utilisés pour la création et la dernière modification en date de l’instance. Puisque l’instance a été créée par cet appel, les valeurs respectives sont celles de la requête.

### Recherche d’une instance par identifiant

Une application peut rechercher une instance à l’aide de l’URL dans l’en-tête d’emplacement renvoyé avec l’appel de création.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE]
>
>Même si `instanceId` est fourni comme paramètre de chemin d’accès, les applications ne doivent pas construire le chemin d’accès elles-mêmes, si possible, mais plutôt suivre les liens vers les instances contenues dans la liste et les opérations de recherche. Consultez les sections ‎ 6.4.4 et ‎ 6.4.6 pour plus de détails.

**Réponse**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

Les propriétés JSON de l’instance sont enveloppées par la propriété `_instance` et les autres propriétés de niveau racine contiennent les métadonnées sur l’instance.

La ressource contient également un tableau d’identifiant de schéma JSON. Ce tableau indique les schémas JSON pour lesquels cette instance est validée.

Chaque instance contient un lien HAL de type de relation self qui correspond à la relation self enregistrée par l’IANA (comme défini dans [RFC5988]).

**Test des nouvelles révisions d’une instance**

La valeur `eTag` actuelle de l’instance est renvoyée avec la réponse. Elle permet aux clients d’exécuter des opérations conditionnelles sur l’instance, soit pour éviter de récupérer le même état de ressource, soit pour éviter de remplacer les valeurs d’une révision ultérieure sans que le client en ait connaissance.

L’API de recherche permet à un client de spécifier un paramètre d’en-tête `If-None-Match`. Consultez la définition de ce paramètre HTTP [RFC2616] standard. La valeur de balise d’entité spécifiée par un client est la valeur reçue avec la dernière réponse en date, qui est issue d’un appel API de mise à jour, de lecture, de liste ou de recherche. Notez que la valeur `etag` doit être opaque pour le client et doit être fournie sous la forme d’une chaîne entourée de guillemets.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

L’API de référentiel répond avec l’état 304 Not Modified lorsque la dernière révision en date de l’instance est celle de l’ETag donné.

### Liste des instances d’un schéma : tri et pagination

Les clients ne pourront pas suivre les instances qu’ils créent et, par conséquent, y accéder via l’instanceId physique. L’utilisation de l’API d’instance de lecture constitue une exception. Les clients ignorent également les instances créées par d’autres clients.

Un modèle d’accès plus classique consiste à parcourir le jeu comprenant toutes les instances.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Réponse**

La réponse dépend du `{schemaId}` spécifié. Par exemple, pour « https<span></span>://ns.adobe.com/experience/offer-management/offer-activity&amp;id=xcore:offer-activity:fa24f9e8fc15c73 », la réponse ressemble à ce qui suit.

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE]
>
>Le résultat contient les instances pour le schéma donné ou la première page de cette liste. Notez que les instances peuvent être conformes à plusieurs schémas et peuvent donc apparaître dans plusieurs listes.

Les ressources de la page sont transitoires et en lecture seule, elles ne peuvent pas être mises à jour ou supprimées. Le modèle de pagination offre un accès aléatoire aux sous-ensembles de longues listes sur une longue période, sans conserver aucun état par client.

Pour accéder à une liste d’instances par page de cette manière, vous devez pouvoir définir un tri stable des entrées énumérées par cette liste d’instances. Notez que « stable » ne signifie pas que les instances apparaîtront sur une page prédéterminée. En réalité, lorsqu’un ordre de pages est formé en triant les instances en fonction d’une propriété P et qu’un client met à jour cette propriété P, un autre client peut accéder à cette instance sur une autre page tout en parcourant la liste. En d’autres termes, le modèle favorise le renvoi des résultats plus récents.

Cependant, lorsque l’ordre de tri est basé sur une propriété non modifiable, un ordre de tri « stable » garantit que toutes les instances existantes au début de l’opération de pagination seront atteintes (sauf si elles ont été supprimées au moment où leur page est atteinte). Lorsque cet ordre de tri dépend d’une propriété qui augmente de manière monotone, les instances créées après le début de l’opération de pagination sont également atteintes.

Un client peut fournir des indicateurs sur la taille de page souhaitée, mais il appartient entièrement au référentiel de fournir plus ou moins d’instances sur la page renvoyée. Pour garantir un ordre stable, le service doit ajouter ou supprimer des éléments de la page, afin que la valeur de la propriété de tri soit différente pour toutes les limites de page. Ainsi, la page suivante ne contiendra plus certains éléments de la page précédente ou, dans le pire des cas, elle contiendra les mêmes éléments sur chaque page.

La pagination est contrôlée par les paramètres suivants :

- **`orderBy`** : contient une liste de propriétés triées et séparées par des virgules qui est utilisée pour trier la liste d’instances. La première propriété est utilisée pour le tri principal, la deuxième pour résoudre les égalités du tri principal, etc. Lorsqu’une propriété est spécifiée avec une valeur unique par instance, les égalités sont impossibles et un saut de page peut survenir après chaque élément. Le nom d’une propriété peut être précédé d’un préfixe `+` pour indiquer un ordre ascendant, ou d’un préfixe `-` pour indiquer un ordre descendant en fonction de cette propriété. Si le nom de la propriété n’est pas précédé d’un préfixe, le résultat est trié par ordre ascendant. Si `orderBy` n’est pas spécifié dans la requête, le référentiel utilise la propriété instanceId physique à la place.
- **`start`** : les clients utilisent le paramètre de début pour définir la page qu’ils souhaitent récupérer. Le paramètre de début détermine le début de la page souhaitée. La réponse contient des instances, en commençant par celles dont la valeur de propriété `orderBy` est strictement supérieure (pour l’ordre ascendant) ou strictement inférieure (pour l’ordre descendant) à la valeur spécifiée. Lorsque le paramètre de requête n’est pas spécifié, la réponse utilise par défaut une valeur instanceId qui trie avant le premier identifiant d’instance possible, omettant cette valeur dans la première page.
- **`limit`** : spécifie un entier positif comme indicateur du nombre maximal d’éléments à renvoyer pour une requête donnée. La taille réelle de la réponse peut être inférieure ou supérieure, dû à la nécessité d’offrir un fonctionnement fiable du paramètre de début.

### Filtrage des listes

Le filtrage des résultats de liste est possible et indépendant du mécanisme de pagination. Les filtres peuvent simplement ignorer les instances dans l’ordre des listes ou vous pouvez demander explicitement à inclure uniquement les instances qui répondent à une condition donnée. Un client peut demander à utiliser une expression de propriété comme filtre ou il peut spécifier une liste d’URI à utiliser comme valeurs de clé primaire pour les instances.

- **`property`** : contient le chemin d’accès d’un nom de propriété suivi d’un opérateur de comparaison, lui-même suivi d’une valeur. <br/>
La liste d’instances renvoyée contient les instances pour lesquelles l’expression est vraie. Par exemple, en supposant que l’instance possède une propriété de charge utile 
`status` et les valeurs possibles sont `draft`, `approved`, `archived` puis `deleted` le paramètre de requête `property=_instance.status==approved` ne renvoie que les instances pour lesquelles l’état est approuvé. <br/>
<br/>
La propriété à comparer à la valeur donnée est identifiée sous la forme d’un chemin d’accès. Les composants individuels du chemin d’accès sont séparés par un « . » (par exemple, « _instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1 »).<br/>

Pour les propriétés qui comportent des valeurs de chaîne, numériques ou de date/heure, les opérateurs autorisés sont les suivants : `==`, `!=`, `<`, `<=`, `>` et `>=`. En outre, il est possible d’utiliser un opérateur `~` pour les propriétés avec une valeur de chaîne. L’opérateur `~` correspond à la propriété donnée, en fonction d’une expression régulière. La valeur de chaîne de la propriété doit correspondre à l’expression **intégrale** pour que les entités soient incluses dans les résultats filtrés. Par exemple, si vous cherchez la chaîne `cars` n’importe où dans la valeur de propriété, l’expression régulière doit être `.*cars.*`. Sans `.*` au début ou à la fin, seules les entités dont la valeur de propriété commencerait ou se terminerait, respectivement, par `cars` pourraient correspondre. Pour l’opérateur `~`, la comparaison des caractères de lettre n’est pas sensible à la casse. Au contraire, la comparaison est sensible à la casse pour tous les autres opérateurs.<br/><br/>
Les propriétés de payload ne sont pas les seules à pouvoir être utilisées dans les expressions de filtre. Les propriétés d’enveloppe sont comparées de la même manière, par exemple : `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
Le paramètre de requête `property` peut être répété afin d’appliquer plusieurs conditions de filtre, par exemple pour renvoyer toutes les instances modifiées pour la dernière fois entre deux dates données. Les valeurs de ces expressions doivent être encodées par l’URL. Si aucune expression n’est donnée et que le nom de la propriété est simplement répertorié, les éléments remplissant les conditions sont ceux qui possèdent une propriété portant le nom donné.<br/>
<br/>

- **`id`** : il arrive qu’une liste doive être filtrée par l’URI des instances. Le paramètre de requête `property` peut être utilisé pour filtrer une instance, tandis qu’une liste d’URI peut être fournie à la requête pour obtenir plusieurs instances. Le paramètre `id` est répété et chaque occurrence spécifie une valeur d’URI, `id={URI_1}&id={URI_2},…`. Les valeurs d’URI doivent être encodées par l’URL.

Les résultats paginés sont renvoyés sous la forme d’un type MIME spécial : `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Réponse**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

La réponse contient la liste des éléments de résultat au sein des résultats de propriété JSON, en regard de deux propriétés qui indiquent le nombre de résultats sur cette page et le nombre total d’éléments dans la liste filtrée en commençant par la page qui vient d’être renvoyée.

### Recherche de texte intégral et requêtes structurées

Dans les cas où les clients souhaitent fournir des conditions de filtre et des instances de recherche plus complexes à l’aide de termes contenus dans des propriétés de chaîne, le référentiel propose une API de recherche plus puissante.

**Requête**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

En plus des paramètres de pagination et de filtrage des API de liste, cette API permet aux clients d’ajouter du texte intégral et des paramètres de requête booléens.

La recherche de texte intégral est contrôlée par les paramètres suivants :

- **`q`** : contient une liste de termes non triés, séparés par des espaces et normalisés avant d’être associés aux propriétés de chaîne des instances. Les propriétés de chaîne sont analysées à la recherche de termes et ces termes sont également normalisés. La requête de recherche tente de faire correspondre un ou plusieurs des termes spécifiés dans le paramètre `q`. Les caractères +, -, =, &amp;&amp;, ||, >, &lt;,!, (,), {, }, [,], ^, &quot;, ~, *, ?, : et / ont une signification spéciale pour déterminer les limites des mots dans la chaîne de requête. Ils doivent être précédés d’une barre oblique inverse lorsqu’ils apparaissent dans un jeton qui doit correspondre au caractère. La chaîne de requête peut être entourée de guillemets doubles pour rechercher une correspondance de chaîne exacte et pour échapper des caractères spéciaux.
- **`field`** : si les termes de recherche ne doivent correspondre qu’à un sous-ensemble des propriétés, le paramètre de champ peut indiquer le chemin d’accès à ces propriétés. Le paramètre peut être répété pour indiquer plusieurs propriétés devant faire l’objet d’une correspondance.
- **`qop`** : contient un paramètre de contrôle utilisé pour modifier le comportement de correspondance de la recherche. Lorsque le paramètre est défini sur « and », tous les termes de recherche doivent correspondre. Au contraire, lorsque le paramètre est absent ou que sa valeur est définie sur « or », n’importe quel terme peut compter comme une correspondance.

### Mise à jour et correction des instances

Pour mettre à jour une instance, un client peut soit remplacer toute la liste des propriétés à la fois, soit utiliser une requête PATCH JSON pour manipuler les valeurs de propriété individuelles, y compris les listes.

Dans les deux cas, l’URL de la requête spécifie le chemin d’accès à l’instance physique et la réponse sera un payload de réception JSON, comme celui renvoyé par l’[opération de création](#create-instances). De préférence, un client doit utiliser un en-tête `Location` ou un lien HAL reçu d’un précédent appel API pour cet objet comme chemin d’accès URL complet pour cette API. Si cela n’est pas possible, le client peut construire l’URL à partir du `containerId` et de l’`instanceId`.

**Requête** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Requête** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

La requête PATCH applique les instructions, puis valide l’entité résultante par rapport au schéma et aux mêmes règles d’intégrité de référentiel et d’entité que la requête PUT.

**Contrôle des modifications de valeur de propriété**

Vous pouvez empêcher la définition des propriétés sur la création et/ou la mise à jour à l’aide des annotations suivantes :

- **`"meta:usereditable"`** : booléen. Lorsqu’une requête provient d’un agent utilisateur qui identifie l’appelant à l’aide d’un jeton d’accès de compte technique ou d’utilisateur, les propriétés annotées avec `"meta:usereditable": false` ne doivent pas être présentes dans le payload. Si elles le sont, elles ne doivent pas avoir une valeur différente de celle actuellement définie. Si les valeurs diffèrent, la requête de mise à jour ou de correctif sera rejetée avec un état 422 Unprocessable Entity.
- **`"meta:immutable"`** : booléen. Une fois définies, les propriétés annotées avec `"meta:immutable": true` ne peuvent pas être modifiées. Cela s’applique aux requêtes émanant d’un utilisateur final, de l’intégration d’un compte technique ou d’un service spécial.

**Test de mises à jour concomitantes**

Il existe des conditions dans lesquelles plusieurs clients essaient de mettre à jour une même instance simultanément. Le référentiel est exploité sur un cluster de nœuds informatiques sans gestion centralisée des transactions. Pour éviter que deux clients ne puissent écrire une instance simultanément, les clients peuvent utiliser une requête conditionnelle de mise à jour ou de correctif. En spécifiant la chaîne `etag` dans l’en-tête `If-Match`, le référentiel s’assure que seule la première requête réussit et que les requêtes suivantes des autres clients utilisant la même valeur `etag` échouent. La valeur `etag` change à chaque modification de l’instance. Les clients doivent récupérer l’instance pour obtenir la dernière valeur `etag` en date, puis une seule des différentes tentatives de mise à jour des clients pourra réussir avec cette valeur. Les autres clients seront rejetés avec un message 409 Conflict.

### Suppression des instances

Les instances peuvent être supprimées avec un appel DELETE. De préférence, un client doit utiliser un en-tête `Location` ou un lien HAL reçu d’un précédent appel API comme chemin d’accès URL complet. Si cela n’est pas possible, le client peut construire l’URL à partir du `containerId` et de l’`instanceId` physique.

**Requête**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Réponse**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

Lors de la réception d’une requête de suppression, le référentiel vérifie toutes les autres instances de tous les schémas faisant référence à l’instance à supprimer. Dans un système distribué et hautement disponible, l’intégrité référentielle ne peut pas être vérifiée immédiatement. En présence de relations de clé externe, les contrôles sont exécutés de manière asynchrone. Cela entraîne un léger retard dans la réponse sur le résultat de la requête de suppression. Lorsque ces vérifications sont effectuées, la réponse immédiate inclut l’état 202 Accepted et un lien permettant de vérifier le résultat de l’opération de suppression dans l’en-tête `Location`. Un client doit alors vérifier ce lien pour consulter le résultat.

Si une instance fait référence à l’instance supprimée, le résultat est un rejet de l’opération de suppression. Si aucune autre référence de clé externe n’est découverte, la suppression est terminée. Si le résultat n’est pas encore décidé, la réponse l’indique à l’aide d’une autre réponse présentant un état 202 Accepted et le même en-tête `Location`, et demande au client de continuer à vérifier. Lorsque le résultat est déterminé, la réponse l’indique avec un état 200 Ok et le payload de la réponse contient le résultat de la requête de suppression initiale. Notez qu’une réponse avec un état 200 Ok signifie uniquement que le résultat est connu et que le corps de la réponse contient la confirmation ou le rejet de la requête de suppression.

## Création d’offres et de leurs sous-composants

Les API décrites dans la section précédente s’appliquent uniformément à tous les types d’objets commerciaux. La seule différence entre, par exemple, la création d’une offre et d’une activité, serait l’en-tête `content-type` notant le schéma JSON et le payload JSON de la requête conforme au schéma. Par conséquent, les sections suivantes se concentreront sur ces schémas et les relations entre eux.

Lors de l’utilisation des API avec le type de contenu `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`, les propriétés de l’instance sont intégrées dans la propriété `_instance` à côté de laquelle il existe une propriété `_links`. Il s’agit du format général dans lequel toutes les instances sont représentées :

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE]
>
>Pour des raisons de concision et ce dans tous les fragments de code JSON, seules les propriétés d’instance sont illustrées, et seules les propriétés d’enveloppe et les sections _links requises sont affichées.

### Propriétés d’offre générales

Les offres sont un type d’option de prise de décision et le schéma JSON des offres hérite des propriétés d’option standard de chaque instance d’option.

- **`@id`** - Identifiant unique pour chaque option et clé primaire qui sert à référencer l’option d’autres objets. Cette propriété est attribuée lorsque l’instance est créée. Elle est inaltérable et non modifiable.
- **`xdm:name`** - Chaque option porte un nom utilisé à des fins de recherche et d’affichage. Le nom n’est pas inaltérable et ne peut pas être utilisé pour identifier l’instance de manière unique. Le nom peut être sélectionné librement, mais il doit être unique dans toutes les instances d’offre.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

Chaque instance d’offre peut comporter un jeu facultatif de propriétés propres à cette instance. Différentes offres peuvent avoir des clés différentes pour ces propriétés, mais les valeurs doivent être des chaînes. Ces propriétés peuvent être utilisées dans les règles de décision et de segmentation. Elles sont également accessibles pour assembler l’expérience décidée, afin de personnaliser davantage les messages.

### Cycle de vie des offres

Toutes les options suivent un flux simple de transition entre les états. Elles commencent dans un état préliminaire, puis leur état est approuvé quand elles sont prêtes. Une fois la date de fin dépassée, elles peuvent passer à l’état archivé. Dans cet état, elles peuvent être supprimées ou réutilisées en les repassant à l’état préliminaire.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Cette propriété est utilisée pour la gestion du cycle de vie de l’instance. La valeur représente un processus utilisé pour indiquer si l’offre est toujours en construction (valeur = draft), si elle peut généralement être envisagée par l’exécution (valeur = approuved) ou si elle ne doit plus être utilisée (valeur = archived).

Une simple opération PATCH sur l’instance est généralement utilisée pour manipuler une propriété `xdm:status` :

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

### Représentations et emplacements

Les offres sont des options de décision qui comportent des représentations de contenu. Lorsqu’une décision est prise, l’option est sélectionnée et son identifiant est utilisé pour obtenir le contenu ou les références de contenu pour l’emplacement à fournir. Une offre peut avoir plusieurs représentations, mais chacune d’elles doit avoir une référence d’emplacement différente. Cela permet de déterminer sans ambiguïté la représentation d’un emplacement donné.
Au cours de l’opération de décision, l’emplacement est déterminé en association avec l’objet d’activité. Les offres qui n’ont pas de représentation avec cet emplacement comme référence sont automatiquement éliminées de la liste des choix.

Avant de pouvoir ajouter des représentations à une offre, les instances d’emplacement doivent exister. Ces instances sont créées avec l’identifiant de schéma `https://ns.adobe.com/experience/offer-management/offer-placement`.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

Une instance d’**emplacement** peut avoir les propriétés suivantes :

- **`xdm:name`** - Contient le nom attribué à l’emplacement pour y faire référence dans les interactions humaines et les interfaces utilisateur.
- **`xdm:description`** - Utilisé pour transmettre des intentions lisibles par l’utilisateur sur la façon dont le contenu à cet emplacement est utilisé dans les diffusions de message générales. Lorsque les canaux de diffusion définissent de nouveaux emplacements, ils peuvent ajouter des informations supplémentaires dans cette propriété, afin qu’un créateur de contenu puisse créer ou sélectionner le contenu en conséquence. Ces instructions ne sont ni interprétées ni appliquées formellement. Cette propriété sert simplement de lieu de communication des intentions.
- **`xdm:channel`** - L’URI d’un canal. Le canal indique la destination souhaitée du contenu dynamique. La contrainte du canal est utilisée non seulement pour indiquer où l’offre sera utilisée, mais aussi pour déterminer le programme de validation ou l’éditeur de contenu utilisé pour l’expérience.
- **`xdm:componentType`** - Un identifiant de modèle, c’est-à-dire un URI, pour le contenu qui peut être affiché à l’emplacement décrit. Les types de composant sont les suivants : lien d’image, HTML ou texte brut. Chaque type de composant peut impliquer un ensemble de propriétés spécifique (un modèle) que l’élément de contenu peut avoir. La liste des types de composant peut être étendue. Il existe trois valeurs de type de composant prédéfinies :
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`** - Contrainte pour les types de média des composants attendus à cet emplacement. Un type de composant peut avoir plusieurs types de média, par exemple différents formats d’image.

Les éléments de **représentation** au sein d’une offre ont une structure d’objet dans la propriété de tableau `xdm:representations`. Chaque élément peut avoir les propriétés suivantes :

- **`xdm:placement`** - Cette propriété contient la référence à l’instance d’emplacement. La valeur est vérifiée lorsque la représentation est ajoutée à l’offre. Une instance d’emplacement avec cet URI doit exister et ne doit pas être marquée comme supprimée. En outre, une vérification est effectuée pour s’assurer qu’une instance d’offre ne comporte pas deux représentations avec la même valeur comme référence d’emplacement.
- **`xdm:components`** - Les composants de contenu sont les fragments associés à une représentation d’offre spécifique. Ces fragments sont ensuite utilisés pour composer l’expérience de l’utilisateur final. Notez que le service de prise de décision ne constitue pas en lui-même l’expérience complète de l’utilisateur final. Les propriétés suivantes font partie du modèle de chaque composant.
   - **`@type`** - Cette propriété identifie le type de composant. On parle également de « modèle de fragment de contenu » pour ce concept. Le `@type` d’un composant est tout simplement un URI de modèle défini par l’application ou le service qui assemble l’expérience de l’utilisateur final.
   - **`repo:id`** - Cette propriété contient un identifiant global unique et inaltérable pour la ressource principale du composant dans le référentiel où l’actif est stocké.
   - **`repo:name`** - Cette propriété contient un nom lisible par l’utilisateur pour l’actif dans le référentiel. Ce nom est défini par l’utilisateur et son caractère unique n’est pas garanti.
   - **`repo:resolveURL`** - Cette propriété contient un localisateur de ressource unique pour lire l’actif dans un référentiel de contenu. Ainsi, il sera plus facile d’obtenir l’actif sans que le client ne comprenne les API à appeler. L’URL renvoie les octets de la ressource principale de l’actif.
   - **`dc:format`** - Cette propriété provient du Dublin Core Metadata Initiative. Le format peut être utilisé pour déterminer le logiciel, le matériel ou tout autre équipement nécessaire pour afficher ou exploiter la ressource. Il est recommandé de sélectionner une valeur dans un vocabulaire contrôlé (par exemple, la liste des types de média Internet définissant les formats de médias informatiques).
   - **`dc:language`** - Cette propriété contient la ou les langues de la ressource. Les langues sont spécifiées dans le code de langue, tel que défini dans l’IETF RFC 3066.

Il existe trois types de composant prédéfinis exprimés dans la propriété `@type` :

- https<span></span>://ns.adobe.com/experience/offer-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-text
- https<span></span>://ns.adobe.com/experience/offer-management/content-component-html

Selon la valeur de la propriété `@type`, `xdm:components` contient des propriétés supplémentaires :

- **`xdm:linkURL`** - Présent lorsque le composant est un lien d’image. Cette propriété contient le lien associé à l’image et vers lequel `user-agent` naviguera lorsque l’utilisateur final interagira avec le contenu de l’offre.
- **`xdm:copyline`** - Utilisé lorsque le composant est textuel. Outre la référence à un actif textuel (par exemple, pour les offres de texte de formulaire long qui peuvent avoir une mise en forme), une chaîne de texte courte peut être directement stockée dans la propriété xdm:copyline.

Des propriétés supplémentaires peuvent être utilisées par les clients pour définir et évaluer les instructions de gestion du contexte. Par exemple, le client de la bibliothèque d’interface utilisateur d’offre ajoute les propriétés facultatives suivantes pour gérer l’affichage plus facilement :

- Dans chaque élément du tableau `xdm:components`, le client d’interface utilisateur de la bibliothèque d’offres ajoute les propriétés suivantes. Ces propriétés ne doivent pas être supprimées ou manipulées sans comprendre l’impact sur l’interface utilisateur :
   - **`offerui:previewThumbnail`** - Il s’agit d’une propriété facultative que l’interface utilisateur de la bibliothèque d’offres utilise pour afficher un rendu de l’actif. Ce rendu n’est pas la même chose que l’actif lui-même. Par exemple, le contenu peut être au format HTML et le rendu peut être une image bitmap approximative. Ce rendu (de qualité inférieure) s’affiche dans le bloc de représentation de l’offre.

Un exemple d’opération PATCH sur une instance d’offre illustre la manipulation des représentations :

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` si l’offre est une offre de secours.

L’opération PATCH peut échouer en l’absence de propriété `xdm:representations`. Dans ce cas, l’opération d’ajout ci-dessus peut être précédée d’une autre opération d’ajout qui crée le tableau `xdm:representations` ou l’opération d’ajout unique définit directement le tableau.
Les schémas et les propriétés décrits sont utilisés pour tous les types d’offre, les offres de personnalisation comme les offres de secours. Les deux sections suivantes portent sur les contraintes et les règles de décision. Elles expliquent les aspects des offres de personnalisation.

## Définition de contraintes d’offre

### Contraintes calendaires

En général, les options de décision peuvent donner une date et une heure de début et de fin qui servent de contraintes calendaires. Les propriétés sont incorporées dans la propriété `xdm:selectionConstraint` :

- **`xdm:startDate`** - Cette propriété indique la date et l’heure de début. La valeur est une chaîne formatée selon les règles RFC 3339, c’est-à-dire sous la forme suivante : 2019-06-13T11:21:23.356Z.
Les options de décision qui n’ont pas atteint leur date et heure de début ne sont pas encore considérées comme éligibles dans le processus de décision.
- **`xdm:endDate`** - Cette propriété indique la date et l’heure de fin. La valeur est une chaîne formatée selon les règles RFC 3339, c’est-à-dire sous la forme suivante : 2019-07-13T11:00:00.000Z.
Les options de décision qui ont dépassé leur date et heure de fin ne sont plus considérées comme éligibles dans le processus de décision.

Vous pouvez modifier une contrainte calendaire à l’aide de l’appel PATCH suivant :

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les offres de secours n’ont aucune contrainte.

### Contraintes de limitation

Une contrainte de limitation est un composant d’option de décision qui définit les paramètres de limitation. La limitation est le processus qui consiste à limiter le nombre de fois où une option peut être proposée pour un profil individuel et pour tous les profils. Les propriétés contiennent une valeur entière qui doit être supérieure ou égale à 1. Les propriétés sont imbriquées dans une propriété `xdm:cappingConstraint` :

- **`xdm:globalCap`** - Une limite globale est une contrainte qui vise le nombre de fois qu’une offre peut être proposée au total.
- **`xdm:profileCap`** - Une limite de profil est une contrainte qui vise le nombre de fois qu’une offre peut être proposée à un certain profil.

La définition ou la modification de la contrainte de limitation sur une offre de personnalisation peut être effectuée avec l’appel PATCH suivant :

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les offres de secours n’ont aucune contrainte.

Pour supprimer les valeurs de limitation, l’opération « add » est remplacée par l’opération « remove ». Notez que les valeurs de limitation existent individuellement et peuvent être définies ou supprimées individuellement.

### Contraintes d’éligibilité

Dans le processus de décision, les offres peuvent être sélectionnées sous condition. Lorsqu’une offre de personnalisation fait référence à une règle d’éligibilité, la condition de la règle doit être vraie pour que l’objet de l’offre soit pris en compte pour un profil donné. Les règles d’éligibilité sont créées et gérées indépendamment des options de décision, et la même règle peut être référencée depuis plusieurs offres de personnalisation.

La référence à la règle est incorporée dans la propriété `xdm:selectionConstraint` :

- **`xdm:eligibilityRule`** - Cette propriété contient une référence à une règle d’éligibilité. La valeur est l’identifiant `@id` d’une instance de schéma https://ns.adobe.com/experience/offer-management/eligibility-rule.

Vous pouvez également ajouter et supprimer une règle à l’aide d’une opération PATCH :

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les offres de secours n’ont aucune contrainte.

Notez que la règle d’éligibilité est incorporée dans la propriété `xdm:selectionConstraint` avec les contraintes calendaires. Les opérations PATCH ne doivent pas essayer de supprimer la totalité de la propriété `SelectionConstraint`.

## Définition de la priorité d’une offre

Les options de décision admissibles seront classées afin de déterminer la meilleure option pour le profil donné. Pour prendre en charge le classement et fournir une valeur par défaut lorsque le classement n’est pas déterminé par un autre mécanisme, une priorité de base peut être définie pour chaque offre de personnalisation.
La priorité de base est incorporée dans la propriété `xdm:rank` :

- **`xdm:priority`** - Cette propriété représente l’ordre par défaut dans lequel une offre est préférée à une autre lorsqu’il n’y a pas d’ordre de classement spécifique connu pour le profil. Après comparaison de la valeur de priorité, si deux offres de personnalisation ou plus sont toujours à égalité, une offre de personnalisation aléatoire est choisie et utilisée dans la proposition d’offre. La valeur de cette propriété doit être une valeur entière supérieure ou égale à 0.

Vous pouvez ajuster la priorité de base avec l’appel PATCH suivant :

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`. Les offres de secours ne présentent pas de propriétés de classement.

## Gestion des règles de décision

Les règles d’éligibilité contiennent les conditions évaluées pour déterminer si une option de décision donnée est admissible pour un profil donné. L’association d’une règle à une ou plusieurs options de décision définit implicitement que la règle doit être vraie pour que la ou les options soient envisagées pour cet utilisateur. La règle peut contenir des tests sur des attributs de profil, évaluer des expressions impliquant des événements d’expérience pour ce profil ou encore inclure des données de contexte transmises à la requête de décision. Par exemple, une condition peut être décrite comme suit :

> « Inclure les personnes ayant un statut d’élite, ayant pris l’avion trois fois au cours des six derniers mois et présentant le numéro de vol du vol actuel. »

Les instances sont créées à l’aide de l’identifiant de schéma
https://ns.adobe.com/experience/offer-management/eligibility-rule. La propriété `_instance` de l’appel de création ou de mise à jour se présente comme suit :

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

La valeur de la propriété de condition de la règle contient une expression PQL. Les données de contexte sont référencées via l’expression de chemin d’accès spécial @{schemaID}.

Rules naturally align with segments in the [!DNL Experience Platform] and often a rule will simply reuse a segment’s intent by testing a profile’s `segmentMembership` property. La propriété `segmentMembership` contient les résultats des conditions de segment déjà évaluées. Cela permet à une organisation de définir une seule fois les audiences spécifiques aux domaines, de le nommer et d’évaluer une seule fois les conditions.

## Gestion des collections d’offres

### Création d’offres de balises et de balisage

Les offres peuvent être organisées en collections où chaque collection définit la condition de filtre à appliquer. Actuellement, l’expression de filtre dans une collection peut avoir l’une des deux formes suivantes :

1. Le paramètre `@id` de l’offre doit correspondre à un identifiant de la liste pour que l’offre soit dans la collection. Ce filtre est une simple énumération des URI des offres dans la collection.
2. Une offre peut avoir une liste de références de balise et le filtre de la collection se compose d’une liste de balises. L’offre se trouve dans la collection lorsque :\
   a. l’une des balises du filtre correspond à l’une des balises de l’offre ;\
   b. toutes les balises du filtre correspondent à l’une des balises de l’offre.

Les balises sont des instances simples auxquelles peuvent être liées des instances d’offre. Ce sont des instances en elles-mêmes et elles possèdent un nom pour les afficher. Le nom doit être unique parmi toutes les instances afin de faciliter leur affichage dans l’interface utilisateur.

Les objets de balise permettent d’établir une classification au sein des options de décision (offres). Une balise peut être liée à de nombreuses offres, et une offre peut avoir de nombreuses références de balise. Une catégorie d’offres est établie en faisant référence à toutes les offres liées à un ensemble donné d’instances de balise.

Les instances de balise sont créées à l’aide de l’identifiant de schéma spécifique
https://ns.adobe.com/experience/offer-management/tag. La propriété `_instance` de l’appel de création ou de mise à jour se présente comme suit :

```json
{
  "xdm:name": "credit card"
} 
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/tag`.


Une instance d’offre peut être créée avec la liste de références de balise, comme suit :

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Une autre solution consiste à appliquer un correctif pour modifier sa liste de balises :

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

Pour ces deux cas, référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/personalized-offer`.

Notez que la propriété `xdm:tags` doit déjà exister pour que l’opération d’ajout réussisse. S’il n’existe aucune balise dans une instance, l’opération PATCH peut d’abord ajouter la propriété de tableau, puis ajouter une référence de balise à ce tableau.

### Définition des filtres pour les collections d’offres

Les instances de filtre sont créées à l’aide de l’identifiant de schéma
https://ns.adobe.com/experience/offer-management/offer-filter. La propriété `_instance` de l’appel de création ou de mise à jour peut se présenter comme suit :

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - Cette propriété indique si le filtre est défini à l’aide de balises ou s’il fait directement référence à des offres à l’aide de leurs identifiants. Lorsque le filtre est défini pour l’utilisation de balises, le type de filtre peut indiquer si toutes les balises doivent correspondre aux balises d’une offre spécifique ou si l’une des balises données est suffisante pour que l’offre soit admissible pour le filtre. Les valeurs valides de cette propriété enum sont les suivantes :
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - Une propriété contient un tableau d’URI qui sont des références à des instances d’offre ou de balise, selon la valeur de `xdm:filterType`.

L’appel suivant illustre la représentation de la propriété `_instance` de l’appel de création ou de mise à jour lorsque des offres sont directement référencées :

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Gestion des activités

Une activité d’offre sert à contrôler le processus de prise de décision. Elle spécifie le filtre d’offre appliqué à l’inventaire complet afin de réduire le nombre d’offres par rubrique/catégorie, l’emplacement afin de limiter l’inventaire aux offres tenant dans l’espace réservé, et une option de secours au cas où les contraintes combinées rendraient toutes les options de personnalisation (offres) disponibles inadmissibles.

Les instances d’activité sont créées à l’aide de l’identifiant de schéma
`https://ns.adobe.com/experience/offer-management/offer-activity`. La propriété `_instance` de l’appel de création ou de mise à jour se présente comme suit :

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - Cette propriété obligatoire contient le nom de l’activité. Le nom s’affiche dans différentes interfaces utilisateur.
- **`xdm:status`** - Cette propriété est utilisée pour la gestion du cycle de vie de l’instance. La valeur représente un processus utilisé pour indiquer si l’activité est toujours en construction (valeur = draft), si elle peut généralement être envisagée par l’exécution (valeur = live) ou si elle ne doit plus être utilisée (valeur = archived).
- **`xdm:placement`** - Une propriété obligatoire contenant une référence à un emplacement d’offre appliqué à l’inventaire lorsqu’une décision est prise dans le contexte de cette activité. La valeur est l’URI (`@id`) de l’emplacement d’offre utilisé.
- **`xdm:filter`** - Une propriété obligatoire contenant une référence à un filtre d’offre appliqué à l’inventaire lorsqu’une décision est prise dans le contexte de cette activité. La valeur est l’URI (`@id`) du filtre d’offre utilisé.
- **`xdm:fallback`** - Une propriété obligatoire contenant une référence à une offre de secours. Une offre de secours est utilisée lorsque la prise de décision écarte toutes les offres de personnalisation. La valeur est l’URI (`@id`) d’une instance d’offre de secours.

### Gestion des offres de secours

Avant de pouvoir créer des instances d’activité, une offre de secours admissible pour l’emplacement de l’activité doit exister. Les instances d’offre de secours sont créées à l’aide de l’identifiant de schéma
`https://ns.adobe.com/experience/offer-management/fallback-offer`. La propriété `_instance` de l’appel de création ou de mise à jour contient les mêmes propriétés générales qu’une offre de personnalisation, mais elle ne peut pas avoir d’autres contraintes.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Référez-vous à [Mise à jour et correction des instances](#updating-and-patching-instances) pour consulter la syntaxe cURL complète. Le paramètre `schemaId` doit être `https://ns.adobe.com/experience/offer-management/fallback-offer`.

