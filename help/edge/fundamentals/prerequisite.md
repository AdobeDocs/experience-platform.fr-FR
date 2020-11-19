---
title: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
seo-title: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
description: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
seo-description: Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: a0ede8c7d3088fe80d6ea014b4a4f9f08ee8a7aa
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# Conditions préalables à l’utilisation du SDK Web Adobe Experience Platform

Pour utiliser ce SDK, vous devez d’abord :

- Configurez votre organisation pour cette fonction. (Si vous souhaitez vous rendre sur la liste d&#39;attente, contactez votre responsable logiciel certifié (CSM)).
- Vous devez disposer d’un domaine propriétaire (CNAME) activé. Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous devez l’utiliser. Les tests en cours de développement fonctionnent sans CNAME, mais vous en avez besoin avant de commencer la production.

>[!IMPORTANT]
>
>**Notez qu’à compter du 10/11/20, les mises en oeuvre CNAME propriétaires expirent à 7 jours sur tous les navigateurs Safari et les périphériques iOS mobiles.**

- Avoir droit à Adobe Experience Platform. Si vous n’avez pas acheté Adobe Experience Platform, l’Adobe vous fournira la Fondation Data Services Experience Platform pour une utilisation limitée avec le SDK sans frais supplémentaires.
- Si votre site Web utilise déjà le service [d’identification des](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) Experience Cloud sur votre site Web (via l’API du Visiteur ou l’extension du service d’identification des Experience Cloud dans Adobe Experience Platform Launch) et que vous souhaitez continuer à l’utiliser lors de la migration vers Adobe Experience Platform Web SDK, vous devez utiliser la dernière version de l’API du Visiteur ou l’extension du service d’identification des Experience Cloud. Pour plus d’informations, voir Migration [des](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) identifiants.
