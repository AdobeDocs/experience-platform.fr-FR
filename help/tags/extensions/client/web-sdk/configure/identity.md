---
title: Paramètres de configuration des identités
description: Définissez la manière dont l’extension des balises identifie les visiteurs et visiteuses.
exl-id: 12e707f4-c37b-4c02-bfec-5ef7b98c2d3b
TQID: https://experienceleague.adobe.com/sCxtj-jtkPjm8vFKwbjyP-bl2nFPLNCFTdTp7E3XtqU
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 271
ht-degree: 11%

---

# Paramètres de configuration des identités {#identity}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_identity"
>title="Identité"
>abstract="Définissez la manière dont l’extension des balises identifie les visiteurs et visiteuses."

Cette section de configuration vous permet de définir le comportement de Web SDK en ce qui concerne la gestion de l’identification des utilisateurs.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Identity]** .

![Image montrant les paramètres d’identité de l’extension de balise Web SDK dans l’interface utilisateur des balises](../assets/web-sdk-ext-identity.png)

Les options disponibles sont les suivantes :

## [!UICONTROL Migrate ECID from VisitorAPI]

Case à cocher qui permet au SDK Web de lire les cookies `AMCV` et `s_ecid` et de définir le cookie `AMCV` utilisé par `Visitor.js`. Cette fonctionnalité est importante lors de la migration des bibliothèques qui utilisent `VisitorAPI.js` vers Web SDK, car certaines pages peuvent encore utiliser `Visitor.js`. Cette option permet au SDK de continuer à utiliser le même ECID, de sorte que les utilisateurs ne soient pas identifiés comme deux utilisateurs distincts. La bibliothèque JavaScript équivalente à cette case à cocher est [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md).

## [!UICONTROL Use third-party cookies]

Lorsque cette option est activée, Web SDK tente de stocker un identifiant utilisateur dans un cookie tiers. En cas de réussite, l’utilisateur est identifié comme un seul utilisateur lorsqu’il navigue sur plusieurs domaines, plutôt que comme un utilisateur distinct sur chaque domaine. Si cette option est activée, il se peut que le SDK ne puisse pas stocker l’identifiant de l’utilisateur dans un cookie tiers si le navigateur ne prend pas en charge les cookies tiers ou s’il a été configuré par l’utilisateur pour ne pas autoriser les cookies tiers. Dans ce cas, le SDK stocke uniquement l’identifiant dans le domaine propriétaire. La bibliothèque JavaScript équivalente à cette case à cocher est [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md).
