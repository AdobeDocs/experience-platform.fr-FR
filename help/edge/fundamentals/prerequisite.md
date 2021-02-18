---
title: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
description: Découvrez les conditions préalables à l’utilisation du SDK Web de Adobe Experience Platform.
keywords: Domaine propriétaire ; CNAME ; schéma ; créer un schéma ; lancement ; extension sdk web aep ; extension ; id de configuration ; outil de configuration ; élément de données ; créer un élément de données ; objet XDM ; sendEvent ; envoyer le Événement ;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 2%

---


# Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform

Pour utiliser le SDK Web de la plate-forme, vous devez d’abord :

- Demandez à votre organisation de configurer cette fonctionnalité. (L&#39;accès au SDK Web de la plate-forme est gratuit. Si vous souhaitez y accéder, contactez votre responsable de succès client (CSM).
- Vous devez disposer d’un domaine propriétaire (CNAME) activé. Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous devez l’utiliser. Les tests en cours de développement fonctionnent sans CNAME, mais vous en avez besoin avant de commencer la production.

>[!IMPORTANT]
>
>**Notez qu’à compter du 10/11/20, les mises en oeuvre CNAME propriétaires expirent à 7 jours sur tous les navigateurs Safari et les périphériques iOS mobiles.**

- Avoir droit à Adobe Experience Platform. Si vous n&#39;avez pas acheté Adobe Experience Platform, l&#39;Adobe vous donnera l&#39;accès nécessaire à une utilisation limitée avec le SDK sans frais supplémentaires.
- Si votre site Web utilise déjà le [service d’identification des Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) de votre site Web (via l’API du Visiteur ou l’extension du service d’identification des Experience Cloud dans Adobe Experience Platform Launch) et que vous souhaitez continuer à l’utiliser lors de la migration vers Adobe Experience Platform Web SDK, vous devez utiliser la dernière version de l’API du Visiteur ou l’extension du service d’identification des Experience Cloud. Voir [Migration des identifiants](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) pour plus d’informations.
