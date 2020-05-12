---
title: Récupération de l’ID Experience Cloud
seo-title: Adobe Experience Platform Web SDK Récupération de l’ID Experience Cloud
description: Découvrez comment obtenir l’ID Adobe Experience Cloud.
seo-description: Découvrez comment obtenir l’ID Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: 9bd6feb767e39911097bbe15eb2c370d61d9842a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 12%

---


# (bêta) Récupération de l’ID Experience Cloud

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Le SDK Web d’Adobe Experience Platform tire parti d’ [Adobe Identity Service](../../identity-service/ecid.md). Ainsi, chaque périphérique dispose d’un identifiant unique qui est conservé sur le périphérique, de sorte que l’activité entre les pages puisse être liée ensemble.

## Identité de premier niveau

Le service d’ID stocke l’identité dans un cookie dans un domaine propriétaire. Le service d’ID tente de définir le cookie à l’aide d’un en-tête HTTP sur le domaine si le service d’ID échoue, puis revient à définir les cookies par le biais de JavaScript. Adobe recommande de configurer un CNAME afin que vos cookies ne soient pas plafonnés par les restrictions ITP côté client.

## Identité tierce

Les services d’ID peuvent synchroniser un identifiant avec un domaine tiers (demdex.net) pour activer le suivi sur l’ensemble du site. Lorsque cette option est activée, la première demande d’un visiteur (par exemple, une personne sans ECID) sera envoyée à demdex.net. Cela ne sera fait que sur les navigateurs qui l’autorisent (Chrome, par exemple) et qui est contrôlé par le `thirdPartyCookiesEnabled` paramètre de la configuration. Si vous souhaitez désactiver cette fonctionnalité, définissez l’ensemble `thirdPartyCookiesEnabled` sur false.

## Récupération de l’ID de Visiteur

Si vous souhaitez utiliser cet identifiant unique, utilisez la `getIdentity` commande. `getIdentity` renvoie l&#39;ECID existant pour le visiteur actuel. Pour les nouveaux visiteurs qui n&#39;ont pas encore d&#39;ECID, cette commande génère un nouvel ECID.

>[!NOTE]
>
>Cette méthode est généralement utilisée avec les solutions personnalisées qui nécessitent la lecture de l’ID Experience Cloud. Il n’est pas utilisé par une mise en oeuvre standard.

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

De plus, Identity Service vous permet de synchroniser vos propres identifiants avec l&#39;ECID à l&#39;aide de la `syncIdentity` commande.

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### Options de synchronisation des identités

#### Symbole d&#39;Espace de nommage d&#39;identité

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

La clé de l&#39;objet est le symbole [d&#39;Espace de nommage](../../identity-service/namespaces.md) d&#39;identité. Cette liste figure dans l’interface utilisateur d’Adobe Experience Platform sous Identités.

#### `id`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

Il s’agit de l’identifiant que vous souhaitez synchroniser pour l’espace de nommage donné.

#### `primary`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

Cette identité doit-elle être utilisée comme fragment principal dans le profil unifié ? Par défaut, l’ECID est défini comme identifiant principal de l’utilisateur.

#### `hashEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

S&#39;il est activé, il hachera l&#39;identité à l&#39;aide du hachage SHA256.