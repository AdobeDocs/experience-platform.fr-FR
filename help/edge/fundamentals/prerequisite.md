---
title: Conditions préalables requises pour l’utilisation du SDK Web de Adobe Experience Platform
description: Découvrez les conditions préalables requises pour utiliser le SDK Web de Adobe Experience Platform.
keywords: Domaine propriétaire;CNAME;schéma;créer un schéma;launch;extension du sdk web aep;extension;ID de configuration;outil de configuration;élément de données;créer un élément de données;objet XDM;sendEvent;envoyer un événement;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 4%

---

# Conditions préalables requises pour l’utilisation du SDK Web de Adobe Experience Platform

Pour utiliser le SDK Web de Adobe Experience Platform, vous devez d’abord :

- disposer des autorisations appropriées configurées pour les utilisateurs de votre entreprise ; Tous les clients Experience Cloud ont accès aux outils de collecte de données. Chaque utilisateur de votre entreprise n’aura besoin que d’autorisations pour les schémas, les identités et les flux de données. Pour en savoir plus sur la configuration de ces autorisations, consultez notre documentation sur [gestion des autorisations de collecte de données](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=fr).
- Il est recommandé d’activer le domaine propriétaire (CNAME). Si vous disposez déjà d’un CNAME pour Adobe Analytics, vous devez l’utiliser. Le test en développement fonctionne sans CNAME, mais Adobe recommande d’en avoir un avant de passer en production. Bien qu’une mise en oeuvre CNAME ne fournisse aucun avantage en termes de durée de vie des cookies, elle peut empêcher certains bloqueurs d’annonces et navigateurs moins courants de bloquer les demandes de SDK. Dans ce cas, l’utilisation d’un CNAME peut empêcher que votre collecte de données ne soit interrompue pour les utilisateurs qui utilisent ces outils.

>[!IMPORTANT]
>
>**Notez qu’à compter du 11/10/20, les mises en oeuvre CNAME propriétaires expirent de 7 jours sur tous les navigateurs Safari et les appareils iOS mobiles.**

- Si votre site web utilise déjà la variable [Service d’ID d’Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=fr) sur votre site web (via l’API visiteur ou l’extension du service d’ID Experience Cloud dans Adobe Experience Platform Launch) et que vous souhaitez continuer à l’utiliser lors de la migration vers le SDK Web Adobe Experience Platform, vous devez utiliser la dernière version de l’API visiteur ou l’extension du service d’ID Experience Cloud. Voir [Migration des identifiants](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#identity) pour plus d’informations.
