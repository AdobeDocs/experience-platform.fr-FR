---
title: Configuration du SDK
seo-title: Configuration du SDK Web d’Adobe Experience Platform
description: Découvrez comment configurer le SDK Web de la plate-forme d’expérience
seo-description: Découvrez comment configurer le SDK Web de la plate-forme d’expérience
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (bêta) Configuration du SDK

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

La configuration du SDK est effectuée à l’aide de la `configure` commande.

>[!Iimportant]
>`configure` doit _toujours_ être la première commande appelée.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

De nombreuses options peuvent être définies lors de la configuration. Vous trouverez ci-dessous toutes les options regroupées par  de.

## Options générales

### `configId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

L’ID de configuration que vous avez attribué, qui lie le SDK aux comptes et à la configuration appropriés.  Lors de la configuration de plusieurs instances dans une seule page, vous devez configurer une instance différente `configId` pour chaque instance.

### `context`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| ---------------- | ------------ | -------------------------------------------------- |
| Tableau de chaînes | Non | `["web", "device", "environment", "placeContext"]` |

Indique le contextuel à collecter automatiquement, comme décrit dans la section Informations [](../reference/automatic-information.md)automatiques.  Si cette configuration n’est pas spécifiée, tous les  de sont utilisés par défaut.

### `debugEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `false` |

Indique si le débogage doit être activé. La définition de cette configuration pour `true` activer les fonctionnalités suivantes :

| **Fonction** |  |  |
| ---------------------- | ------------------ |
| Validation synchrone | Valide les données collectées par rapport au  du et renvoie une erreur dans la réponse sous l’étiquette suivante : `collect:error OR success` |
| Journalisation de la console | Permet l’affichage des messages de débogage dans la console JavaScript du navigateur. |

### `edgeDomain`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ------------------ |
| Chaîne | Non | `beta.adobedc.net` |

Domaine utilisé pour interagir avec Adobe Services. Cette valeur est utilisée uniquement si vous disposez d’un domaine propriétaire (CNAME) qui effectue des requêtes proxy vers l’infrastructure Adobe Edge.

### `errorsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Indique si les erreurs doivent être supprimées. Comme décrit dans [Exécution des commandes](executing-commands.md), les erreurs _non interceptées_ sont consignées dans la console du développeur, que le débogage soit activé ou non dans le SDK Web d’Adobe Experience Platform. En définissant `errorsEnabled` sur `false`, les promesses renvoyées par le SDK Web d’Adobe Experience Platform ne sont jamais rejetées, bien que les erreurs soient toujours consignées dans la console si la journalisation est activée dans le SDK Web d’Adobe Experience Platform.

### `orgId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

ID d’organisation Experience Cloud que vous avez attribué.  Lors de la configuration de plusieurs instances dans une page, vous devez configurer une instance différente `orgId` pour chaque instance.

## Collecte de données

### `clickCollectionEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Indique si les données associées aux clics sur les liens doivent être automatiquement collectées. Pour les clics qualifiés de clics sur des liens, les données d’interaction [](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) Web suivantes sont collectées :

| **Propriété** |  |
| ------------ | ----------------------------------- |
| Link Name | Nom déterminé par le contexte du lien |
| URL du lien | URL normalisée |
| Type de lien | Défini pour télécharger, quitter ou autre |

### `onBeforeEventSend`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Fonction | Non | () => non définies |

Définissez cette option pour configurer un rappel appelé pour chaque juste avant son envoi.  Un objet avec le champ `xdm` est envoyé dans le rappel.  Modifiez l’objet xdm pour modifier ce qui est envoyé.  Dans le rappel, les données `xdm` de l’objet sont déjà transmises dans la commande de  du et les informations collectées automatiquement.  Pour plus d’informations sur le timing de ce rappel et pour consulter un exemple, voir [Modification de l’globalement](tracking-events.md#modifying-events-globally).

## Options de confidentialité

### `defaultConsent`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Objet | Non | `{"general": "in"}` |

Définit le consentement par défaut de l’utilisateur. Elle est utilisée lorsqu’aucune préférence de consentement n’est déjà enregistrée pour l’utilisateur. L’autre valeur valide est `{"general": "pending"}`. Lorsque cette option est définie, le travail est mis en file d’attente jusqu’à ce que l’utilisateur donne ses préférences de consentement. Une fois les préférences de l’utilisateur fournies, le travail se poursuit ou est abandonné en fonction des préférences de l’utilisateur. Pour plus d’informations, voir [Prise en charge du consentement](supporting-consent.md) .

## Options de personnalisation

### `prehidingStyle`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Non | Aucune |

Permet de créer une définition de style CSS qui masque les zones de contenu de votre page Web pendant le chargement du contenu personnalisé à partir du serveur. Si cette option n’est pas fournie, le SDK ne tente pas de masquer les zones de contenu pendant le chargement du contenu personnalisé, ce qui peut entraîner un &quot;scintillement&quot;.

Si, par exemple, vous aviez un élément sur votre page Web avec un ID dont `container` le contenu par défaut que vous souhaitez masquer lors du chargement du contenu personnalisé à partir du serveur, voici un exemple de style prémasqué :

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

##  options 

### `cookieDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active les destinations de cookies, ce qui permet de définir des cookies en fonction de la qualification des segments.

### `urlDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active les destinations URL, ce qui permet le déclenchement d’URL en fonction de la qualification des segments.

## Options d’identité

### `idSyncContainerId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Nombre | Non | Aucune |

ID de  qui spécifie l’ID synchronisé qui est déclenché. Il s’agit d’un entier non négatif qui peut être obtenu auprès de votre consultant.

### `idSyncEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

Active la fonctionnalité de synchronisation des identifiants, qui permet de déclencher des URL pour synchroniser l’ID utilisateur unique Adobe avec l’ID utilisateur unique d’une source de données tierce.

### `thirdPartyCookiesEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | true |

Active le paramètre des cookies tiers Adobe. Le kit SDK permet de conserver l’ID de dans un contexte tiers afin de permettre l’utilisation du même ID de sur l’ensemble du site. Cela s’avère utile si vous disposez de plusieurs sites ou si vous souhaitez partager des données avec des partenaires ; toutefois, cela n&#39; est pas toujours souhaitable pour des raisons de confidentialité.
