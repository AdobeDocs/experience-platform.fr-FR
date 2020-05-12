---
title: Configuration du SDK
seo-title: Configuration du SDK Web d’Adobe Experience Platform
description: Découvrez la procédure de configuration du SDK Web d’Experience Platform
seo-description: Découvrez la procédure de configuration du SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: 767f0e1bfdfcc898313b546c804ba1287f2aec50
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 100%

---


# (Version bêta) Configuration du SDK

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

La configuration du SDK est effectuée à l’aide de la commande `configure`.

>[!IImportant]
>`configure` doit _toujours_ être la première commande appelée.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

De nombreuses options peuvent être définies lors de la configuration. Vous trouverez ci-dessous toutes les options regroupées par catégorie.

## Options générales

### `configId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

L’ID de configuration que vous avez attribué, qui lie le SDK aux comptes et à la configuration appropriés.  Lors de la configuration de plusieurs instances dans une seule page, vous devez configurer un `configId` différent pour chaque instance.

### `context`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| ---------------- | ------------ | -------------------------------------------------- |
| Tableau de chaînes | Non | `["web", "device", "environment", "placeContext"]` |

Indique les catégories contextuelles à collecter automatiquement, comme décrit dans la section [Informations automatiques](../reference/automatic-information.md).  Si cette configuration n’est pas spécifiée, toutes les catégories sont utilisées par défaut.

### `debugEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `false` |

Indique si le débogage doit être activé. La définition de cette configuration sur la valeur `true` permet d’activer les fonctionnalités suivantes :

| **Fonctionnalité** |  |  |
| ---------------------- | ------------------ |
| Validation synchrone | Valide les données collectées par rapport au schéma et renvoie une erreur dans la réponse sous le libellé suivant : `collect:error OR success` |
| Journalisation de la console | Permet l’affichage des messages de débogage dans la console JavaScript du navigateur. |

### `edgeDomain`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ------------------ |
| Chaîne | Non | `beta.adobedc.net` |

Domaine utilisé pour interagir avec Adobe Services. Cette valeur est utilisée uniquement si vous disposez d’un domaine propriétaire (CNAME) qui effectue des requêtes proxy vers l’infrastructure Adobe Edge.

### `orgId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

L’identifiant d’organisation d’Experience Cloud qui vous est attribué.  Lors de la configuration de plusieurs instances dans une page, vous devez configurer un `orgId` différent pour chaque instance.

## Collecte de données

### `clickCollectionEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Indique si les données associées aux clics sur les liens doivent être automatiquement collectées. Pour les clics considérés comme des clics sur des liens, les données d’[interaction Web](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) suivantes sont collectées :

| **Propriété** |  |
| ------------ | ----------------------------------- |
| Nom du lien | Nom déterminé par le contexte du lien |
| URL du lien | URL normalisée |
| Type de lien | Défini sur téléchargement, sortie ou autre |

### `onBeforeEventSend`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Fonction | Non | () => non définie |

Définissez cette option pour configurer un rappel appelé pour chaque événement juste avant son envoi.  Un objet avec le champ `xdm` est envoyé dans le rappel.  Modifiez l’objet xdm pour changer ce qui est envoyé.  Dans le rappel, les données de l’objet `xdm` sont déjà transmises dans la commande d’événement et les informations collectées automatiquement.  Pour plus d’informations sur le minutage de ce rappel et pour obtenir un exemple, voir [Modification globale des événements](tracking-events.md#modifying-events-globally).

## Options de confidentialité

### `defaultConsent`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Objet | Non | `{"general": "in"}` |

Définit le consentement par défaut de l’utilisateur. Cette option est utilisée lorsqu’aucune préférence de consentement n’est déjà enregistrée pour l’utilisateur. L’autre valeur valide est `{"general": "pending"}`. Lorsque cette option est définie, le travail est mis en file d’attente jusqu’à ce que l’utilisateur indique ses préférences de consentement. Une fois les préférences de l’utilisateur fournies, le travail se poursuit ou est abandonné en fonction de celles-ci. Pour plus d’informations, voir [Prise en charge du consentement](supporting-consent.md).

## Options de personnalisation

### `prehidingStyle`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Non | Aucune |

Permet de créer une définition de style CSS qui masque les zones de contenu de votre page web pendant le chargement du contenu personnalisé à partir du serveur. Si cette option n’est pas spécifiée, le SDK ne tente pas de masquer les zones de contenu pendant le chargement du contenu personnalisé, ce qui peut entraîner un « scintillement ».

Si, par exemple, votre page web contient un élément ayant un ID `container` dont vous souhaitez masquer le contenu par défaut lors du chargement du contenu personnalisé à partir du serveur, voici un exemple de style prémasqué :

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Options d’audiences

### `cookieDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active les destinations de cookies, ce qui permet de définir des cookies en fonction de la qualification des segments.

### `urlDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active les destinations d’URL, ce qui permet le déclenchement d’URL en fonction de la qualification des segments.

## Options d’identité

### `idSyncContainerId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Nombre | Non | Aucune |

ID de conteneur qui spécifie les synchronisations d’identifiants qui sont déclenchées. Il s’agit d’un entier non négatif que vous pouvez obtenir auprès de votre consultant.

### `idSyncEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active la fonctionnalité de synchronisation des identifiants, qui permet de déclencher des URL pour synchroniser l’ID utilisateur unique Adobe avec l’ID utilisateur unique d’une source de données tierce.

### `thirdPartyCookiesEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | vrai |

Active le paramètre des cookies tiers Adobe. Le kit SDK permet de conserver l’identifiant visiteur dans un contexte tiers afin de permettre l’utilisation du même identifiant visiteur sur l’ensemble du site. Cela s’avère utile si vous disposez de plusieurs sites ou si vous souhaitez partager des données avec des partenaires ; toutefois, pour des raisons de confidentialité, cela n’est pas toujours souhaitable.
