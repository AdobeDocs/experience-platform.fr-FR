---
title: Synchronisation des profils en temps réel pour mbox3rdPartyId
description: Découvrez comment utiliser mbox3rdPartyId avec le SDK Web de Adobe Experience Platform.
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 5%

---

# Présentation `mbox3rdPartyId`

mbox3rdPartyId dans Adobe Target est l’identifiant visiteur de votre entreprise, tel que l’identifiant d’adhésion au programme de fidélité de votre entreprise.

Lorsqu’un visiteur se connecte au site d’une entreprise, celle-ci crée généralement un ID lié au compte, à la carte de fidélité, au numéro de membre ou à tout autre identifiant applicable du visiteur pour cette entreprise. [En savoir plus](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## Utilisation `mbox3rdPartyId` avec le SDK Web

### Etape 1 : configurer la variable `Target Third Party ID Namespace`

Configurez la variable `Target Third Party ID Namespace` dans votre [Datastream](../../../datastreams/overview.md), à l’aide de l’espace de noms d’ID que vous souhaitez utiliser comme identifiant tiers mbox.
[En savoir plus sur les espaces de noms d’ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

![L’interface utilisateur de Platform affiche le champ Espace de noms de l’identifiant tiers Target .](assets/mbox3rdpartyid.png)

### Étape 2 : envoyez la variable `mbox3rdpartyId` vers Target

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
