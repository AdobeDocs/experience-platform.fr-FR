---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; registre des schémas ; registre des Schémas ;
solution: Experience Platform
title: Prise en main de l’API Schéma Registry
description: Ce document présente les concepts de base que vous devez connaître avant de tenter d'appeler l'API de registre du Schéma.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 39%

---

# Prise en main de l’API [!DNL Schema Registry]

L’API [!DNL Schema Registry] vous permet de créer et de gérer diverses ressources de modèle de données d’expérience (XDM). Ce document présente les concepts de base que vous devez connaître avant de tenter d&#39;appeler l&#39;API [!DNL Schema Registry].

## Conditions préalables  

L’utilisation du guide du développeur nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](../home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Notions de base de la composition du schéma](../schema/composition.md) : en savoir plus sur les blocs de création de base des schémas XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

XDM utilise le formatage de Schéma JSON pour décrire et valider la structure des données d’expérience client assimilées. Il est donc fortement recommandé de consulter la [documentation officielle du Schéma JSON](https://json-schema.org/) pour mieux comprendre cette technologie sous-jacente.

## Lecture d’exemples d’appels API

La documentation de l&#39;API [!DNL Schema Registry] fournit des exemples d&#39;appels d&#39;API pour montrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Schema Registry], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation de sandbox](../../sandboxes/home.md).

Toutes les requêtes de recherche (GET) envoyées à [!DNL Schema Registry] nécessitent un en-tête `Accept` supplémentaire, dont la valeur détermine le format des informations renvoyées par l&#39;API. Voir la section [En-tête Accept](#accept) ci-dessous pour plus d’informations.

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Connaître votre TENANT_ID {#know-your-tenant_id}

Dans les guides d&#39;API, vous verrez des références à `TENANT_ID`. Cet identifiant est utilisé pour assurer que les espaces de noms des ressources que vous créez sont corrects et contenus dans votre organisation IMS. Si vous ne connaissez pas votre identifiant, vous pouvez y accéder en réalisant la requête GET suivante :

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse positive renvoie des informations concernant l&#39;utilisation de [!DNL Schema Registry] par votre organisation. Cela inclut un attribut `tenantId`, dont la valeur est votre `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "fieldgroups": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "fieldgroups",
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
      "meta:resourceType": "fieldgroups",
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

Les appels à l&#39;API [!DNL Schema Registry] nécessitent l&#39;utilisation d&#39;un `CONTAINER_ID`. Il existe deux conteneurs pour lesquels des appels d&#39;API peuvent être effectués : le conteneur `global` et le conteneur `tenant`.

### Conteneur mondial

Le conteneur `global` contient tous les Adobes standard et [!DNL Experience Platform] partenaires ont fourni des classes, des groupes de champs de schéma, des types de données et des schémas. Vous ne pouvez exécuter que des requêtes de liste et de recherche (GET) sur le conteneur `global`.

Voici un exemple d&#39;appel qui utilise le conteneur `global` :

```http
GET /global/classes
```

### Conteneur client

À ne pas confondre avec votre `TENANT_ID` unique, le conteneur `tenant` contient toutes les classes, les groupes de champs, les types de données, les schémas et les descripteurs définis par une organisation IMS. Ils sont spécifiques à chaque organisation, ce qui signifie qu’ils ne sont pas visibles ou gérables par d’autres organisations IMS. Vous pouvez exécuter toutes les opérations CRUD (GET, POST, PUT, PATCH, DELETE) par rapport aux ressources que vous créez dans le conteneur `tenant`.

Voici un exemple d&#39;appel qui utilise le conteneur `tenant` :

```http
POST /tenant/fieldgroups
```

Lorsque vous créez une classe, un groupe de champs, un schéma ou un type de données dans le conteneur `tenant`, il est enregistré dans [!DNL Schema Registry] et un URI `$id` doté de votre `TENANT_ID` est affecté. Cet `$id` est utilisé sur l’ensemble de l’API pour faire référence à des ressources spécifiques. Des exemples de valeurs `$id` sont fournis à la section suivante.

## Identification des ressources {#resource-identification}

Les ressources XDM sont identifiées avec un attribut `$id` sous la forme d&#39;un URI, comme dans les exemples suivants :

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Pour rendre l’URI plus REST-friendly, les schémas possèdent également un encodage de notation à point de l’URI dans une propriété intitulée `meta:altId` :

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Les appels à l&#39;API [!DNL Schema Registry] prennent en charge soit l&#39;URI `$id` codé en URL, soit le `meta:altId` (format de notation par point). La bonne pratique est d’utiliser l’URI `$id` encodé par l’URL lorsque vous passez un appel REST à l’API, comme :

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## En-tête Accept {#accept}

Lorsque vous effectuez des opérations de liste et de recherche (GET) dans l&#39;API [!DNL Schema Registry], un en-tête `Accept` est nécessaire pour déterminer le format des données renvoyées par l&#39;API. Lors de la recherche de ressources spécifiques, un numéro de version doit également être inclus dans l&#39;en-tête `Accept`.

Le tableau suivant liste des valeurs d&#39;en-tête `Accept` compatibles, y compris celles avec des numéros de version, ainsi que des descriptions de ce que l&#39;API retournera lorsqu&#39;elles seront utilisées.

| Accept | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Renvoie uniquement une liste d’identifiants. Il s’agit de l’en-tête le plus souvent utilisé pour répertorier des ressources. |
| `application/vnd.adobe.xed+json` | Renvoie une liste de schémas JSON complets qui incluent le `$ref` et le `allOf` d’origine. Cet en-tête est utilisé pour renvoyer une liste de ressources complètes. |
| `application/vnd.adobe.xed+json; version=1` | XDM brut avec `$ref` et `allOf`. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version=1` | Attributs `$ref` et `allOf` résolus. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version=1` | XDM brut avec `$ref` et `allOf`. Aucun titre ni description. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | Attributs `$ref` et `allOf` résolus. Aucun titre ni description. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | Attributs `$ref` et `allOf` résolus. Les descripteurs sont inclus. |

>[!NOTE]
>
>La plate-forme ne prend actuellement en charge qu&#39;une seule version majeure pour chaque schéma (`1`). Par conséquent, la valeur de `version` doit toujours être `1` lorsque vous exécutez des requêtes de recherche pour renvoyer la dernière version mineure du schéma. Consultez la sous-section ci-dessous pour plus d&#39;informations sur le contrôle de version des schémas.

### Version du schéma {#versioning}

Les versions de schéma sont référencées par des en-têtes `Accept` dans l&#39;API de registre de Schéma et dans les propriétés `schemaRef.contentType` dans les charges d&#39;API de service de plateforme en aval.

Actuellement, Platform ne prend en charge qu&#39;une seule version majeure (`1`) pour chaque schéma. Selon les [règles d&#39;évolution du schéma](../schema/composition.md#evolution), chaque mise à jour d&#39;un schéma doit être non destructive, ce qui signifie que de nouvelles versions mineures d&#39;un schéma (`1.2`, `1.3`, etc.) sont toujours rétrocompatibles avec les versions mineures précédentes. Par conséquent, lors de la spécification de `version=1`, le Registre de Schéma renvoie toujours la **dernière** version principale `1` d&#39;un schéma, ce qui signifie que les versions mineures précédentes ne sont pas renvoyées.

>[!NOTE]
>
>L&#39;exigence non destructive pour l&#39;évolution des schémas n&#39;est appliquée qu&#39;après que le schéma a été référencé par un jeu de données et l&#39;un des cas suivants est vrai :
>
>* Les données ont été ingérées dans le jeu de données.
>* Le jeu de données a été activé pour une utilisation dans le Profil client en temps réel (même si aucune donnée n’a été ingérée).

>
>
Si le schéma n&#39;a pas été associé à un jeu de données qui répond à l&#39;un des critères ci-dessus, tout changement peut être apporté à celui-ci. Cependant, dans tous les cas, le composant `version` reste à `1`.

## Contraintes de champ XDM et bonnes pratiques

Les champs d’un schéma sont répertoriés dans son objet `properties`. Chaque champ est lui-même un objet et contient des attributs pour décrire et contraindre les données que le champ peut contenir.

Pour plus d&#39;informations sur la définition des types de champ dans l&#39;API, consultez le [guide des contraintes de champ](../schema/field-constraints.md) pour ce guide, y compris des exemples de code et des contraintes facultatives pour les types de données les plus couramment utilisés.

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
* Le Camel case est préférable pour le nom du champ objet. Exemple : `fieldName`
* Le champ doit inclure un `title`, écrit en Casse Titre. Exemple : `Field Name`
* Le champ nécessite un `type`.
   * La définition de certains types peut nécessiter un `format` facultatif.
   * Lorsqu’une mise en forme spécifique des données est requise, vous pouvez ajouter des `examples` sous la forme d’un tableau.
   * Il est également possible de définir le type de champ à l’aide d’un type de données dans le registre. Pour plus d&#39;informations, consultez la section [création d&#39;un type de données](./data-types.md#create) dans le guide des points de terminaison des types de données.
* Le `description` explique le champ et des informations pertinentes concernant les données du champ. Il doit être écrit en phrases complètes dans une langue claire afin que toute personne accédant au schéma puisse comprendre l’intention du champ.

Voir le document sur [les contraintes de champ](../schema/field-constraints.md) pour plus d&#39;informations sur la manière de définir différents types de champ dans l&#39;API.

## Étapes suivantes

Pour commencer à effectuer des appels à l&#39;aide de l&#39;API [!DNL Schema Registry], sélectionnez l&#39;un des guides de points de terminaison disponibles.
