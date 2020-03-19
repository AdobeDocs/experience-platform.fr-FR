---
title: Informations collectées automatiquement
seo-title: Informations automatiquement collectées par le SDK Web d’Adobe Experience Platform
description: Description de chaque information collectée automatiquement par le SDK Adobe Experience Cloud
seo-description: Description de chaque information collectée automatiquement par le SDK Adobe Experience Cloud
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Informations collectées automatiquement

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Le SDK Adobe Experience Cloud collecte automatiquement plusieurs éléments d’informations sans configuration particulière. Toutefois, ces informations peuvent être désactivées si nécessaire à l’aide de l’ `context` option de la `configure` commande. [Voir Configuration du SDK](../fundamentals/configuring-the-sdk.md). Voici un  de ces informations. Le nom entre parenthèses indique la chaîne à utiliser lors de la configuration du contexte.

## Périphérique (`device`)

Informations sur le périphérique. Cela n’inclut pas les données qui peuvent être recherchées côté serveur à partir de la chaîne de l’agent utilisateur.

### Hauteur de l’écran

| **Chemin dans Payload :** | **Exemple :** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Hauteur en pixels de l’écran.

### Orientation de l’écran

| **Chemin dans Payload :** | **Valeurs possibles :** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` ou `portrait` |

Orientation de l’écran.

### Largeur de l’écran

| **Chemin dans Payload :** | **Exemple :** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Largeur de l’écran (en pixels).

## Environnement (`environment`)

Détails sur le navigateur  .

###  type de 

Browser (Navigateur)

| **Chemin dans Payload :** | **Exemple :** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Type de   par laquelle l’expérience a été affichée. Le SDK Adobe Experience Platform pour JavaScript est toujours défini `browser`.

### Hauteur de la fenêtre d’affichage

| **Chemin dans Payload :** | **Exemple :** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Hauteur de la zone de contenu du navigateur (en pixels).

### Largeur de la fenêtre d’affichage

| **Chemin dans Payload :** | **Exemple :** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Largeur de la zone de contenu du navigateur (en pixels).

## Détails de l’implémentation

Informations sur le SDK utilisé pour collecter le  de.

### Nom

| **Chemin dans Payload :** | **Exemple :** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Identifiant du kit de développement logiciel (SDK).  Ce champ utilise un URI pour améliorer l’unicité entre les identifiants fournis par différentes bibliothèques de logiciels.

### Version

| **Chemin dans Payload :** | **Exemple :** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

## Contexte de l’emplacement (`placeContext`)

Informations sur l’emplacement de l’utilisateur final.

### Heure locale

| **Chemin dans Payload :** | **Exemple :** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Horodatage local pour l’utilisateur final au format ISO étendu simplifié [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Décalage du fuseau horaire local

| **Chemin dans Payload :** | **Exemple :** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Nombre de minutes pendant lesquelles l’utilisateur est décalé par rapport à GMT.

## Horodatage

| **Chemin dans Payload :** | **Exemple :** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Horodatage de l’événement.  Cette partie du contexte ne peut pas être supprimée.

Horodatage UTC pour l&#39;utilisateur final au format ISO étendu simplifié [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Détails Web (`web`)

Informations détaillées sur la page sur laquelle se trouve l’utilisateur.

### URL de la page active

| **Chemin dans Payload :** | **Exemple :** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

URL de la page active.

### URL 

| **Chemin dans Payload :** | **Exemple :** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

URL de la page précédente visitée.
