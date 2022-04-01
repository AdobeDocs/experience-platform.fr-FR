---
title: Dépannage
description: Découvrez comment résoudre les erreurs lors de l’utilisation de l’API Adobe Experience Platform Edge Network Server
seo-description: Learn how to troubleshoot errors when using the Adobe Experience Platform Edge Network Server API
keywords: réseau Edge;passerelle;api;dépannage;erreurs;griffon
source-git-commit: 2b501c9384fecb016489a21a308a595186153f03
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 1%

---


# Dépannage

L’API Adobe Experience Platform Edge Network Server vous permet de capturer les informations de débogage des services, car vos événements sont traités par le biais du pipeline de collecte de données Edge Network.

Même mécanisme utilisé par la fonction [Débogueur Experience Platform](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) vous permet de déboguer des implémentations basées sur l’API.

Utilisation [Griffon du projet](https://aep-sdks.gitbook.io/docs/beta/project-griffon), vous pouvez créer un ID de session de débogage que vous pourrez ensuite utiliser dans les requêtes réseau Edge pour suivre les événements.

