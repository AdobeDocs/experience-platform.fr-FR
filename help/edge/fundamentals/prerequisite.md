---
title: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
seo-title: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
description: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
seo-description: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform

Pour utiliser ce SDK, vous devez d’abord :

- Configurez votre organisation pour cette fonction. (Si vous souhaitez prendre part à la liste d’attente, contactez votre responsable de succès client (CSM).
- Vous devez disposer d’un domaine propriétaire (CNAME) activé. Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous devez l’utiliser. Les tests en cours de développement fonctionnent sans CNAME, mais vous en avez besoin avant de commencer la production.

>[!IMPORTANT]
>
>**Notez qu’à compter du 10/11/20, les mises en oeuvre CNAME propriétaires expirent à 7 jours sur tous les navigateurs Safari et les périphériques iOS mobiles.**

- Avoir droit à Adobe Experience Platform. Si vous n’avez pas acheté Adobe Experience Platform, l’Adobe vous fournira la Fondation Data Services Experience Platform pour une utilisation limitée avec le SDK sans frais supplémentaires.
- Si votre site Web utilise déjà le [service d’identification des Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) de votre site Web (via l’API du Visiteur ou l’extension du service d’identification des Experience Cloud dans Adobe Experience Platform Launch) et que vous souhaitez continuer à l’utiliser lors de la migration vers Adobe Experience Platform Web SDK, vous devez utiliser la dernière version de l’API du Visiteur ou l’extension du service d’identification des Experience Cloud. Voir [Migration des identifiants](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) pour plus d’informations.
