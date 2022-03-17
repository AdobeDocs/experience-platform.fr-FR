---
title: Configuration du SDK Web de Adobe Experience Platform
description: Découvrez comment configurer le SDK Web de Adobe Experience Platform.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configure;configuration;SDK;edge;SDK Web;configure;edgeConfigId;contexte;web;périphérique;environnement;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;paramètres du sdk web;prehideStyle;opacity;cookieDestinationsEnabled;urlDestinations;idMigrationEnabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: 4d0f1b3e064bd7b24e17ff0fafb50d930b128968
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 39%

---

# Configuration du SDK Web de Platform

La configuration du SDK est effectuée à l’aide de la commande `configure`.

>[!IMPORTANT]
>
>`configure` is *always* la première commande appelée.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

De nombreuses options peuvent être définies lors de la configuration. Vous trouverez ci-dessous toutes les options regroupées par catégorie.

## Options générales

### `edgeConfigId`

>[!NOTE]
>
>**Les configurations Edge ont été renommées en Datastreams. Un identifiant de flux de données est identique à un identifiant de configuration.**

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucun |

{style=&quot;table-layout:auto&quot;}

L’ID de configuration que vous avez attribué, qui lie le SDK aux comptes et à la configuration appropriés. Lors de la configuration de plusieurs instances dans une seule page, vous devez configurer un `edgeConfigId` différent pour chaque instance.

### `context`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| ---------------- | ------------ | -------------------------------------------------- |
| Tableau de chaînes | Non | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

Indique les catégories contextuelles à collecter automatiquement, comme décrit dans la section [Informations automatiques](../data-collection/automatic-information.md). Si cette configuration n&#39;est pas spécifiée, toutes les catégories sont utilisées par défaut.

### `debugEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `false` |

{style=&quot;table-layout:auto&quot;}

Indique si le débogage est activé. La définition de cette configuration sur la valeur `true` permet d’activer les fonctionnalités suivantes :

| **Fonctionnalité** | **Fonction** |
| ---------------------- | ------------------ |
| Journalisation de la console | Permet l’affichage des messages de débogage dans la console JavaScript du navigateur. |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Renseignez ce champ avec votre domaine propriétaire. Pour plus d’informations, reportez-vous à la section [documentation](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=fr).

Le domaine est similaire à `data.{customerdomain.com}` pour un site web à l’adresse www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Chemin d’accès après le edgeDomain utilisé pour communiquer et interagir avec les services Adobe.  Souvent, cela ne change que si vous n’utilisez pas l’environnement de production par défaut.

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Non | ee |

{style=&quot;table-layout:auto&quot;}

### `orgId`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucun |

{style=&quot;table-layout:auto&quot;}

Votre [!DNL Experience Cloud] ID d’organisation. Lors de la configuration de plusieurs instances dans une page, vous devez configurer un `orgId` différent pour chaque instance.

## Collecte de données

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style=&quot;table-layout:auto&quot;}

Indique si les données associées aux clics sur les liens sont automatiquement collectées. Voir [Suivi automatique des liens](../data-collection/track-links.md#automaticLinkTracking) pour plus d’informations. Les liens sont également étiquetés comme liens de téléchargement s’ils incluent un attribut de téléchargement ou si le lien se termine par une extension de fichier. Les qualificateurs de lien de téléchargement peuvent être configurés avec une expression régulière. La valeur par défaut est `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Fonction | Non | () => non définie |

{style=&quot;table-layout:auto&quot;}

Configurez un rappel appelé pour chaque événement juste avant son envoi. Un objet avec le champ `xdm` est envoyé dans le rappel. Pour modifier ce qui est envoyé, modifiez la variable `xdm` . Dans le rappel, la variable `xdm` contient déjà les données transmises dans la commande d’événement et les informations collectées automatiquement. Pour plus d’informations sur le minutage de ce rappel et pour obtenir un exemple, voir [Modification globale des événements](tracking-events.md#modifying-events-globally).

## Options de confidentialité

### `defaultConsent` {#default-consent}

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Objet | Non | `"in"` |

{style=&quot;table-layout:auto&quot;}

Définit le consentement par défaut de l’utilisateur. Utilisez ce paramètre lorsqu’aucune préférence de consentement n’est déjà enregistrée pour l’utilisateur. Les autres valeurs valides sont `"pending"` et `"out"`. Cette valeur par défaut n’est pas conservée dans le profil de l’utilisateur. Le profil de l’utilisateur n’est mis à jour que lorsque `setConsent` est appelée.
* `"in"`: Lorsque ce paramètre est défini ou qu’aucune valeur n’est fournie, le travail se poursuit sans préférences de consentement de l’utilisateur.
* `"pending"`: Lorsque ce paramètre est défini, le travail est mis en file d’attente jusqu’à ce que l’utilisateur fournisse les préférences de consentement.
* `"out"`: Lorsque ce paramètre est défini, le travail est ignoré jusqu’à ce que l’utilisateur fournisse les préférences de consentement.
Une fois les préférences de l’utilisateur fournies, le travail se poursuit ou est abandonné en fonction de celles-ci. Pour plus d’informations, voir [Prise en charge du consentement](../consent/supporting-consent.md).

## Options de personnalisation

### `prehidingStyle`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Non | Aucun |

{style=&quot;table-layout:auto&quot;}

Permet de créer une définition de style CSS qui masque les zones de contenu de votre page web pendant le chargement du contenu personnalisé à partir du serveur. Si cette option n’est pas fournie, le SDK ne tente pas de masquer les zones de contenu pendant le chargement du contenu personnalisé, ce qui peut entraîner un &quot;scintillement&quot;.

Par exemple, si un élément de votre page web comporte un identifiant de `container`, dont vous souhaitez masquer le contenu par défaut lorsque le contenu personnalisé est chargé à partir du serveur, utilisez le style de prémasquage suivant :

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Options d’audiences

### `cookieDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style=&quot;table-layout:auto&quot;}

Active [!DNL Audience Manager] destinations de cookie, qui permet de définir des cookies en fonction de la qualification des segments.

### `urlDestinationsEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style=&quot;table-layout:auto&quot;}

Active [!DNL Audience Manager] Destinations d’URL, qui permettent de déclencher des URL en fonction de la qualification des segments.

## Options d’identité

### `idMigrationEnabled` {#id-migration-enabled}

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style=&quot;table-layout:auto&quot;}

Si la valeur est true, le SDK lit et définit les anciens cookies AMCV. Cette option permet de passer à l’utilisation du SDK Web Adobe Experience Platform, tandis que certaines parties du site peuvent toujours utiliser Visitor.js. Si l’API visiteur est définie sur la page, le SDK interroge l’API visiteur pour l’ECID. Cette option vous permet de créer des pages à deux balises avec le SDK Web de Adobe Experience Platform et qui possèdent toujours le même ECID.

### `thirdPartyCookiesEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style=&quot;table-layout:auto&quot;}

Active le paramètre des cookies tiers Adobe. Le SDK peut conserver l’identifiant visiteur dans un contexte tiers afin de permettre l’utilisation du même identifiant visiteur sur plusieurs sites. Utilisez cette option si vous disposez de plusieurs sites ou si vous souhaitez partager des données avec des partenaires. cependant, cette option n’est parfois pas souhaitée pour des raisons de confidentialité.
