---
title: Configuration du SDK Web de Adobe Experience Platform
description: Découvrez comment configurer le SDK Web de Adobe Experience Platform.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 24%

---


# Configuration du SDK Web

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

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucun |

{style="table-layout:auto"}

L’identifiant de configuration qui vous a été attribué, qui lie le SDK aux comptes et à la configuration appropriés. Lors de la configuration de plusieurs instances dans une seule page, vous devez configurer un `edgeConfigId` différent pour chaque instance.

### `context` {#context}

| **Type** | Obligatoire | **Valeur par défaut** |
| ---------------- | ------------ | -------------------------------------------------- |
| Tableau de chaînes | Non | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

Indique les catégories contextuelles à collecter automatiquement, comme décrit dans la section [Informations automatiques](../data-collection/automatic-information.md). Si cette configuration n&#39;est pas spécifiée, toutes les catégories sont utilisées par défaut.

>[!IMPORTANT]
>
>Toutes les propriétés contextuelles, à l’exception de `highEntropyUserAgentHints`, sont activés par défaut. Si vous avez spécifié les propriétés de contexte manuellement dans votre configuration de SDK Web, vous devez activer toutes les propriétés de contexte pour continuer à collecter les informations nécessaires.

Pour activer [indices client à forte entropie](user-agent-client-hints.md#enabling-high-entropy-client-hints) sur votre déploiement du SDK Web, vous devez inclure les `highEntropyUserAgentHints` l’option contextuelle , avec votre configuration existante.

Par exemple, pour récupérer des indices client à forte entropie à partir de propriétés web, votre configuration ressemblerait à ceci :

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Booléen | Non | `false` |

{style="table-layout:auto"}

Indique si le débogage est activé. La définition de cette configuration sur la valeur `true` permet d’activer les fonctionnalités suivantes :

| **Fonctionnalité** | **Fonction** |
| ---------------------- | ------------------ |
| Journalisation de la console | Permet l’affichage des messages de débogage dans la console JavaScript du navigateur. |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

Renseignez ce champ avec votre domaine propriétaire. Pour plus d’informations, voir [documentation](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=fr).

Le domaine est similaire à `data.{customerdomain.com}` pour un site web à l’adresse www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Chemin d’accès après le edgeDomain utilisé pour communiquer et interagir avec les services Adobe.  Souvent, cela ne change que si vous n’utilisez pas l’environnement de production par défaut.

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Chaîne | Non | ee |

{style="table-layout:auto"}

### `orgId`

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucun |

{style="table-layout:auto"}

Votre [!DNL Experience Cloud] ID d’organisation. Lors de la configuration de plusieurs instances dans une page, vous devez configurer un `orgId` différent pour chaque instance.

## Collecte de données

### `clickCollectionEnabled` {#clickCollectionEnabled}

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style="table-layout:auto"}

Indique si les données associées aux clics sur les liens sont automatiquement collectées. Voir [Suivi automatique des liens](../data-collection/track-links.md#automaticLinkTracking) pour plus d’informations. Les liens sont également étiquetés comme liens de téléchargement s’ils incluent un attribut de téléchargement ou si le lien se termine par une extension de fichier. Les qualificateurs de lien de téléchargement peuvent être configurés avec une expression régulière. La valeur par défaut est `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`.

### `onBeforeEventSend`

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Fonction | Non | () => non définie |

{style="table-layout:auto"}

Configurez un rappel appelé pour chaque événement juste avant son envoi. Objet avec le champ `xdm` est envoyé au rappel. Pour modifier ce qui est envoyé, modifiez la variable `xdm` . Dans le rappel, la variable `xdm` contient déjà les données transmises dans la commande d’événement et les informations collectées automatiquement. Pour plus d’informations sur le minutage de ce rappel et pour obtenir un exemple, voir [Modification globale des événements](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Fonction | Non | () => non définie |

{style="table-layout:auto"}

Configurez un rappel appelé pour chaque événement de suivi des clics sur les liens juste avant son envoi. Le rappel envoie un objet avec l’événement `xdm`, `clickedElement`, et `data` des champs.

Lors du filtrage du suivi des liens à l’aide de la structure d’éléments DOM, vous pouvez utiliser la variable `clickElement` . `clickedElement` est le noeud d’élément DOM sur lequel l’utilisateur a cliqué et qui a encapsulé l’arborescence des noeuds parents.

Pour modifier les données envoyées, modifiez la variable `xdm` et/ou `data` objets. Dans le rappel, la variable `xdm` contient déjà les données transmises dans la commande d’événement et les informations collectées automatiquement.

* Toute valeur autre que `false` permet le traitement de l’événement et l’envoi du rappel.
* Si le rappel renvoie la variable `false` , le traitement des événements est arrêté, sans erreur, et l’événement n’est pas envoyé. Ce mécanisme permet de filtrer certains événements en examinant les données d’événement et en renvoyant `false` si l’événement ne doit pas être envoyé.
* Si le rappel renvoie une exception, le traitement de l’événement est arrêté et l’événement n’est pas envoyé.


## Options de confidentialité

### `defaultConsent` {#default-consent}

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Objet | Non | `"in"` |

{style="table-layout:auto"}

Définit le consentement par défaut de l’utilisateur. Utilisez ce paramètre lorsqu’aucune préférence de consentement n’est déjà enregistrée pour l’utilisateur. Les autres valeurs valides sont `"pending"` et `"out"`. Cette valeur par défaut n’est pas conservée dans le profil de l’utilisateur. Le profil de l’utilisateur n’est mis à jour que lorsque `setConsent` est appelée.
* `"in"`: lorsque ce paramètre est défini ou qu’aucune valeur n’est fournie, le travail se poursuit sans préférences de consentement de l’utilisateur.
* `"pending"`: lorsque ce paramètre est défini, le travail est mis en file d’attente jusqu’à ce que l’utilisateur fournisse les préférences de consentement.
* `"out"`: lorsque ce paramètre est défini, le travail est ignoré jusqu’à ce que l’utilisateur fournisse les préférences de consentement.
Une fois les préférences de l’utilisateur fournies, le travail se poursuit ou est abandonné en fonction de celles-ci. Pour plus d’informations, voir [Prise en charge du consentement](../consent/supporting-consent.md).

## Options de personnalisation {#personalization}

### `prehidingStyle` {#prehidingStyle}

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Chaîne | Non | Aucun |

{style="table-layout:auto"}

Permet de créer une définition de style CSS qui masque les zones de contenu de votre page web pendant le chargement du contenu personnalisé à partir du serveur. Si cette option n’est pas fournie, le SDK ne tente pas de masquer les zones de contenu pendant le chargement du contenu personnalisé, ce qui peut entraîner un &quot;scintillement&quot;.

Par exemple, si un élément de votre page web comporte un identifiant de `container`, dont vous souhaitez masquer le contenu par défaut lorsque le contenu personnalisé est chargé à partir du serveur, utilisez le style de prémasquage suivant :

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

Cette option doit être utilisée lors de la migration de pages individuelles depuis [!DNL at.js] vers le SDK Web.

Utilisez cette option pour permettre au SDK Web de lire et d’écrire l’héritage `mbox` et `mboxEdgeCluster` les cookies utilisés par [!DNL at.js]. Vous pouvez ainsi conserver le profil du visiteur lors du passage d’une page qui utilise le SDK Web à une page qui utilise la variable [!DNL at.js] et vice versa.

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Booléen | Non | `false` |

## Options d’audiences

### `cookieDestinationsEnabled`

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style="table-layout:auto"}

Active [!DNL Audience Manager] destinations de cookie, qui permet de définir des cookies en fonction de la qualification des segments.

### `urlDestinationsEnabled`

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style="table-layout:auto"}

Active [!DNL Audience Manager] Destinations d’URL, qui permettent de déclencher des URL en fonction de la qualification des segments.

## Options d’identité

### `idMigrationEnabled` {#id-migration-enabled}

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style="table-layout:auto"}

Si la valeur est true, le SDK lit et définit les anciens cookies AMCV. Cette option permet de passer à l’utilisation du SDK Web de Adobe Experience Platform, tandis que certaines parties du site peuvent toujours utiliser Visitor.js.

Si l’API visiteur est définie sur la page, le SDK interroge l’API visiteur pour l’ECID. Cette option vous permet de créer des pages à deux balises avec le SDK Web de Adobe Experience Platform et qui possèdent toujours le même ECID.

### `thirdPartyCookiesEnabled`

| Type | Obligatoire | Valeur par défaut |
| -------- | ------------ | ----------------- |
| Booléen | Non | `true` |

{style="table-layout:auto"}

Active le paramètre des cookies tiers Adobe. Le SDK peut conserver l’identifiant visiteur dans un contexte tiers afin de permettre l’utilisation du même identifiant visiteur sur plusieurs sites. Utilisez cette option si vous disposez de plusieurs sites ou si vous souhaitez partager des données avec des partenaires. Toutefois, cette option n’est parfois pas souhaitée pour des raisons de confidentialité.
