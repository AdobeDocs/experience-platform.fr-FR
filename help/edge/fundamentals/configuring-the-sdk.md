---
title: Configuration du SDK Web Adobe Experience Platform
description: Découvrez comment configurer le SDK Web de Adobe Experience Platform.
seo-description: Découvrez la procédure de configuration du SDK Web d’Experience Platform
keywords: configure;configuration;SDK;edge;Web SDK;configure;edgeConfigId;context;web;device;environnement;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk settings;prehideStyle;opacity;cookieDestinationsEnabled;urlDestinations Activé ; idMigrationEnabled ; thirdPartyCookiesEnabled ;
translation-type: tm+mt
source-git-commit: 85bb984231a3069aad0c63707f5024612181798c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 70%

---


# Configuration de Platform Web SDK

La configuration du SDK est effectuée à l’aide de la commande `configure`.

>[!IMPORTANT]
>
>`configure` doit *toujours* être la première commande appelée.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

De nombreuses options peuvent être définies lors de la configuration. Vous trouverez ci-dessous toutes les options regroupées par catégorie.

## Options générales

### `edgeConfigId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

L’ID de configuration que vous avez attribué, qui lie le SDK aux comptes et à la configuration appropriés.  Lors de la configuration de plusieurs instances dans une seule page, vous devez configurer un `edgeConfigId` différent pour chaque instance.

### `context`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| ---------------- | ------------ | -------------------------------------------------- |
| Tableau de chaînes | Non | `["web", "device", "environment", "placeContext"]` |

Indique les catégories contextuelles à collecter automatiquement, comme décrit dans la section [Informations automatiques](../data-collection/automatic-information.md).  Si cette configuration n’est pas spécifiée, toutes les catégories sont utilisées par défaut.

### `debugEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `false` |

Indique si le débogage doit être activé. La définition de cette configuration sur la valeur `true` permet d’activer les fonctionnalités suivantes :

| **Fonctionnalité** | **Fonction** |
| ---------------------- | ------------------ |
| Validation synchrone | Valide les données collectées par rapport au schéma et renvoie une erreur dans la réponse sous le libellé suivant : `collect:error OR success` |
| Journalisation de la console | Permet l’affichage des messages de débogage dans la console JavaScript du navigateur. |

### `edgeDomain` {#edge-domain}

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ------------------ |
| Chaîne | Non | `beta.adobedc.net` |
| Chaîne | Non | `omtrdc.net` |

Domaine utilisé pour interagir avec les services d’Adobe. Cette valeur est utilisée uniquement si vous disposez d’un domaine propriétaire (CNAME) qui effectue des requêtes proxy vers l’infrastructure Adobe Edge.

### `orgId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

ID d&#39;organisation [!DNL Experience Cloud] que vous avez attribué.  Lors de la configuration de plusieurs instances dans une page, vous devez configurer un `orgId` différent pour chaque instance.

## Collecte de données

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Indique si les données associées aux clics sur les liens doivent être automatiquement collectées. Voir [Suivi automatique des liens](../data-collection/track-links.md#automaticLinkTracking) pour plus d’informations.

### `onBeforeEventSend`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Fonction | Non | () => non définie |

Définissez cette option pour configurer un rappel appelé pour chaque événement juste avant son envoi.  Un objet avec le champ `xdm` est envoyé dans le rappel.  Modifiez l&#39;objet `xdm` pour modifier ce qui est envoyé.  Dans le rappel, les données de l’objet `xdm` sont déjà transmises dans la commande d’événement et les informations collectées automatiquement. Pour plus d’informations sur le minutage de ce rappel et pour obtenir un exemple, voir [Modification globale des événements](tracking-events.md#modifying-events-globally).

## Options de confidentialité

### `defaultConsent` {#default-consent}

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Objet | Non | `"in"` |

Définit le consentement par défaut de l’utilisateur. Cette option est utilisée lorsqu’aucune préférence de consentement n’est déjà enregistrée pour l’utilisateur. L’autre valeur valide est `"pending"`. Lorsque cette option est définie, le travail est mis en file d’attente jusqu’à ce que l’utilisateur indique ses préférences de consentement. Une fois les préférences de l’utilisateur fournies, le travail se poursuit ou est abandonné en fonction de celles-ci. Pour plus d’informations, voir [Prise en charge du consentement](../consent/supporting-consent.md).

## Options de personnalisation

### `prehidingStyle`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Non | Aucune |

Permet de créer une définition de style CSS qui masque les zones de contenu de votre page web pendant le chargement du contenu personnalisé à partir du serveur. Si cette option n’est pas fournie, le SDK ne tente pas de masquer les zones de contenu pendant le chargement du contenu personnalisé, ce qui peut entraîner un &quot;scintillement&quot;.

Si, par exemple, votre page web contient un élément ayant un ID `container` dont vous souhaitez masquer le contenu par défaut lors du chargement du contenu personnalisé à partir du serveur, voici un exemple de style prémasqué :

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Options d’audiences

### `cookieDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active les destinations de cookie [!DNL Audience Manager], ce qui permet la définition de cookies en fonction de la qualification du segment.

### `urlDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active les destinations URL [!DNL Audience Manager], ce qui permet de déclencher des URL en fonction de la qualification des segments.

## Options d’identité

### `idMigrationEnabled` {#id-migration-enabled}

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | vrai |

Si la valeur est true, le SDK lit et définit les anciens cookies AMCV. Cela permet de passer à l’utilisation du SDK Web Adobe Experience Platform alors que certaines parties du site peuvent encore utiliser Visiteur.js. De plus, si l’API du Visiteur est définie sur la page, le SDK requête l’API du Visiteur pour l’ECID. Cela vous permet de créer deux pages de balises avec le SDK Web AEP et d’avoir toujours le même ECID.

### `thirdPartyCookiesEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | vrai |

Active le paramètre des cookies tiers Adobe. Le SDK permet de conserver l’ID de visiteur dans un contexte tiers afin de permettre l’utilisation du même ID de visiteur sur plusieurs sites. Cela s’avère utile si vous disposez de plusieurs sites ou si vous souhaitez partager des données avec des partenaires ; toutefois, pour des raisons de confidentialité, cela n’est pas toujours souhaitable.
