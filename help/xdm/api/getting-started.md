---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;registre des schémas;modèle de données
solution: Experience Platform
title: Prise en main de l’API Schema Registry
description: Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels vers l’API Schema Registry.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: eb1cf204e95591082b27dc97cd3c709a23b20b08
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 42%

---

# Prise en main de l’API [!DNL Schema Registry]

L’API [!DNL Schema Registry] vous permet de créer et de gérer diverses ressources du modèle de données d’expérience (XDM). Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API [!DNL Schema Registry].

## Conditions préalables

L’utilisation du guide de développement nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](../home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Notions de base de la composition du schéma](../schema/composition.md) : en savoir plus sur les blocs de création de base des schémas XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

XDM utilise le formatage du schéma JSON pour décrire et valider la structure des données d’expérience client ingérées. Il est donc vivement recommandé de consulter la [documentation officielle du schéma JSON](https://json-schema.org/) pour mieux comprendre cette technologie sous-jacente.

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Schema Registry] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Schema Registry], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation sur les environnements de test](../../sandboxes/home.md).

Toutes les requêtes de recherche (GET) envoyées à [!DNL Schema Registry] nécessitent un en-tête `Accept` supplémentaire, dont la valeur détermine le format des informations renvoyées par l’API. Voir la section [En-tête Accept](#accept) ci-dessous pour plus d’informations.

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Connaître votre TENANT_ID {#know-your-tenant_id}

Dans les guides d’API, vous trouverez des références à un `TENANT_ID`. Cet identifiant permet de s’assurer que les espaces de noms des ressources que vous créez sont corrects et contenus dans votre organisation. Si vous ne connaissez pas votre identifiant, vous pouvez y accéder en réalisant la requête GET suivante :

**Format d’API**

```http
GET /stats
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie des informations concernant l’utilisation de [!DNL Schema Registry] par votre organisation. Cela inclut un attribut `tenantId`, dont la valeur est votre `TENANT_ID`.

```JSON
{
  "imsOrg":"{ORG_ID}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## Comprendre le `CONTAINER_ID` {#container}

Les appels à l’API [!DNL Schema Registry] nécessitent l’utilisation d’un `CONTAINER_ID`. Il existe deux conteneurs sur lesquels vous pouvez effectuer des appels API : le conteneur `global` et le conteneur `tenant`.

### Conteneur mondial

Le conteneur `global` contient toutes les classes d’Adobe standard et [!DNL Experience Platform] fournies par les partenaires, les groupes de champs de schéma, les types de données et les schémas. Vous pouvez uniquement effectuer des requêtes de liste et de recherche (GET) sur le conteneur `global`.

Voici un exemple d’appel qui utilise le conteneur `global` :

```http
GET /global/classes
```

### Conteneur client

À ne pas confondre avec votre `TENANT_ID` unique, le conteneur `tenant` contient toutes les classes, tous les groupes de champs, tous les types de données, tous les schémas et tous les descripteurs définis par une organisation. Elles sont propres à chaque organisation, ce qui signifie qu’elles ne sont pas visibles ou gérables par d’autres organisations. Vous pouvez effectuer toutes les opérations CRUD (GET, POST, PUT, PATCH, DELETE) sur les ressources que vous créez dans le conteneur `tenant`.

Voici un exemple d’appel qui utilise le conteneur `tenant` :

```http
POST /tenant/fieldgroups
```

Lorsque vous créez une classe, un groupe de champs, un schéma ou un type de données dans le conteneur `tenant`, il est enregistré dans le conteneur [!DNL Schema Registry] et se voit attribuer un URI `$id` qui inclut votre `TENANT_ID`. Cet `$id` est utilisé sur l’ensemble de l’API pour faire référence à des ressources spécifiques. Des exemples de valeurs `$id` sont fournis à la section suivante.

## Identification des ressources {#resource-identification}

Les ressources XDM sont identifiées avec un attribut `$id` sous la forme d’un URI, comme les exemples suivants :

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Pour rendre l’URI plus REST-friendly, les schémas possèdent également un encodage de notation à point de l’URI dans une propriété intitulée `meta:altId` :

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Les appels à l’API [!DNL Schema Registry] prennent en charge l’URI `$id` encodé par l’URL ou le `meta:altId` (format de notation par points). La bonne pratique est d’utiliser l’URI `$id` encodé par l’URL lorsque vous passez un appel REST à l’API, comme :

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## En-tête Accept {#accept}

Lors des opérations de liste et de recherche (GET) dans l’API [!DNL Schema Registry], un en-tête `Accept` est nécessaire pour déterminer le format des données renvoyées par l’API. Lors de la recherche de ressources spécifiques, un numéro de version doit également être inclus dans l’en-tête `Accept`.

Le tableau suivant répertorie les valeurs d’en-tête `Accept` compatibles, y compris celles avec des numéros de version, ainsi que des descriptions de ce que l’API renverra lorsqu’elles sont utilisées.

| Accept | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Renvoie uniquement une liste d’identifiants. Il s’agit de l’en-tête le plus souvent utilisé pour répertorier des ressources. |
| `application/vnd.adobe.xed+json` | Renvoie une liste de schémas JSON complets qui incluent le `$ref` et le `allOf` d’origine. Cet en-tête est utilisé pour renvoyer une liste de ressources complètes. |
| `application/vnd.adobe.xed+json; version=1` | XDM brut avec `$ref` et `allOf`. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version=1` | Attributs `$ref` et `allOf` résolus. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM brut avec `$ref` et `allOf`. Aucun titre ni description. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | Attributs `$ref` et `allOf` résolus. Aucun titre ni description. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | Attributs `$ref` et `allOf` résolus. Les descripteurs sont inclus. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` et `allOf` résolus, contient des titres et des descriptions. Les champs obsolètes sont indiqués avec un attribut `meta:status` de `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Platform ne prend actuellement en charge qu’une seule version majeure pour chaque schéma (`1`). Par conséquent, la valeur de `version` doit toujours être `1` lors de l’exécution de requêtes de recherche afin de renvoyer la dernière version mineure du schéma. Pour plus d’informations sur le contrôle de version des schémas, reportez-vous à la sous-section ci-dessous.

### Contrôle de version des schémas {#versioning}

Les versions des schémas sont référencées par les en-têtes `Accept` de l’API Schema Registry et dans les propriétés `schemaRef.contentType` des payloads de l’API du service Platform en aval.

Actuellement, Platform ne prend en charge qu’une seule version majeure (`1`) pour chaque schéma. Selon les [ règles d’évolution du schéma ](../schema/composition.md#evolution), chaque mise à jour d’un schéma doit être non destructive, ce qui signifie que de nouvelles versions mineures d’un schéma (`1.2`, `1.3`, etc.) sont toujours rétrocompatibles avec les versions mineures précédentes. Par conséquent, lors de la spécification de `version=1`, le registre des schémas renvoie toujours la **dernière** version majeure `1` d’un schéma, ce qui signifie que les versions mineures précédentes ne sont pas renvoyées.

>[!NOTE]
>
>L’exigence non destructive pour l’évolution du schéma n’est appliquée qu’après que le schéma a été référencé par un jeu de données et que l’un des cas suivants est vrai :
>
>* Les données ont été ingérées dans le jeu de données.
>* Le jeu de données a été activé pour une utilisation dans Real-Time Customer Profile (même si aucune donnée n’a été ingérée).
>
>Si le schéma n’a pas été associé à un jeu de données qui répond à l’un des critères ci-dessus, toute modification peut lui être apportée. Cependant, dans tous les cas, le composant `version` reste à `1`.

## Contraintes de champ XDM et bonnes pratiques

Les champs d’un schéma sont répertoriés dans son objet `properties`. Chaque champ est lui-même un objet, contenant des attributs pour décrire et contraindre les données que le champ peut contenir. Reportez-vous au guide sur la [définition de champs personnalisés dans l’API](../tutorials/custom-fields-api.md) pour obtenir des exemples de code et des contraintes facultatives pour les types de données les plus couramment utilisés.

Le champ d’exemple suivant illustre un champ XDM formaté correctement avec de plus amples détails sur les contraintes de dénomination et les bonnes pratiques fournies ci-dessous. Ces pratiques peuvent également s’appliquer lorsque vous définissez les autres ressources pouvant contenir des attributs similaires.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* Le nom d’un objet de champ peut contenir des caractères alphanumériques, des tirets ou des traits de soulignement, mais **ne peut pas** commencer par un trait de soulignement.
   * **Correct :** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorrect :** `_fieldName`
* Les noms de champ ne sont pas sensibles à la casse et doivent porter des noms différents au même niveau dans votre schéma.
* Le Camel case est préférable pour le nom du champ objet. Exemple : `fieldName`
* Le champ doit inclure un `title`, écrit en Casse Titre. Exemple : `Field Name`
* Le champ nécessite un `type`.
   * La définition de certains types peut nécessiter un `format` facultatif.
   * Lorsqu’une mise en forme spécifique des données est requise, vous pouvez ajouter des `examples` sous la forme d’un tableau.
   * Il est également possible de définir le type de champ à l’aide d’un type de données dans le registre. Pour plus d’informations, consultez la section sur la [création d’un type de données](./data-types.md#create) dans le guide de point de terminaison des types de données .
* Le `description` explique le champ et des informations pertinentes concernant les données du champ. Il doit être écrit en phrases complètes dans une langue claire afin que toute personne accédant au schéma puisse comprendre l’intention du champ.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Schema Registry], sélectionnez l’un des guides de point d’entrée disponibles.
