---
title: Récupération de l'ID d'Experience Cloud
seo-title: Adobe Experience Platform Web SDK Récupération de l’ID d’Experience Cloud
description: Découvrez comment obtenir l’identifiant Adobe Experience Cloud.
seo-description: Découvrez comment obtenir l’identifiant Adobe Experience Cloud.
keywords: Identity;First Party Identity;Identity Service;3rd Party Identity;ID Migration;Visitor ID;third party identity;thirdPartyCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;syncIdentity;sendEvent;identityMap;primary;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: d069b3007265406367ca9de2b85540b2a070cf36
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 6%

---


# Identité - Récupération de l&#39;ID d&#39;Experience Cloud

Le Adobe Experience Platform [!DNL Web SDK] tire parti du service [d&#39;identité](../../identity-service/ecid.md)Adobe. Ainsi, chaque périphérique dispose d’un identifiant unique qui est conservé sur le périphérique, de sorte que l’activité entre les pages puisse être liée ensemble.

## Identité de premier niveau

L’ [!DNL Identity Service] utilisateur stocke l’identité dans un cookie dans un domaine propriétaire. Le cookie [!DNL Identity Service] tente de le définir à l’aide d’un en-tête HTTP sur le domaine. Si cela échoue, la [!DNL Identity Service] fonction revient à définir des cookies via Javascript. Adobe vous recommande de configurer un CNAME pour vous assurer que vos cookies ne seront pas plafonnés par les restrictions ITP côté client.

## Identité tierce

Il [!DNL Identity Service] peut synchroniser un identifiant avec un domaine tiers (demdex.net) pour activer le suivi sur plusieurs sites. Lorsque cette option est activée, la première demande d’un visiteur (par exemple, une personne sans ECID) sera envoyée à demdex.net. Cela ne sera fait que sur les navigateurs qui l’autorisent (Chrome, par exemple) et qui est contrôlé par le `thirdPartyCookiesEnabled` paramètre de la configuration. Si vous souhaitez désactiver cette fonctionnalité ensemble, définissez la valeur `thirdPartyCookiesEnabled` sur false.

## Migration des identifiants

Lors de la migration à partir de l’API du Visiteur, vous pouvez également migrer les cookies AMCV existants. Pour activer la migration ECID, définissez le `idMigrationEnabled` paramètre dans la configuration. La migration des identifiants est configurée pour activer certains cas d’utilisation :

* Lorsque certaines pages d’un domaine utilisent l’API du Visiteur et que d’autres pages utilisent ce SDK. Pour prendre en charge ce cas, le SDK lit les cookies AMCV existants et écrit un nouveau cookie avec l’ECID existant. En outre, le SDK écrit des cookies AMCV de sorte que si l’ECID est obtenu en premier sur une page instrumentée avec le SDK Web AEP, les pages suivantes instrumentées avec l’API Visiteur ont le même ECID.
* Lorsque le SDK Web AEP est configuré sur une page qui comporte également une API de Visiteur. Pour prendre en charge ce cas, si le cookie AMCV n’est pas défini, le SDK recherche l’API du Visiteur sur la page et l’appelle pour obtenir l’ECID.
* Lorsque le site entier utilise le SDK Web AEP et ne dispose pas d’API de Visiteur, il est utile de migrer les ECID pour que les informations de visiteur de retour soient conservées. Une fois le SDK déployé `idMigrationEnabled` pendant un certain temps afin que la plupart des cookies visiteurs soient migrés, le paramètre peut être désactivé.

## Récupération de l’ID de Visiteur

Si vous souhaitez utiliser cet identifiant unique, utilisez la `getIdentity` commande. `getIdentity` renvoie l&#39;ECID existant pour le visiteur actuel. Pour les nouveaux visiteurs qui n&#39;ont pas encore d&#39;ECID, cette commande génère un nouvel ECID.

>[!NOTE]
>
>This method is typically used with custom solutions that require reading the [!DNL Experience Cloud] ID. Elle n’est pas utilisée par une mise en œuvre standard.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## Synchronisation des identités

>[!NOTE]
>
>La `syncIdentity` méthode a été supprimée dans la version 2.1.0, en plus de la fonction de hachage. Si vous utilisez la version 2.1.0+ et souhaitez synchroniser les identités, vous pouvez les envoyer directement dans l&#39; `xdm` option de la `sendEvent` commande, sous le `identityMap` champ.

En outre, la [!DNL Identity Service] permet de synchroniser vos propres identifiants avec l&#39;ECID à l&#39;aide de la `syncIdentity` commande.

>[!NOTE]
>
>Il est vivement recommandé de transmettre toutes les identités disponibles à chaque `sendEvent` commande. Cette opération permet de déverrouiller une gamme de cas d’utilisation, y compris la personnalisation. Maintenant que vous pouvez transmettre ces identités dans la `sendEvent` commande, elles peuvent être placées directement dans votre couche de données.

La synchronisation des identités vous permet d&#39;identifier un périphérique/utilisateur à l&#39;aide de plusieurs identités, de définir leur état d&#39;authentification et de décider quel identifiant est considéré comme Principal. Si aucun identifiant n’a été défini comme `primary`, la valeur par défaut de l’identifiant Principal est `ECID`.

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
})
```


### Options de synchronisation des identités

#### Symbole de l&#39;espace de nommage d&#39;identité

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

La clé de l&#39;objet est le symbole [d&#39;Espace de nommage](../../identity-service/namespaces.md) d&#39;identité. Vous trouverez cette liste dans l’interface utilisateur de Adobe Experience Platform sous &quot;[!UICONTROL Identités]&quot;.

#### `id`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

Il s’agit de l’identifiant que vous souhaitez synchroniser pour l’espace de nommage donné.

#### `authenticationState`

| **Type** | **Obligatoire** | **Valeur par défaut** | **Valeurs possibles** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Chaîne | Oui | ambigu | ambigu, authentifié et déconnecté |

État d’authentification de l’ID.

#### `primary`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

Détermine si cette identité doit être utilisée comme Principal fragment dans le profil unifié. Par défaut, l’ECID est défini comme identifiant Principal de l’utilisateur.

#### `hashEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

S&#39;il est activé, il hachera l&#39;identité à l&#39;aide du hachage SHA256.
