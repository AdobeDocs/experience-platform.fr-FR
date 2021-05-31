---
title: Récupération des ID Experience Cloud à l’aide du SDK Web de Adobe Experience Platform
description: Découvrez comment récupérer les Adobe Experience Cloud ID (ECID) à l’aide du SDK Web de Adobe Experience Platform.
seo-description: Découvrez comment obtenir l’identifiant Adobe Experience Cloud.
keywords: Identité;identité propriétaire;service d’identité;identité tierce;migration des identifiants;identifiant visiteur;identité tierce;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;synchroniser les identités;syncIdentity;sendEvent;identityMap;Principal;ecid;espace de noms d’identité;idd’espace de noms;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---

# Récupération des Adobe Experience Cloud ID

Le SDK Web de Adobe Experience Platform exploite [Adobe Identity Service](../../identity-service/ecid.md). Cela permet de s’assurer que chaque appareil dispose d’un identifiant unique qui est conservé sur l’appareil afin que l’activité entre les pages puisse être liée.

## Identité propriétaire

[!DNL Identity Service] stocke l’identité dans un cookie dans un domaine propriétaire. [!DNL Identity Service] tente de définir le cookie à l’aide d’un en-tête HTTP sur le domaine. Si cela échoue, la fonction [!DNL Identity Service] revient à définir des cookies via Javascript. Adobe vous recommande de configurer un CNAME pour vous assurer que vos cookies ne seront pas plafonnés par les restrictions ITP côté client.

## Identité tierce

[!DNL Identity Service] peut synchroniser un ID avec un domaine tiers (demdex.net) pour activer le suivi sur plusieurs sites. Lorsque cette option est activée, la première requête d’un visiteur (par exemple, une personne sans ECID) est envoyée à demdex.net. Cela ne sera effectué que sur les navigateurs qui le permettent (Chrome par exemple) et est contrôlé par le paramètre `thirdPartyCookiesEnabled` dans la configuration. Si vous souhaitez désactiver toutes ces fonctionnalités ensemble, définissez `thirdPartyCookiesEnabled` sur false.

## Migration des identifiants

Lors de la migration depuis à l’aide de l’API visiteur, vous pouvez également migrer les cookies AMCV existants. Pour activer la migration ECID, définissez le paramètre `idMigrationEnabled` dans la configuration. La migration des identifiants permet les cas d’utilisation suivants :

* Lorsque certaines pages d’un domaine utilisent l’API visiteur et d’autres utilisent ce SDK. Pour prendre en charge ce cas, le SDK lit les cookies AMCV existants et écrit un nouveau cookie avec l’ECID existant. En outre, le SDK écrit des cookies AMCV de sorte que si l’ECID est obtenu en premier sur une page instrumentée avec le SDK, les pages suivantes instrumentées avec l’API visiteur ont le même ECID.
* Lorsque le SDK Web Adobe Experience Platform est configuré sur une page qui comporte également l’API visiteur. Pour prendre en charge ce cas, si le cookie AMCV n’est pas défini, le SDK recherche l’API visiteur sur la page et l’appelle pour obtenir l’ECID.
* Lorsque l’ensemble du site utilise le SDK Web de Adobe Experience Platform et ne dispose pas d’API visiteur, il est utile de migrer les ECID afin de conserver les informations sur les visiteurs récurrents. Une fois le SDK déployé avec `idMigrationEnabled` pendant une période afin que la plupart des cookies de visiteur soient migrés, le paramètre peut être désactivé.

## Mise à jour des caractéristiques pour la migration

Lorsque des données au format XDM sont envoyées en Audience Manager, ces données doivent être converties en signaux lors de la migration. Vos caractéristiques devront être mises à jour pour prendre en compte les nouvelles clés fournies par XDM. Ce processus est plus facile en utilisant l’outil [BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) que l’Audience Manager a créé.

## Transfert côté serveur

Si le transfert côté serveur est actuellement activé et que vous utilisez `appmeasurement.js`. et `visitor.js` vous pouvez conserver la fonction de transfert côté serveur activée, ce qui ne posera aucun problème. Dans le serveur principal, Adobe récupère tous les segments AAM et les ajoute à l’appel à Analytics. Si l’appel à Analytics contient ces segments, Analytics n’appelle pas l’Audience Manager pour transférer aucune donnée. Il n’y a donc pas de collecte de données double. Il n’est pas non plus nécessaire d’avoir des conseils sur l’emplacement lors de l’utilisation du SDK Web, car les mêmes points de fin de segmentation sont appelés dans le serveur principal.

## Récupération de l’identifiant visiteur et de l’identifiant de région

Si vous souhaitez utiliser l’identifiant visiteur unique, utilisez la commande `getIdentity`. `getIdentity` renvoie l’ECID existant pour le visiteur actuel. Pour les nouveaux visiteurs qui n’ont pas encore d’ECID, cette commande génère un nouvel ECID. `getIdentity` renvoie également l’identifiant de région du visiteur. Pour plus d’informations, consultez le [Guide de l’utilisateur de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) .

>[!NOTE]
>
>Cette méthode est généralement utilisée avec les solutions personnalisées qui nécessitent la lecture de l’ID [!DNL Experience Cloud] ou qui ont besoin de l’indice d’emplacement Adobe Audience Manager. Elle n’est pas utilisée par une mise en œuvre standard.

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

## Synchronisation des identités

>[!NOTE]
>
>La méthode `syncIdentity` a été supprimée de la version 2.1.0, en plus de la fonction de hachage. Si vous utilisez la version 2.1.0+ et souhaitez synchroniser les identités, vous pouvez les envoyer directement dans l&#39;option `xdm` de la commande `sendEvent`, sous le champ `identityMap`.

En outre, la fonction [!DNL Identity Service] vous permet de synchroniser vos propres identifiants avec l’ECID à l’aide de la commande `syncIdentity`.

>[!NOTE]
>
>Il est vivement recommandé de transmettre toutes les identités disponibles sur chaque commande `sendEvent`. Cela permet de déverrouiller un certain nombre de cas d’utilisation, y compris la personnalisation. Maintenant que vous pouvez transmettre ces identités dans la commande `sendEvent`, elles peuvent être placées directement dans votre couche de données.

La synchronisation des identités vous permet d’identifier un appareil/utilisateur à l’aide de plusieurs identités, de définir leur état d’authentification et de décider quel identifiant est considéré comme le Principal. Si aucun identifiant n’a été défini sur `primary`, la Principale est par défaut `ECID`.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

Chaque propriété dans `identityMap` représente les identités appartenant à un [espace de noms d’identité](../../identity-service/namespaces.md) spécifique. Le nom de la propriété doit être le symbole d’espace de noms d’identité, que vous trouverez dans l’interface utilisateur de Adobe Experience Platform sous &quot;[!UICONTROL Identités]&quot;. La valeur de propriété doit être un tableau d’identités appartenant à cet espace de noms d’identité.

Chaque objet d’identité du tableau d’identités est structuré comme suit :

### `id`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

Il s’agit de l’identifiant que vous souhaitez synchroniser pour l’espace de noms donné.

### `authenticationState`

| **Type** | **Obligatoire** | **Valeur par défaut** | **Valeurs possibles** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Chaîne | Oui | ambigu | ambigu, authentifié et déconnecté |

L’état d’authentification de l’ID.

### `primary`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

Détermine si cette identité doit être utilisée comme Principal fragment dans le profil unifié. Par défaut, l’ECID est défini comme identifiant Principal de l’utilisateur.
