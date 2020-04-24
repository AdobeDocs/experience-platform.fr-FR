---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur de l''API de registre des '
topic: developer guide
translation-type: tm+mt
source-git-commit: 387cbdebccb9ae54a2907d1afe220e9711927ca6

---


# Guide du développeur de l&#39;API de registre des 

Le Registre des  permet d’accéder à la bibliothèque de  dans Adobe Experience Platform, fournissant une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources de bibliothèque disponibles sont accessibles.

Grâce à l’API de registre des , vous pouvez effectuer des opérations CRUD de base afin de et de gérer toutes les  et ressources connexes disponibles dans Adobe Experience Platform. Cela inclut celles définies par Adobe, les partenaires Experience Platform et les fournisseurs dont vous utilisez les applications. Vous pouvez également utiliser les appels d’API pour créer de nouveaux  et ressources pour votre organisation, ainsi que pour et modification des ressources que vous avez déjà définies.

Ce guide du développeur décrit les étapes à suivre pour vous aider à  à l’aide de l’API de registre . Le guide fournit ensuite des exemples d’appels d’API pour effectuer des opérations clés à l’aide du Registre des  d’.

## Conditions préalables

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../schema/composition.md)de  : Découvrez les blocs de création de base des  XDM.
* [](../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels vers l&#39;API de Registre du .

## Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

## Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au Registre des  d’, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes de recherche (GET) envoyées au Registre des  du nécessitent un en-tête Accept supplémentaire, dont la valeur détermine le format des informations renvoyées par l’API. Voir la section d’en-tête [](#accept) Accepter ci-dessous pour plus d’informations.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

* Content-Type : application/json

## Connaissez votre ID_TENANT {#know-your-tenant_id}

Dans ce guide, vous verrez des références à un `TENANT_ID`. Cet identifiant permet de s’assurer que les ressources que vous créez sont correctement nommées et contenues dans votre organisation IMS. Si vous ne connaissez pas votre ID, vous pouvez y accéder en exécutant la requête GET suivante :

**Format API**

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

Une réponse positive renvoie des informations concernant l&#39;utilisation du Registre des  par votre organisation. Ceci inclut un `tenantId` attribut, dont la valeur est votre `TENANT_ID`attribut.

```JSON
{
  "imsOrg":"{IMS_ORG}",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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

* `tenantId`: La `TENANT_ID` valeur de votre organisation IMS.

## Comprendre les `CONTAINER_ID`{#container}

Les appels à l’API de registre  nécessitent l’utilisation d’une `CONTAINER_ID`. Il existe deux  par rapport auxquels les appels d’API peuvent être effectués : le  **global** et le **locataire**.

###  globale

Le global contient toutes les classes, mixins, types de données et  de Adobe et Experience Platform standard. Vous ne pouvez exécuter que des demandes de  et de recherche (GET) par rapport à la  globale.

### locataire

A ne pas confondre avec votre unique `TENANT_ID`, le locataire contient toutes les classes, les mixins, les types de données, les et les descripteurs définis par une organisation IMS. Elles sont propres à chaque organisation, ce qui signifie qu&#39;elles ne sont ni visibles ni gérables par d&#39;autres organismes du SGI. Vous pouvez effectuer toutes les opérations CRUD (GET, POST, PUT, PATCH, DELETE) par rapport aux ressources que vous créez dans le  du client.

Lorsque vous créez une classe, un mixin, un  ou un type de données dans le du client, il est enregistré dans le registre de l&#39; de l&#39;entreprise et un `$id` URI contenant votre `TENANT_ID`URI est affecté. Elle `$id` est utilisée dans toute l’API pour référencer des ressources spécifiques. Des exemples de `$id` valeurs sont fournis dans la section suivante.

## identification {#schema-identification}

Les  sont identifiés avec un `$id` attribut sous la forme d’un URI, tel que :
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Pour rendre l’URI plus conviviale,  les disposent également d’un encodage en notation point de l’URI dans une propriété appelée `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Les appels à l’API de registre  prennent en charge soit l’ `$id` URI codé en URL, soit le `meta:altId` (format de notation par point). Il est recommandé d’utiliser l’ `$id` URI codé en URL lors d’un appel REST à l’API, comme suit :
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## En-tête Accepter {#accept}

Lorsque vous effectuez des opérations de recherche et de  (GET) dans l&#39;API de Registre de , un en-tête Accepter est nécessaire pour déterminer le format des données renvoyées par l&#39;API. Lors de la recherche de ressources spécifiques, un numéro de version doit également être inclus dans l’en-tête Accepter.

Le tableau suivant  des valeurs d’en-tête Accepter compatibles, y compris celles avec des numéros de version, ainsi que des descriptions de ce que l’API renverra lorsqu’elles seront utilisées.

| Accepter | Description |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Renvoie un  d’ID uniquement. Il est le plus souvent utilisé pour répertorier des ressources. |
| `application/vnd.adobe.xed+json` | Renvoie un de JSON complet  avec l’original `$ref` et `allOf` inclus. Il est utilisé pour renvoyer un de ressources complètes. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw XDM avec `$ref` et `allOf`. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus. Contient des titres et des descriptions. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw XDM avec `$ref` et `allOf`. Aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus. Aucun titre ni aucune description. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` et `allOf` résolus. Les descripteurs sont inclus. |

>[!NOTE] Si vous fournissez la `major` version seulement (p. ex. 1, 2, 3), le registre renverra la dernière `minor` version (p. ex. .1, .2, .3) automatiquement.

## Contraintes de champ XDM et bonnes pratiques

Les champs d’un  sont répertoriés dans son `properties` objet. Chaque champ est lui-même un objet, contenant des attributs pour décrire et contraindre les données que le champ peut contenir.

Vous trouverez plus d’informations sur la définition des types de champs dans l’API dans l’ [annexe](appendix.md) de ce guide, y compris des exemples de code et des contraintes facultatives pour les types de données les plus couramment utilisés.

L’exemple de champ suivant illustre un champ XDM correctement formaté, avec des détails supplémentaires sur les contraintes d’affectation de nom et les bonnes pratiques fournies ci-dessous. Ces pratiques peuvent également être appliquées lors de la définition d’autres ressources qui contiennent des attributs similaires.

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

* Le nom d’un objet de champ peut contenir des caractères alphanumériques, des tirets ou des traits de soulignement, mais il **peut ne pas**  avec un trait de soulignement.
   * **Correct :** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Incorrect :** `_fieldName`
* camelCase est préférable pour le nom de l’objet field. Exemple: `fieldName`
* Le champ doit inclure un `title`, écrit dans la casse du titre. Exemple: `Field Name`
* Le champ nécessite un `type`champ.
   * La définition de certains types peut nécessiter une option `format`.
   * Lorsqu’une mise en forme spécifique des données est requise, `examples` vous pouvez l’ajouter sous forme de tableau.
   * Le type de champ peut également être défini à l’aide de n’importe quel type de données dans le registre. Pour plus d&#39;informations, consultez la section sur la [création d&#39;un type](create-data-type.md) de données dans ce guide.
* Le `description` document explique le champ et les informations pertinentes concernant les données sur le terrain. Il doit être rédigé en phrases complètes avec un langage clair afin que quiconque accède au  puisse comprendre l&#39;intention du champ.

Voir l’ [annexe](appendix.md) pour plus d’informations sur la définition des types de champ dans l’API.

## Étapes suivantes

Ce  couvert les connaissances préalables requises pour effectuer des appels à l&#39;API de registre de , y compris les informations d&#39;identification d&#39;authentification requises. Vous pouvez maintenant accéder aux exemples d’appels fournis dans ce guide du développeur et suivre leurs instructions. Pour une présentation détaillée de la manière de créer un dans l’API, reportez-vous au [didacticiel](../tutorials/create-schema-api.md)suivant.
