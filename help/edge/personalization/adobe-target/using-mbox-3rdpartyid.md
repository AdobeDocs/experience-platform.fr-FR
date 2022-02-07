---
title: Synchronisation des profils en temps réel pour mbox3rdPartyId
description: Découvrez comment utiliser mbox3rdPartyId avec le SDK Web de Adobe Experience Platform.
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
source-git-commit: 439f26177837e985ef95e972c3102cc2db37d539
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 9%

---


# En quoi consiste `mbox3rdPartyId`

mbox3rdPartyId dans Adobe Target correspond à l’identifiant visiteur de votre entreprise, tel que l’identifiant de membre pour le programme de fidélité de votre entreprise.

Lorsqu’un visiteur se connecte au site d’une entreprise, celle-ci crée généralement un identifiant lié au compte, à la carte de fidélité, au numéro de membre ou à tout autre identifiant applicable du visiteur pour cette entreprise. [En savoir plus](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## Utilisation `mbox3rdPartyId` avec le SDK Web

### Étape 1 : Configurez la variable `Target Third Party ID Namespace`

Configurez la variable `Target Third Party ID Namespace` dans votre [Datastream](../../fundamentals/datastreams.md), à l’aide de l’espace de noms d’ID que vous souhaitez utiliser comme identifiant tiers mbox.
[En savoir plus sur les espaces de noms d’ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

![](assets/mbox3rdpartyid.png)

### Étape 2 : Envoyez la variable `mbox3rdpartyId` vers Target

Envoyez la variable `mbox3rdpartyId` à Target dans le `sendEvent` à l’aide de l’espace de noms d’ID que vous avez configuré à l’étape 1.
[En savoir plus sur l’envoi d’identifiants](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```


