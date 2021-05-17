---
title: Informations collectées automatiquement dans le SDK Web Adobe Experience Platform
description: Présentation de chaque élément d’informations que le kit Adobe Experience Platform SDK collecte automatiquement.
keywords: collecter des informations ; contexte ; configurer ; périphérique ; hauteur de l’écran ; orientation de l’écran ; orientation de l’écran ; largeur d’écran ; largeur d’écran ; environnement ; hauteur de la fenêtre d’affichage ; hauteur de la fenêtre d’affichage ; largeur de la fenêtre d’affichage ; détails de l’écran ; détails de l’implémentation ; détails de l’implémentation ; nom ; version ; contexte local ; heure locale ; local ; local;décalage du fuseau horaire local;horodatage;web;url;webPageDetails;web PageDetails;webReferrer;web Parrain;paysage;portrait;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 0f671a967a67761e0cfef6fa0d022e3c3790c2d8
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 58%

---

# Informations collectées automatiquement

Le Adobe Experience Platform Web SDK collecte automatiquement un certain nombre d’informations sans configuration particulière. Toutefois, ces informations peuvent être désactivées si nécessaire à l’aide de l’option `context` de la commande `configure`. [Voir Configuration du SDK](../fundamentals/configuring-the-sdk.md). Vous trouverez ci-dessous la liste de ces informations. Le nom entre parenthèses indique la chaîne à utiliser lors de la configuration du contexte.

## Appareil (`device`)

Informations sur l’appareil. Elles ne comprennent pas les données qui peuvent être recherchées côté serveur à partir de la chaîne de l’agent utilisateur.

### Hauteur d’écran

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Hauteur de l’écran (en pixels).

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

Type d’environnement par lequel l’expérience est apparue. Le SDK Web de Adobe Experience Platform définit toujours cette valeur sur `browser`.

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

Identifiant du kit de développement logiciel (SDK).  Ce champ utilise un URI pour améliorer l’unicité entre les identifiants fournis par différentes bibliothèques de logiciels. Lorsque la bibliothèque autonome est utilisée, la valeur est `https://ns.adobe.com/experience/alloy`. Lorsque la bibliothèque est utilisée dans le cadre de l’extension de Platform launch, la valeur est `https://ns.adobe.com/experience/alloy+reactor`.

### Version

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Lorsque la bibliothèque autonome est utilisée, la valeur est simplement la version de la bibliothèque. Lorsque la bibliothèque est utilisée dans le cadre de l&#39;extension de Platform launch, il s&#39;agit de la version de la bibliothèque et de la version de l&#39;extension de Platform launch associée à un &quot;+&quot;. Par exemple, si la version de la bibliothèque était 2.1.0 et la version de l’extension de Platform launch 2.1.3, la valeur serait `2.1.0+2.1.3`.

### Environnement

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Environnement de collecte des données. Il est toujours défini sur `browser`.

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
