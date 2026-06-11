---
title: datastreamId
description: Déterminez l’identifiant du flux de données auquel vous souhaitez envoyer des données.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
TQID: https://experienceleague.adobe.com/mKVKjTc3GpTx-AYw54rFETXaFRRoGA0l5EYtqy-UtBw
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 221
ht-degree: 0%

---

# `datastreamId`

La propriété `datastreamId` est une chaîne qui détermine le [flux de données](/help/datastreams/overview.md) dans Adobe Experience Platform auquel vous souhaitez envoyer des données. Cette propriété est requise lors de l’envoi de données à Adobe. Les versions 2.20.0 ou antérieures de Web SDK utilisent `edgeConfigId` à la place.

Pour localiser un identifiant de flux de données :

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Flux de données]**.
1. Utilisez le champ de recherche pour localiser le flux de données de votre choix, puis sélectionnez **[!UICONTROL Copier]** ![Copier](../../assets/copy.png) en regard de l’identifiant du flux de données.

Vous pouvez également sélectionner le nom du flux de données de votre choix et l’identifiant du flux de données s’affiche dans la colonne de droite pour que vous puissiez le copier.

## Exemple de code

Définissez la propriété de chaîne `datastreamID` lors de l’exécution de la commande `configure`. Cette propriété est requise pour toutes les implémentations de Web SDK. Si vous omettez cette propriété, le SDK Web ne sait pas à quel flux de données envoyer des données, ce qui entraîne la perte définitive de ces données.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Si vous configurez plusieurs instances de Web SDK sur une seule page, vous devez configurer un `datastreamId` différent pour chaque instance.

## Sélectionnez l’identifiant du flux de données à l’aide de l’extension de balise Web SDK

Consultez [ Paramètres de configuration des flux de données ](/help/tags/extensions/client/web-sdk/configure/datastreams.md) dans la documentation de l’extension de balise Web SDK pour savoir comment définir le flux de données souhaité pour chaque environnement à l’aide de balises. Vous pouvez envoyer des données à différents flux de données pour les environnements de balises de production, d’évaluation et de développement.
