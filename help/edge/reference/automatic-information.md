---
title: Informations collectées automatiquement
seo-title: Informations automatiquement collectées par le SDK Web d’Adobe Experience Platform
description: Description de chaque information collectée automatiquement par le SDK d’Adobe Experience Cloud
seo-description: Description de chaque information collectée automatiquement par le SDK d’Adobe Experience Cloud
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 100%

---


# Informations collectées automatiquement

Le SDK d’Adobe Experience Cloud collecte automatiquement plusieurs informations sans configuration particulière. Toutefois, ces informations peuvent être désactivées si nécessaire à l’aide de l’option `context` de la commande `configure`. [Voir Configuration du SDK](../fundamentals/configuring-the-sdk.md). Vous trouverez ci-dessous la liste de ces informations. Le nom entre parenthèses indique la chaîne à utiliser lors de la configuration du contexte.

## Appareil (`device`)

Informations sur l’appareil. Elles ne comprennent pas les données qui peuvent être recherchées côté serveur à partir de la chaîne de l’agent utilisateur.

### Hauteur d’écran

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Hauteur en pixels de l’écran.

### Orientation de l’écran

| **Chemin d’accès dans la charge utile :** | **Valeurs possibles :** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` ou `portrait` |

Orientation de l’écran.

### Largeur d’écran

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Largeur de l’écran (en pixels).

## Environnement (`environment`)

Détails sur l’environnement du navigateur.

### Type d’environnement

Navigateur

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Type d’environnement d’affichage de l’expérience. Le SDK d’Adobe Experience Platform pour JavaScript définit toujours `browser`.

### Hauteur de la fenêtre d’affichage

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Hauteur de la zone de contenu du navigateur (en pixels).

### Largeur de la fenêtre d’affichage

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Largeur de la zone de contenu du navigateur (en pixels).

## Détails d’implémentation

Informations sur le SDK utilisé pour collecter l’événement.

### Nom

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Identifiant du kit de développement logiciel (SDK).  Ce champ utilise un URI pour améliorer l’unicité entre les identifiants fournis par différentes bibliothèques de logiciels.

### Version

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

## Contexte de l’emplacement (`placeContext`)

Informations sur l’emplacement de l’utilisateur final.

### Heure locale

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Horodatage local pour l’utilisateur final au format ISO étendu simplifié [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Décalage du fuseau horaire local

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Nombre de minutes pendant lesquelles l’utilisateur est décalé par rapport au temps universel.

## Horodatage

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Horodatage de l’événement.  Cette partie du contexte ne peut pas être supprimée.

Horodatage UTC pour l’utilisateur final au format ISO étendu simplifié [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Détails Web (`web`)

Informations sur la page sur laquelle se trouve l’utilisateur.

### URL de la page actuelle

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

URL de la page active.

### URL du référent

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

URL de la page précédemment visitée.
