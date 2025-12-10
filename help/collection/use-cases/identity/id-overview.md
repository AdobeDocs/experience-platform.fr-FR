---
title: Données d’identité dans le SDK Web
description: Découvrez comment récupérer et gérer les Adobe Experience Cloud ID (ECID) à l’aide de Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 1%

---

# Données d’identité dans le SDK Web

Adobe Experience Platform Web SDK utilise [des identifiants Adobe Experience Cloud (ECID)](/help/identity-service/features/ecid.md) pour suivre le comportement des visiteurs. Grâce à [!DNL ECIDs], vous pouvez vous assurer que chaque appareil dispose d’un identifiant unique qui peut persister sur plusieurs sessions, liant tous les accès qui se produisent pendant et entre les sessions web à un appareil spécifique.

Ce document présente un aperçu de la gestion des [!DNL ECIDs] et des [!DNL CORE IDs] à l’aide de Web SDK.

## Suivi des ECID à l’aide de Web SDK {#tracking-ecids-web-sdk}

Le SDK Web attribue et suit les [!DNL ECIDs] à l’aide de cookies, avec plusieurs méthodes disponibles pour configurer la manière dont ces cookies sont générés.

Lorsqu’un nouvel utilisateur arrive sur votre site web, le service d’identités [Adobe Experience Cloud](/help/identity-service/home.md) tente de définir un cookie d’identification d’appareil pour cet utilisateur.

* Pour les nouveaux visiteurs, une [!DNL ECID] est générée et renvoyée dans la première réponse d’Experience Platform Edge Network.
* Pour les visiteurs réguliers, la [!DNL ECID] est récupérée à partir du cookie [`kndctr_<orgId>_identity`](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) et ajoutée à la payload de la requête par Edge Network.

Une fois le cookie contenant le [!DNL ECID] défini, chaque requête suivante générée par le SDK Web inclut un [!DNL ECID] codé dans le cookie `kndctr_<orgId>_identity`.

Lors de l’utilisation de cookies pour l’identification d’un appareil, vous avez deux manières d’interagir avec Edge Network :

1. Créez un CNAME sur votre propre domaine qui pointe vers `adobedc.net`. Cette méthode est appelée [collecte de données propriétaire](#first-party).
1. Envoyez directement les données au `adobedc.net` de domaine Edge Network. Cette méthode est appelée [&#x200B; collecte de données tierce &#x200B;](#third-party).

Comme expliqué dans les sections ci-dessous, la méthode de collecte de données que vous choisissez d’utiliser a un impact direct sur la durée de vie des cookies dans les navigateurs.

## Suivi des identifiants CORE à l’aide de Web SDK {#tracking-coreid-web-sdk}

Lors de l’utilisation de Google Chrome avec des cookies tiers activés et qu’aucun cookie `kndctr_<orgId>_identity` n’est défini, la première requête Edge Network passe par un domaine `demdex.net`, qui définit un cookie demdex. Ce cookie contient un [!DNL CORE ID]. Il s’agit d’un identifiant utilisateur unique, différent du [!DNL ECID].

Selon votre implémentation, vous pouvez [accéder au  [!DNL CORE ID]](#retrieve-coreid).

### Collecte de données propriétaire {#first-party}

La collecte de données propriétaire implique de définir des cookies par le biais d’un `CNAME` sur votre propre domaine qui pointe vers `adobedc.net`.

Bien que les navigateurs aient longtemps traité les cookies définis par `CNAME` points d’entrée de la même manière que ceux définis par les points d’entrée appartenant au site, des modifications récentes mises en œuvre par les navigateurs ont créé une distinction dans la manière dont les cookies `CNAME` sont traités. Bien qu’aucun navigateur ne bloque actuellement les cookies `CNAME` propriétaires par défaut, certains navigateurs limitent la durée de vie des cookies définis à l’aide d’un `CNAME` à seulement sept jours.

### Collecte de données tierces {#third-party}

La collecte de données tierces implique l’envoi direct de données au `adobedc.net` de domaine Edge Network.

Ces dernières années, les navigateurs web sont devenus de plus en plus restrictifs dans leur gestion des cookies définis par des tiers. Certains navigateurs bloquent les cookies tiers par défaut. Si vous utilisez des cookies tiers pour identifier les visiteurs du site, la durée de vie de ces cookies est presque toujours inférieure à celle qui serait disponible autrement à l’aide de cookies propriétaires. Parfois, un cookie tiers arrive à expiration dans un délai aussi court que sept jours.

En outre, lorsque vous utilisez la collecte de données tierce, certains bloqueurs d’annonces limitent le trafic aux points d’entrée de la collecte de données d’Adobe.

### Effets de la durée de vie des cookies sur les applications Adobe Experience Cloud {#lifespans}

Que vous choisissiez la collecte de données propriétaire ou tierce, la durée pendant laquelle un cookie peut persister a un impact direct sur le nombre de visiteurs dans [Adobe Analytics](https://experienceleague.adobe.com/fr/docs/analytics) et [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/customer-journey-analytics). En outre, les utilisateurs finaux peuvent rencontrer des expériences de personnalisation incohérentes lorsque [Adobe Target](https://experienceleague.adobe.com/en/docs/target) ou [Offer Decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision) sont utilisés sur le site.

Supposons, par exemple, que vous ayez créé une expérience de personnalisation qui promeut n’importe quel élément sur la page d’accueil si un utilisateur l’a consulté trois fois au cours des sept derniers jours.

Si un utilisateur final visite le site trois fois par semaine et ne revient pas sur le site pendant sept jours, il peut être considéré comme un nouvel utilisateur lorsqu’il y revient, car ses cookies peuvent avoir été supprimés par une politique de navigateur (en fonction du navigateur qu’il utilisait lors de sa visite). Si cela se produit, votre outil Analytics traite le visiteur comme un nouvel utilisateur, même s’il a visité le site il y a un peu plus de sept jours. En outre, tout effort de personnalisation de l’expérience pour l’utilisateur ou l’utilisatrice recommence.

### Identifiants d’appareils propriétaires (FPID) {#fpid}

Pour tenir compte des effets de la durée de vie des cookies comme indiqué ci-dessus, vous pouvez choisir de définir et de gérer vos propres identifiants d’appareil à la place. Pour plus d’informations, consultez le guide des [Identifiants d’appareils propriétaires](./first-party-device-ids.md).

## Récupérer l’ECID et la région pour l’utilisateur actuel {#retrieve-ecid}

Selon votre cas d’utilisation, vous pouvez accéder au [!DNL ECID] de deux façons :

* [Récupérer le via la préparation  [!DNL ECID]  données pour la collecte de données](#retrieve-ecid-data-prep) : il s’agit de la méthode recommandée que vous devez utiliser.
* [Récupérer le via  [!DNL ECID]  commande `getIdentity()`](#retrieve-ecid-getidentity) : n’utilisez cette méthode que lorsque vous avez besoin des informations [!DNL ECID] côté client.

### Récupérez le [!DNL ECID] via la préparation des données pour la collecte de données {#retrieve-ecid-data-prep}

Utilisez [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md) pour mapper la [!DNL ECID] à un champ [!DNL XDM]. Il s’agit de la méthode recommandée pour accéder au [!DNL ECID].

Pour ce faire, définissez le champ source sur le chemin suivant :

```js
xdm.identityMap.ECID[0].id
```

Définissez ensuite le champ cible sur un chemin XDM où le champ est de type `string`.

![Capture d’écran du mappage de flux de données](/help/tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Récupérez le [!DNL ECID] via la commande `getIdentity()` {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>Vous ne devez récupérer l’ECID que par le biais de la commande `getIdentity()` si vous avez besoin de l’[!DNL ECID] côté client. Si vous souhaitez uniquement mapper l’ECID à un champ XDM, utilisez plutôt [Préparation des données pour la collecte de données](#retrieve-ecid-data-prep).

Pour récupérer l’ECID unique du visiteur actuel, utilisez la commande `getIdentity` . Pour les nouveaux visiteurs qui n’ont pas encore de [!DNL ECID], cette commande génère une nouvelle [!DNL ECID]. `getIdentity` renvoie également l’ID de région pour le visiteur.

>[!NOTE]
>
>Cette méthode est généralement utilisée avec des solutions personnalisées qui nécessitent de lire l’identifiant de [!DNL Experience Cloud] ou qui nécessitent un conseil d’emplacement pour Adobe Audience Manager. Il n’est pas utilisé par une implémentation standard.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Récupérer l’ID CORE pour l’utilisateur actuel {#retrieve-coreid}

Pour récupérer l’ID CORE d’un utilisateur, vous pouvez utiliser la commande [`getIdentity()`](/help/collection/js/commands/getidentity.md), comme illustré ci-dessous.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```

## Utilisation de `identityMap` {#using-identitymap}

À l’aide d’un champ de [`identityMap` XDM](/help/xdm/schema/composition.md#identityMap) vous pouvez identifier un appareil/utilisateur à l’aide de plusieurs identités, définir son état d’authentification et décider quel identifiant est considéré comme le principal. Si aucun identifiant n’a été défini comme `primary`, le principal est par défaut le `ECID`.

`identityMap` champs sont mis à jour à l’aide de la commande `sentEvent` .

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>Adobe recommande d’envoyer des espaces de noms qui représentent une personne, tels que `CRMID`, comme identité principale.

Chaque propriété dans `identityMap` représente des identités appartenant à un [espace de noms d’identité](/help/identity-service/features/namespaces.md) particulier. Le nom de la propriété doit être le symbole d’espace de noms d’identité. Il est répertorié dans l’interface utilisateur de Adobe Experience Platform sous « [!UICONTROL Identities] ». La valeur de la propriété doit être un tableau d’identités appartenant à cet espace de noms d’identité.

>[!IMPORTANT]
>
>L’identifiant d’espace de noms transmis dans le `identityMap` est sensible à la casse. Veillez à utiliser l’identifiant d’espace de noms correct pour éviter une collecte de données incomplète.

Chaque objet d’identité du tableau d’identités contient les propriétés suivantes :

| Propriété | Type de données | Description |
| --- | --- | --- |
| `id` | Chaîne | **(Obligatoire)** Identifiant à définir pour l’espace de noms donné. |
| `authenticatedState` | Chaîne | **(Obligatoire)** État d’authentification de l’ID. Les valeurs possibles sont les suivantes : `ambiguous`, `authenticated` et `loggedOut`. |
| `primary` | Booléen | Détermine si cette identité doit être utilisée comme fragment principal dans le profil. Par défaut, l’ECID est défini comme identifiant principal de l’utilisateur. Cette valeur est définie par défaut sur `false` si vous l’ignorez. |

L’utilisation du champ `identityMap` pour identifier les appareils ou les utilisateurs aboutit au même résultat que l’utilisation de la méthode [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) du [!DNL ID Service API] . Pour plus d’informations[&#x200B; consultez la documentation de l’API du service &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html)ID.

## Migration de l’API visiteur vers ECID {#migrating-visitor-api-ecid}

Lors de la migration à partir de à l’aide de l’API visiteur, vous pouvez également migrer les cookies AMCV existants. Pour activer la migration ECID, définissez le paramètre `idMigrationEnabled` dans la configuration. La migration des identifiants active les cas d’utilisation suivants :

* Lorsque certaines pages d’un domaine utilisent l’API visiteur et d’autres pages utilisent ce SDK. Pour prendre en charge ce cas, le SDK lit les cookies AMCV existants et écrit un nouveau cookie avec l’ECID existant. En outre, le SDK écrit des cookies AMCV afin que si l’ECID est obtenu en premier sur une page instrumentée avec le SDK, les pages suivantes instrumentées avec l’API visiteur disposent du même ECID.
* Lorsque Adobe Experience Platform Web SDK est configuré sur une page qui comporte également une API visiteur. Pour prendre en charge ce cas, si le cookie AMCV n’est pas défini, le SDK recherche l’API visiteur sur la page et l’appelle pour obtenir l’ECID.
* Lorsque l’ensemble du site utilise Adobe Experience Platform Web SDK et ne dispose pas d’une API visiteur, il est utile de migrer les ECID afin que les informations du visiteur renvoyé soient conservées. Une fois le SDK déployé avec `idMigrationEnabled` pendant un certain temps afin que la plupart des cookies des visiteurs soient migrés, le paramètre peut être désactivé.

### Mise à jour des caractéristiques pour la migration

Lorsque des données au format XDM sont envoyées dans Audience Manager, elles doivent être converties en signaux lors de la migration. Vos caractéristiques doivent être mises à jour pour refléter les nouvelles clés fournies par XDM. Ce processus est facilité par l’utilisation de l’outil [BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) créé par Audience Manager.

## Utilisation dans le transfert d’événement

Si le [transfert d’événement](/help/tags/ui/event-forwarding/overview.md) est actuellement activé et que vous utilisez `appmeasurement.js` et `visitor.js`, vous pouvez conserver la fonctionnalité de transfert d’événement activée, ce qui ne provoquera aucun problème. Sur le serveur principal, Adobe récupère tous les segments AAM et les ajoute à l’appel à Analytics. Si l’appel à Analytics contient ces segments, Analytics n’appelle pas Audience Manager pour transférer des données. Il n’y a donc pas de double collecte de données. Il n’est pas non plus nécessaire d’utiliser l’indicateur d’emplacement lors de l’utilisation de Web SDK, car les mêmes points d’entrée de segmentation sont appelés dans le serveur principal.
