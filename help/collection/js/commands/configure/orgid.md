---
title: orgId
description: La propriété orgId est une chaîne qui indique à Adobe à quelle organisation ces données sont envoyées.
exl-id: 0e04e85a-800c-4927-a165-80a5a578f4c2
TQID: https://experienceleague.adobe.com/7KRreqDcqK-Jpj2MB3AMUXkkvpcqD40pID3tyjEif4A
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 191
ht-degree: 1%

---

# `orgId`

La propriété `orgId` est une chaîne qui indique à Adobe à quelle organisation les données sont envoyées. **Cette propriété est requise pour toutes les données envoyées à l’aide de Web SDK.**

Pour localiser votre `orgID` :

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Où que vous soyez dans Adobe Experience Cloud, appuyez sur **`[Ctrl]`** + **`[I]`**. Une fenêtre [!UICONTROL Débogueur de données utilisateur] s’ouvre.
1. Cliquez sur **[!UICONTROL Copier]** ![Copier](../../assets/copy.png) en regard de l’[!UICONTROL ID d’organisation actuel] ou cliquez sur l’onglet **[!UICONTROL Organisations affectées]** pour afficher d’autres ID d’organisation auxquels vous pouvez accéder.
1. Lorsque vous avez terminé de localiser les informations souhaitées, cliquez sur **[!UICONTROL Fermer]**.

Les identifiants d’organisation sont toujours des chaînes alphanumériques de 24 caractères et se terminent toujours par `@AdobeOrg`.

Définissez la chaîne de `orgId` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, Web SDK renvoie une erreur de console et les données ne sont pas envoyées à Adobe.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

## Définir l’ID d’organisation à l’aide de l’extension de balise Web SDK

Ce paramètre peut être configuré dans l’extension de balise Web SDK à l’aide des paramètres de configuration de l’instance SDK [](/help/tags/extensions/client/web-sdk/configure/general.md). Le champ est automatiquement renseigné en fonction de l’organisation sous laquelle la propriété de balise a été créée.
