---
title: idMigrationEnabled
description: Permet au SDK Web de lire les cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# `idMigrationEnabled`

La propriété `idMigrationEnabled` permet au SDK Web de lire les cookies AMCV définis par les implémentations Adobe Experience Cloud précédentes. Si votre entreprise met à niveau votre implémentation vers Web SDK, ce paramètre permet une transition plus fluide vers le service Adobe Experience Cloud ID actuel. Ce paramètre est utile pour éviter une forte augmentation du nombre de visiteurs uniques lors de la mise à niveau vers le SDK web.

Si votre organisation exécute une nouvelle implémentation de Web SDK, l’activation de ce paramètre n’a aucun impact sur la collecte de données ou l’identification des visiteurs. Il n’y a aucun inconvénient à ce qu’il soit activé pour toutes les implémentations.

Définissez la valeur booléenne `idMigrationEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, elle est définie par défaut sur `true`. Définissez cette propriété si vous souhaitez désactiver la possibilité de lire les cookies AMCV définis par l’API visiteur. La plupart des organisations n’ont pas besoin de définir cette propriété.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Activer la migration des identifiants visiteur à l’aide de l’extension de balise Web SDK

Ces paramètres peuvent être configurés dans l’extension de balise Web SDK à l’aide des [ Paramètres de configuration des identités ](/help/tags/extensions/client/web-sdk/configure/identity.md).
