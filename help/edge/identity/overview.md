---
title: Récupération d’ID d’Experience Cloud à l’aide du SDK Web Adobe Experience Platform
description: Découvrez comment récupérer des identifiants Adobe Experience Cloud (ECID) à l’aide du kit de développement Web Adobe Experience Platform.
seo-description: Découvrez comment obtenir l’identifiant Adobe Experience Cloud.
keywords: Identité ; Identité propriétaire ; Service d'identité ; Identité tierce ; Migration d'identifiants ; Identifiant Visiteur ; Identité tierce ; Cookies tiersEnabled ; idMigrationEnabled ; getIdentity ; Identité de synchronisation ; Identité de synchronisation ; IdentitéSynchronisée ; EnvoiEvent ; IdentitéMap ; Principal ; Identité Espace de nommage ; Identifiant espace de nommage ; AuthentificationState ; HashEnabled ;
translation-type: tm+mt
source-git-commit: 882bcd2f9aa7a104270865783eed82089862dea3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 3%

---


# Récupération des identifiants Adobe Experience Cloud

Adobe Experience Platform Web SDK exploite [Adobe Identity Service](../../identity-service/ecid.md). Ainsi, chaque périphérique dispose d’un identifiant unique qui est conservé sur le périphérique, de sorte que l’activité entre les pages puisse être liée ensemble.

## Identité de premier niveau

[!DNL Identity Service] stocke l&#39;identité dans un cookie dans un domaine propriétaire. [!DNL Identity Service] tente de définir le cookie à l’aide d’un en-tête HTTP sur le domaine. Si cela échoue, le [!DNL Identity Service] revient à définir des cookies via Javascript. Adobe vous recommande de configurer un CNAME pour vous assurer que vos cookies ne seront pas plafonnés par les restrictions ITP côté client.

## Identité tierce

[!DNL Identity Service] permet de synchroniser un identifiant avec un domaine tiers (demdex.net) pour activer le suivi sur plusieurs sites. Lorsque cette option est activée, la première requête d’un visiteur (par exemple, une personne sans ECID) est envoyée à demdex.net. Cette opération ne sera effectuée que sur les navigateurs qui l’autorisent (tels que Chrome) et est contrôlée par le paramètre `thirdPartyCookiesEnabled` dans la configuration. Si vous souhaitez désactiver cette fonctionnalité ensemble, définissez `thirdPartyCookiesEnabled` sur false.

## Migration des identifiants

Lors de la migration à partir de l’API du Visiteur, vous pouvez également migrer les cookies AMCV existants. Pour activer la migration ECID, définissez le paramètre `idMigrationEnabled` dans la configuration. La migration des identifiants permet les cas d’utilisation suivants :

* Lorsque certaines pages d’un domaine utilisent l’API du Visiteur et que d’autres pages utilisent ce SDK. Pour prendre en charge ce cas, le SDK lit les cookies AMCV existants et écrit un nouveau cookie avec l’ECID existant. En outre, le SDK écrit des cookies AMCV de sorte que si l’ECID est obtenu en premier sur une page instrumentée avec le SDK, les pages suivantes instrumentées avec l’API du Visiteur ont le même ECID.
* Lorsque le SDK Web Adobe Experience Platform est configuré sur une page qui comporte également une API Visiteur. Pour prendre en charge ce cas, si le cookie AMCV n’est pas défini, le SDK recherche l’API du Visiteur sur la page et l’appelle pour obtenir l’ECID.
* Lorsque le site entier utilise le SDK Web de Adobe Experience Platform et ne dispose pas d’API de Visiteur, il est utile de migrer les ECID afin que les informations du visiteur de retour soient conservées. Une fois le SDK déployé avec `idMigrationEnabled` pendant un certain temps afin que la plupart des cookies de visiteur soient migrés, le paramètre peut être désactivé.

## Mise à jour des caractéristiques pour la migration

Lorsque des données au format XDM sont envoyées en Audience Manager, ces données doivent être converties en signaux lors de la migration. Vos caractéristiques devront être mises à jour pour refléter les nouvelles clés fournies par XDM. Ce processus est facilité en utilisant l&#39;outil [BAAAM](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) que l&#39;Audience Manager a créé.

## Transfert côté serveur

Si le transfert côté serveur est actuellement activé et que vous utilisez `appmeasurement.js`. et `visitor.js` vous pouvez conserver la fonction de transfert côté serveur activée, ce qui ne provoquera aucun problème. Dans le serveur principal, l’Adobe récupère les segments AAM et les ajoute à l’appel à Analytics. Si l’appel à Analytics contient ces segments, Analytics n’appelle aucune Audience Manager pour transférer des données. Il n’y a donc aucune collecte de données de doublon. Il n’est pas non plus nécessaire d’avoir des conseils sur l’emplacement lors de l’utilisation du SDK Web, car les mêmes points de terminaison de segmentation sont appelés dans le serveur principal.

## Récupération de l’ID de visiteur et de l’ID de région

Si vous souhaitez utiliser l&#39;identifiant de visiteur unique, utilisez la commande `getIdentity`. `getIdentity` renvoie l&#39;ECID existant pour le visiteur actuel. Pour les nouveaux visiteurs qui n&#39;ont pas encore d&#39;ECID, cette commande génère un nouvel ECID. `getIdentity` renvoie également l’identifiant de région du visiteur. Pour plus d’informations, consultez le [Guide de l’utilisateur de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html).

>[!NOTE]
>
>Cette méthode est généralement utilisée avec les solutions personnalisées qui nécessitent la lecture de l&#39;ID [!DNL Experience Cloud] ou l&#39;indication d&#39;emplacement Adobe Audience Manager. Elle n’est pas utilisée par une mise en œuvre standard.

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
>La méthode `syncIdentity` a été supprimée dans la version 2.1.0, en plus de la fonction de hachage. Si vous utilisez la version 2.1.0+ et souhaitez synchroniser les identités, vous pouvez les envoyer directement dans l&#39;option `xdm` de la commande `sendEvent`, sous le champ `identityMap`.

De plus, la commande [!DNL Identity Service] vous permet de synchroniser vos propres identifiants avec l&#39;ECID à l&#39;aide de la commande `syncIdentity`.

>[!NOTE]
>
>Il est vivement recommandé de transmettre toutes les identités disponibles à chaque commande `sendEvent`. Cette opération permet de déverrouiller une gamme de cas d’utilisation, y compris la personnalisation. Maintenant que vous pouvez transmettre ces identités dans la commande `sendEvent`, elles peuvent être placées directement dans votre couche de données.

La synchronisation des identités vous permet d&#39;identifier un périphérique/utilisateur à l&#39;aide de plusieurs identités, de définir leur état d&#39;authentification et de décider quel identifiant est considéré comme Principal. Si aucun identifiant n&#39;a été défini comme `primary`, la valeur par défaut Principale est `ECID`.

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

Chaque propriété dans `identityMap` représente des identités appartenant à un [espace de nommage d&#39;identité ](../../identity-service/namespaces.md) particulier. Le nom de la propriété doit être le symbole de l&#39;espace de nommage d&#39;identité, que vous trouverez dans l&#39;interface utilisateur de Adobe Experience Platform sous &quot;[!UICONTROL Identities]&quot;. La valeur de propriété doit être un tableau d&#39;identités appartenant à cet espace de nommage d&#39;identité.

Chaque objet d&#39;identité du tableau identités est structuré comme suit :

### `id`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

Il s’agit de l’identifiant que vous souhaitez synchroniser pour l’espace de nommage donné.

### `authenticationState`

| **Type** | **Obligatoire** | **Valeur par défaut** | **Valeurs possibles** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Chaîne | Oui | ambigu | ambigu, authentifié et déconnecté |

État d’authentification de l’ID.

### `primary`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

Détermine si cette identité doit être utilisée comme Principal fragment dans le profil unifié. Par défaut, l’ECID est défini comme identifiant Principal de l’utilisateur.
