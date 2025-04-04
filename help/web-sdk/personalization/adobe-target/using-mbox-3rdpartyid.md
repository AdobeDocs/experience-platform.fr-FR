---
title: Synchronisation des profils en temps réel pour mbox3rdPartyId
description: Découvrez comment utiliser mbox3rdPartyId avec le SDK Web Adobe Experience Platform.
keywords: personnalisation;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# Qu’est-ce que `mbox3rdPartyId`

Le mbox3rdPartyId dans Adobe Target est l’identifiant visiteur de votre société. Il s’agit par exemple de l’identifiant d’abonnement pour le programme de fidélité de votre société.

Lorsqu’un visiteur se connecte au site d’une entreprise, l’entreprise crée généralement un identifiant lié au compte du visiteur, à la carte de fidélité, au numéro d’abonnement ou à d’autres identifiants applicables de cette entreprise. [En savoir plus](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)


## Utilisation de `mbox3rdPartyId` avec le SDK Web

### Étape 1 : configurer le `Target Third Party ID Namespace`

Configurez le `Target Third Party ID Namespace` dans votre [flux de données](../../../datastreams/overview.md) en utilisant l’espace de noms d’identifiant que vous souhaitez utiliser comme identifiant tiers de mbox.
[En savoir plus sur les espaces de noms d’ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

![Interface utilisateur d’Experience Platform affichant le champ Espace de noms de l’identifiant tiers cible.](assets/mbox3rdpartyid.png)

### Étape 2 : envoyer le `mbox3rdpartyId` à Target

Envoyez le `mbox3rdpartyId` à Target dans la commande `sendEvent`, à l’aide de l’espace de noms d’identifiant que vous avez configuré à l’étape 1.
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
