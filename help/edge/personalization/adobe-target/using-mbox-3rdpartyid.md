---
title: Synchronisation des profils en temps réel pour mbox3rdPartyId
description: Découvrez comment utiliser mbox3rdPartyId avec le SDK Web de Adobe Experience Platform.
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 30%

---

# En quoi consiste `mbox3rdPartyId`

mbox3rdPartyId dans Adobe Target est l’identifiant visiteur de votre entreprise, tel que l’identifiant d’adhésion au programme de fidélité de votre entreprise.

Lorsqu’un visiteur se connecte au site de votre entreprise, cette dernière crée généralement un identifiant qui est associé au compte du visiteur, à sa carte de fidélité, à son numéro de membre ou à tout autre identifiant applicable de l’entreprise. [En savoir plus](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#).


## Utilisation `mbox3rdPartyId` avec le SDK Web

### Étape 1 : Configurez la variable `Target Third Party ID Namespace`

Configurez la variable `Target Third Party ID Namespace` dans votre [Datastream](../../../datastreams/overview.md), à l’aide de l’espace de noms d’ID que vous souhaitez utiliser comme identifiant tiers mbox.
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
