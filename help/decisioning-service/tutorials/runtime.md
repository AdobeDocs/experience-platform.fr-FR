---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Utilisation du composant d’exécution du service de prise de décision à l’aide d’API
topic: tutorial
description: 'Ce document fournit un tutoriel expliquant comment utiliser les services du composant d’exécution du service de prise de décision à l’aide d’API Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 81%

---


# Utilisation du composant d’exécution du service de prise de décision à l’aide d’API

This document provides a tutorial for working with the runtime services of [!DNL Decisioning Service] using Adobe Experience Platform APIs.

## Prise en main

This tutorial requires a working understanding of the [!DNL Experience Platform] services involved in decisioning and determining the next best offer to present during customer experiences. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux éléments suivants :

- [[ !Service de prise de décision DNL]](./../home.md): Fournit la structure permettant d’ajouter et de supprimer des offres et de créer des algorithmes pour choisir le meilleur à présenter lors de l’expérience d’un client.
- [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
- [[ ! DNL Profil Requête Language (PQL)]](../../segmentation/pql/overview.md): PQL est utilisé pour définir des règles et des filtres.
- [Gestion des objets et des règles de prise de décision à l’aide d’API](./entities.md) : avant d’utiliser le composant d’exécution des services de prise de décision, vous devez configurer les entités associées.

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
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../tutorials/authentication.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

Les requêtes de composant d’exécution nécessitent aussi les éléments suivants :

- x-request-id: `{UUID}`

>[!NOTE]
>
>`UUID`  est une chaîne au format UUID unique au niveau global et ne doit pas être réutilisée pour différents appels API.

[!DNL Decisioning Service] est contrôlée par un certain nombre d’objets commerciaux qui sont liés les uns aux autres. All business objects are stored in [!DNL Platform’s] business object repository, XDM Core Object Repository. Une caractéristique clé de ce référentiel est que les API sont indépendantes du type d’objet commercial. Contrairement aux API POST, GET, PUT, PATCH ou DELETE indiquant le type de ressources au point de terminaison de l’API, les 6 points de terminaison génériques uniques existants acceptent ou renvoient un paramètre indiquant le type d’objet lorsque cette clarification est nécessaire. Le schéma doit être enregistré dans le référentiel, mais le référentiel peut être utilisé pour un ensemble non limité de types d’objets.

Les chemins d’accès des points de terminaison de toutes les API XDM Core Object Repository commencent par `https://platform.adobe.io/data/core/ode/`.

Le premier élément de chemin d’accès suivant le point de terminaison est le `containerId`. Cet identifiant est obtenu via le point de terminaison racine du référentiel XDM Core Object Repository `GET https://platform.adobe.io/data/core/xcore/`.

## Compilation des modèles de décision

L’activation des entités de la logique commerciale s’effectue automatiquement et en continu. Dès qu’une nouvelle option est enregistrée dans le référentiel et est marquée comme « approuvée », elle peut être incluse à l’ensemble des options disponibles. Dès qu’une règle de décision est mise à jour, le jeu de règles est reconstitué et préparé pour l’exécution du composant d’exécution. Lors de cette étape d’activation automatique, toutes les contraintes définies par la logique commerciale qui ne dépendent pas du contexte d’exécution seront évaluées. The results of this activation step are sent to a cache where they are available to the [!DNL Decisioning Service] runtime.

### Effets de placements, filtres et états de cycle de vie

Des offres sont créées en permanence, l’état de leur cycle de vie subit des modifications ou de nouvelles représentations de contenu peuvent leur être envoyées. Le filtre d’offre d’une activité permet de modifier des offres, de les faire correspondre ou d’écarter en les filtrant celles dont les jeux de balises ont été mis à jour. Ce processus peut être relativement complexe, et les applications et services doivent savoir quel sera le jeu de candidats résultant d’une activité. Le composant d’exécution du service de prise de décision fournit une API activité-offre permettant d’écarter en les filtrant les offres non approuvées, celles qui ne correspondent pas au filtre d’offre ou ne disposent d’aucune représentation pour l’emplacement référencé par l’activité.

**Requête**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Réponse**

Le paramètre `activityId` peut être répété dans l’URL et chaque requête peut contenir jusqu’à 30 références d’activité différentes. La réponse sera utile pour détecter les circonstances inattendues liées à la configuration et se présentera comme suit :

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Il y a un délai de quelques secondes entre le moment où les objets sont mis à jour et le moment où la réponse de l’API répercute le mappage activité-offre. La révision de chaque objet étant indiquée dans la réponse, les clients peuvent vérifier si une mise à jour d’objets n’a pas été répercutée.

### API de diagnostic et dépannage

Les activités, offres et règles d’éligibilité sont compilées dans un format interne (catalogue d’offres du composant d’exécution) utilisé par le composant d’exécution du service de prise décision. La compilation permet de détecter des erreurs n’ayant pas été détectées par les vérifications effectuées lors du stockage des objets et de l’établissement des liens dans le référentiel XDM Core Object Repository.

Une API de diagnostic fournie indique toutes les erreurs de compilation identifiées au cours de cette étape et, en l’absence d’erreur, des informations sur le moment de la dernière recompilation.

**Requête**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

Le seul paramètre de cet appel API est `containerId`. Les résultats de toutes les mises à jour de tous les clients qui ont modifié des règles de décision, des offres, des activités ou des filtres d’offres dans ce conteneur. Il y a un délai de quelques secondes entre le moment où les objets sont mis à jour et le moment où la compilation se termine. L’horodatage de la dernière mise à jour et les erreurs éventuelles sont renvoyés dans la réponse à l’appel de diagnostic.

**Réponse**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## Appels API REST pour exécuter des décisions

The REST API is one of the routes for applications running on top of [!DNL Platform] to obtain the next best experience based on the rules, models and constraints that the organization has set for their users. Applications send one of the profile’s identities (profile ID and identity namespace) the [!DNL Decisioning Service] will look up the profile and the information is used to apply the business logic. Des données contextuelles supplémentaires peuvent être transmises à la requête et, si elles sont spécifiées dans les règles commerciales, incluses aux données pour prendre la décision.

Les applications peuvent atteindre de meilleures performances en exécutant une requête de prise de décision pour un maximum de 30 activités à la fois. Les URI des activités sont transmis dans la même requête. L’API REST est synchrone et renvoie les options proposées pour toutes ces activités ou l’option de secours si aucune option de personnalisation ne répond aux contraintes.

Il est possible que deux activités différentes proposent la même option comme leur « meilleure ». To avoid repeating a composed experience, by default, [!DNL Decisioning Service] arbitrates between the activities that are referenced in the same request. L’arbitrage implique que, pour chaque activité, les N premières options sont prises en compte, mais qu’aucune option n’est proposée plus d’une fois dans ces activités. Si la même option est classée en tête pour deux activités, l’une d’elles sera sélectionnée pour utiliser son deuxième ou troisième meilleur choix, et ainsi de suite. Ces règles de déduplication visent à éviter que l’une des activités ne doive utiliser son option de secours.

La requête de décision contient les arguments d’une requête POST dans son corps. Le corps est formaté en tant que `Content-Type` JSON ayant pour valeur d’en-tête `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

La version et le schéma de requête pris en charge à l’heure actuelle sont `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. Par la suite, d’autres versions ou schémas de requête seront fournis.

**Requête**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - Lorsque la valeur de cette propriété facultative est définie sur true, la requête de décision obéit à des contraintes de limitation, mais ne réduit pas réellement ces compteurs. Il est probable que l’appelant n’ait pas l’intention de présenter la proposition au profil. The [!DNL Decisioning Service] will not record the proposition as an official XDM decision event and it will not appear in reporting datasets. La valeur par défaut de cette propriété est false et, quand la propriété est omise, la décision n’est pas considérée comme un test et doit donc être présentée à l’utilisateur final.
- **`xdm:validateContextData`** - Cette propriété facultative active ou désactive la validation des données contextuelles. Si la validation est activée, pour chaque élément de données contextuelles fourni, le schéma (basé sur le champ `@type`) est récupéré du registre XDM et l’objet `xdm:data` est validé sur la base de ce schéma.

La requête liée à ce schéma contient un tableau d’URI référençant des activités d’offre, une identité de profil et un tableau d’éléments de données contextuelles :

- **`xdm:offerActivities`** - Cette propriété obligatoire est un tableau d’objets dans lequel chaque élément contient des données sur l’activité d’offre. L’activité d’offre comporte les propriétés suivantes :
   - **`xdm:offerActivity`** - L’identificateur unique (URI) de l’activité. Il s’agit de la valeur de la propriété `@id` de l’activité d’offre.
- **`xdm:identityMap`** - Une propriété obligatoire contenant un objet JSON conforme au schéma XDM `https://ns.adobe.com/xdm/context/identitymap`. La propriété définit une map dans laquelle la clé est un code d’espace de noms d’identité et la valeur une liste des identifiants d’utilisateur final dans l’espace de noms donné.  
- **`xdm:contextData`** - Une propriété facultative qui contient des éléments décrits par une référence à leur schéma. Chaque élément de données contextuelles du tableau doit comporter les propriétés suivantes :
   - **`@type`** - Une propriété obligatoire référençant le schéma XDM de l’objet dans cet élément.
   - **`xdm:data`** - Une propriété obligatoire contenant les propriétés de l’objet selon le schéma XDM de la propriété `@type`.

## Données contextuelles dynamiques dans les requêtes de décision

La section précédente indique comment les objets XDM peuvent être transmis à une requête de décision. Voici un exemple de ce type de tableau d’objets contextuels :

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

Le schéma doit avoir été créé par votre organisation. Pour en savoir plus sur la création de schémas, consultez le [tutoriel de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md). Votre schéma est associé à un espace de noms `https://ns.adobe.com/{TENANT_ID}/schemas`.

Le [guide de développement de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md) explique comment accéder aux schémas par programmation et comment un développeur peut obtenir l’identifiant du client et l’identifiant numérique de votre schéma. Le numéro de version est obligatoire et est aussi fourni par les API Schema Registry.

Un schéma défini par une organisation a généralement une propriété racine nommée `_{TENANT_ID}`, aussi appelée chaîne d’espace de noms du client.
Notez que les propriétés utilisées à partir d’un composant de schéma global tel que _`https://ns.adobe.com/xdm/context/product` possèdent un préfixe d’espace de noms `xdm:`. Dans l’exemple ci-dessus, la propriété définie par l’organisation `productDetails` a été créée avec ce type de données. Bien que les propriétés du client soient imbriquées dans une propriété nommée en fonction de l’espace de noms du client, les types de données disponibles de manière globale utilisent le préfixe réservé `xdm:` pour empêcher les collisions de noms de propriété.

Plusieurs objets de données peuvent être répertoriés dans la propriété `xdm:contextData`. Chaque objet doit identifier son type via la propriété `@type`.
Les valeurs des objets de données contextuelles peuvent être utilisées dans les expressions PQL, par exemple dans la condition d’une règle d’éligibilité. L’objet de données contextuelles doit être traité par le biais de l’expression de référence à chemin d’accès spécial `@{schemaId}`. Les expressions qui suivent cette expression de référence sont des expressions de chemin d’accès régulières qui accèdent aux propriétés de l’objet de données :

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Dans l’exemple ci-dessus, la variable `p` se réitère sur le tableau des objets marqués par `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

Notez que la syntaxe PQL n’utilise pas de préfixes dans les noms de propriété. Par défaut, les propriétés globales sont simplement référencées sans le préfixe `xdm:`. Les propriétés que votre organisation définit sont imbriquées dans une propriété **supplémentaire** nommée d’après l’espace de noms du client (dans l’exemple indiqué par la variable `{TENANT_ID}`). Pour pouvoir référencer les propriétés personnalisées directement, la variable `p` est liée au résultat du chemin d’accès qui déréférence la propriété d’imbrication supplémentaire.

## Utilisation d’enregistrements de profil

Tous les enregistrements de profil et d’événement d’expérience sont déjà gérés dans la banque de profils. En transmettant une ou plusieurs identités de profil à la requête, le profil de ces identités est identifié et consulté depuis la banque de données. Les données sont alors automatiquement disponibles pour les modèles et règles de décision évalués par la stratégie de décision.

Pour récupérer les enregistrements de profil et d’expérience, la stratégie de fusion par défaut est appliquée.
Note, that after uploading profile records to the [!DNL Platform] datalake there is a slight delay until the profile records can be looked up. Il en va de même pour l’ingestion d’enregistrements de profil et d’expérience via des API par flux. Il faut quelques secondes pour que les données soient disponibles pour l’évaluation des règles de décision évaluant les données de profils et d’événements d’expériences.