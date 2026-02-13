---
title: Paramètres de configuration des identités
description: Définissez la manière dont l’extension de balise identifie les visiteurs.
exl-id: 12e707f4-c37b-4c02-bfec-5ef7b98c2d3b
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 3%

---

# Paramètres de configuration des identités {#identity}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_identity"
>title="Identité"
>abstract="Définissez la manière dont l’extension de balise identifie les visiteurs."

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

>[!IMPORTANT]
>
>Les cookies tiers ne sont pas compatibles avec la fonctionnalité [Identifiant d’appareil interne](/help/collection/use-cases/identity/first-party-device-ids.md) de Web SDK. Vous pouvez utiliser des identifiants d’appareil propriétaires ou des cookies tiers ; vous ne pouvez pas utiliser les deux fonctionnalités simultanément.
