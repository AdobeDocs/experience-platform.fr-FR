---
title: Informations collectées automatiquement dans le SDK Web de Adobe Experience Platform
description: Une vue d’ensemble de chaque information collectée automatiquement par le SDK Adobe Experience Platform.
keywords: collecter des informations;contexte;configurer;appareil;hauteur d’écran;orientation de l’écran;orientation de l’écran;largeur d’écran;largeur d’écran;environnement;hauteur de fenêtre d’affichage;hauteur de fenêtre d’affichage;largeur de fenêtre d’affichage;détails du navigateur;détails de la mise en oeuvre;détails de la mise en oeuvre;nom;version;contexte local;heure locale;fuseau horaire local Décalage du fuseau horaire;horodatage;web;url;webPageDetails;détails de la page web;webReferrer;référent web;paysage;portrait;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: e3f507e010ea2a32042b53d46795d87e82e3fb72
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 60%

---

# Informations collectées automatiquement

Le SDK Web de Adobe Experience Platform collecte automatiquement un certain nombre d’informations sans configuration particulière. Toutefois, ces informations peuvent être désactivées si nécessaire à l’aide de l’option `context` de la commande `configure`. [Voir Configuration du SDK](../fundamentals/configuring-the-sdk.md). Vous trouverez ci-dessous la liste de ces informations. Le nom entre parenthèses indique la chaîne à utiliser lors de la configuration du contexte.

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

Identifiant du kit de développement logiciel (SDK).  Ce champ utilise un URI pour améliorer l’unicité entre les identifiants fournis par différentes bibliothèques de logiciels. Lorsque la bibliothèque autonome est utilisée, la valeur est `https://ns.adobe.com/experience/alloy`. Lorsque la bibliothèque est utilisée dans le cadre de l’extension de balise, la valeur est `https://ns.adobe.com/experience/alloy+reactor`.

### Version

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Lorsque la bibliothèque autonome est utilisée, la valeur est simplement la version de la bibliothèque. Lorsque la bibliothèque est utilisée dans le cadre de l’extension de balise, il s’agit de la version de la bibliothèque et de la version de l’extension de balise associée à un &quot;+&quot;. Par exemple, si la version de la bibliothèque est 2.1.0 et que la version de l’extension de balise est 2.1.3, la valeur est `2.1.0+2.1.3`.

### Environnement {#environment}

| **Chemin d’accès dans la charge utile :** | **Exemple :** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Environnement dans lequel les données ont été collectées. Cette valeur est toujours définie sur `browser`.

## Contexte de l’emplacement (`placeContext`) {#place-context}

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
