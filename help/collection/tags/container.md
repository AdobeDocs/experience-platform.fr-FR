---
title: _conteneur
description: Voir l’intégralité du conteneur de balises dans un seul objet .
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

L’objet `_satellite._container` contient la configuration complète et le contexte d’exécution de la propriété de balise chargée sur la page. Toutes les informations, telles que les règles, les éléments de données, les extensions et les environnements, sont disponibles dans cet objet. Son utilisation principale consiste à vous aider à déboguer votre implémentation afin que vous puissiez voir exactement quelle logique est exposée ou publiée.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>Cet objet est uniquement à des fins de débogage. Ne liez pas la logique de production à cet objet, ne référencez pas cet objet dans votre implémentation et ne modifiez pas les valeurs au sein de cet objet. La disponibilité des propriétés ou des noms dans cet objet peut être modifiée par Adobe à tout moment.

## Champs disponibles

Les objets suivants sont disponibles à titre de référence :

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

L’objet `_satellite._container.buildInfo` contient une copie de [`_satellite.buildInfo`](buildinfo.md).

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

L’objet `_satellite._container.company` contient une copie de [`_satellite.company`](company.md).

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

L’objet `_satellite._container.dataElements` fournit une référence de tous les éléments de données dans votre propriété de balise.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

Chaque élément de données comprend les propriétés suivantes :

| Nom | Type | Description |
|---|---|---|
| **`modulePath`** | `string` | Chemin d’accès au fichier JavaScript qui détermine la logique de ce type d’élément de données. |
| **`settings`** | `Settings` | Paramètres de l’élément de données. Les propriétés de cet objet dépendent du type d’élément de données. |

## `environment`

L’objet `_satellite._container.environment` contient une copie de [`_satellite.environment`](environment.md).

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

L’objet `_satellite._container.extensions` répertorie toutes les extensions publiées sur la propriété de balise.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

Chaque extension comprend les propriétés suivantes :

| Nom | Type | Description |
|---|---|---|
| **`displayName`** | `string` | Nom convivial de l’extension. |
| **`hostedLibFilesUrl`** | `string` | L’emplacement sur le réseau CDN où réside l’extension. |
| **`modules`** | `Modules` | La logique JavaScript de tous les événements, actions, conditions et éléments de données utilisés par l’extension. Le contenu de cet objet est différent pour chaque extension. |

## `property`

L’objet `_satellite._container.property` fournit des informations sur la propriété de balise elle-même.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| Nom | Type | Description |
|---|---|---|
| **`id`** | `string` | Identifiant unique de la propriété de balise. |
| **`name`** | `string` | Nom convivial de la propriété de balise. |
| **`settings`** | `PropertySettings` | Paramètres de cette propriété. Voir le tableau ci-dessous. |

| Nom du paramètre | Type | Description |
|---|---|---|
| **`domains`** | `string[]` | Domaines configurés pour la propriété , tels que définis lors de la [configuration d’une propriété de balise](/help/tags/ui/administration/companies-and-properties.md). |
| **`ruleComponentSequencingEnabled`** | `boolean` | Détermine si la case à cocher **[!UICONTROL Run rule components in sequence]** est activée lors de la configuration de la propriété de balise. |
| **`undefinedVarsReturnEmpty`** | `boolean` | Détermine si la case à cocher **[!UICONTROL Return an empty string for undefined data elements]** est activée lors de la configuration de la propriété de balise. |

## `_container.rules`

Le tableau d’objets `rules` fournit une référence de toutes les règles de votre propriété de balise.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

Chaque règle contient les champs suivants :

| Nom | Type | Description |
|---|---|---|
| **`id`** | `string` | Identifiant unique de la règle. |
| **`name`** | `string` | Nom convivial de la règle. |
| **`events`** | `Event[]` | Tableau d’événements que vous avez configurés pour déclencher la règle. |
| **`conditions`** | `Condition[]` | Tableau de conditions que vous avez configurées pour déclencher la règle. |
| **`actions`** | `Action[]` | Tableau d’actions que vous avez configuré pour exécuter lorsque la règle est déclenchée. |
