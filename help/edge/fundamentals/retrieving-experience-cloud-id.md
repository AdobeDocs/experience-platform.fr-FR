---
title: Récupération de l’ID Experience Cloud
seo-title: Adobe Experience Platform Web SDK Récupération de l’ID Experience Cloud
description: Découvrez comment obtenir l’ID Adobe Experience Cloud.
seo-description: Découvrez comment obtenir l’ID Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 19%

---


# (bêta) Récupération de l’ID Experience Cloud

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Adobe Experience Cloud utilise un identifiant unique pour chaque client. Si vous souhaitez utiliser cet identifiant unique, utilisez la `getIdentity` commande. `getIdentity` renvoie l&#39;ECID existant pour le visiteur actuel. Pour les nouveaux visiteurs qui n&#39;ont pas encore d&#39;ECID, cette commande génère un nouvel ECID.

>[!NOTE]
>
>Cette méthode est généralement utilisée avec les solutions personnalisées qui nécessitent la lecture de l’ID Experience Cloud. Il n’est pas utilisé par une mise en oeuvre standard.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
