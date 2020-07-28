---
title: Récupération de l'ID d'Experience Cloud
seo-title: Adobe Experience Platform du SDK Web Récupération de l'ID d'Experience Cloud
description: Découvrez comment obtenir l’identifiant Adobe Experience Cloud.
seo-description: Découvrez comment obtenir l’identifiant Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 10%

---


# Identité - Récupération de l&#39;ID d&#39;Experience Cloud

L&#39;Adobe Experience Platform [!DNL Web SDK] tire parti du service [d&#39;identité](../../identity-service/ecid.md)Adobe. Ainsi, chaque périphérique dispose d’un identifiant unique qui est conservé sur le périphérique, de sorte que l’activité entre les pages puisse être liée ensemble.

## Identité de premier niveau

L’ [!DNL Identity Service] utilisateur stocke l’identité dans un cookie dans un domaine propriétaire. Le cookie [!DNL Identity Service] tente de le définir à l’aide d’un en-tête HTTP sur le domaine. Si cela échoue, la [!DNL Identity Service] fonction revient à définir des cookies via Javascript. Adobe vous recommande de configurer un CNAME pour vous assurer que vos cookies ne seront pas plafonnés par les restrictions ITP côté client.

## Identité tierce

Il [!DNL Identity Service] peut synchroniser un identifiant avec un domaine tiers (demdex.net) pour activer le suivi sur plusieurs sites. Lorsque cette option est activée, la première demande d’un visiteur (par exemple, une personne sans ECID) sera envoyée à demdex.net. Cela ne sera fait que sur les navigateurs qui l’autorisent (Chrome, par exemple) et qui est contrôlé par le `thirdPartyCookiesEnabled` paramètre de la configuration. Si vous souhaitez désactiver cette fonctionnalité ensemble, définissez la valeur `thirdPartyCookiesEnabled` sur false.

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

En outre, la [!DNL Identity Service] permet de synchroniser vos propres identifiants avec l&#39;ECID à l&#39;aide de la `syncIdentity` commande.

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

La clé de l&#39;objet est le symbole [d&#39;Espace de nommage](../../identity-service/namespaces.md) d&#39;identité. Cette liste figure dans l’interface utilisateur de l’Adobe Experience Platform sous [!UICONTROL Identités].

#### `id`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Chaîne | Oui | Aucune |

Il s’agit de l’identifiant que vous souhaitez synchroniser pour l’espace de nommage donné.

#### `authenticationState`

| **Type** | **Obligatoire** | **Valeur par défaut** | **Valeurs possibles** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Chaîne | Oui | ambigu | ambigu, authentifié et déconnecté |

Etat d’authentification de l’ID.

#### `primary`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

Détermine si cette identité doit être utilisée comme fragment principal dans le profil unifié. Par défaut, l’ECID est défini comme identifiant principal de l’utilisateur.

#### `hashEnabled`

| **Type** | **Obligatoire** | **Valeur par défaut** |
| -------- | ------------ | ----------------- |
| Booléen | facultatif | false |

S&#39;il est activé, il hachera l&#39;identité à l&#39;aide du hachage SHA256.
