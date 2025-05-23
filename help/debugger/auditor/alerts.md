---
title: Référence de test d’alerte
description: Découvrez comment l’auditeur teste les alertes dans Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 13%

---

# Référence du test d’alerte

Cette référence fournit des informations supplémentaires sur la manière dont la fonction d’audit d’Adobe Experience Platform Debugger exécute les tests d’alerte.

>[!NOTE]
>
>Pour plus d’informations sur les tests de l’auditeur dans Experience Platform Debugger, consultez la [présentation des fonctionnalités de l’auditeur](./overview.md).

Les alertes indiquent les problèmes que vous devez connaître, mais qui n’affectent pas votre score. Il s’agit de recommandations de bonnes pratiques qui, dans certains cas, peuvent ne pas s’appliquer à votre mise en œuvre.

| Test | Poids | Critères | Recommandation |
| --- | --- | --- | --- |
| Advertising Cloud - Balise De Conversion Correcte Implémentée | 0 | Vérifiez si c’est la balise de conversion appropriée qui est utilisée.<br><br>**Avertissement** : l’utilisation des balises de conversion TubeMogul obsolètes peut entraîner une perte de données. | Mettez à niveau vos pixels de conversion vers les nouvelles balises de conversion d’image uniquement Advertising Cloud. Ce type d’opération est plus facile à réaliser avec l’extension de balises [ Advertising Cloud ](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Balise JS Correcte Utilisée | 0 | Advertising Cloud doit utiliser les dernières balises JavaScript. | Mettez à niveau votre JavaScript Advertising Cloud vers la dernière version. L’utilisation des versions obsolètes de JavaScript peut entraîner une perte de fonctionnalités. Pour ce faire, il suffit d’utiliser l’extension de balise [ Advertising Cloud ](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Balise d’image seule | 0 | Le format de pixel d’image Advertising Cloud doit correspondre à l’un des formats recommandés suivants : <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Mettez à niveau vos pixels Advertising Cloud vers les nouvelles balises Image seule Advertising Cloud, qui vous permettent de tirer parti de l’ensemble des fonctionnalités d’Advertising Cloud. Ce type d’opération est plus facile à réaliser avec l’extension de balises [ Advertising Cloud ](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Synchronisation DSP Des Pixels De Segment Activée | 0 | Vérifiez si le pixel de segment TubeMogul contient un paramètre de synchronisation DSP et recommandez que le paramètre soit ajouté au pixel. Le paramètre de synchronisation DSP est déterminé par l’utilisation d’un paramètre de chaîne de requête. Pour résumer : <ul><li>SI la balise est déclenchée vers l’un des éléments suivants :<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>ET la balise contient le paramètre URL `sid=`</li><li>Ensuite, vérifiez si le paramètre d’URL `cs=0` ou `cs=1` existe et, dans le cas contraire, `cs=1` recommandons de l’ajouter à ces pixels afin d’améliorer les taux de correspondance d’audience.</li></ul> | Ajoutez le paramètre d’URL `cs=1` à vos pixels Advertising Cloud afin que la synchronisation DSP puisse avoir lieu, ce qui augmente les taux de correspondance d’audience. Cela est plus facile à réaliser avec l’extension de balises [ Advertising Cloud ](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Service Experience Cloud ID : utiliser une seule AdobeOrg | 0 | Dans une implémentation ECID normale, une seule AdobeOrg doit être utilisée. | Vérifiez qu’il existe plusieurs ID d’organisation Adobe pour cette implémentation. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html?lang=fr) |
| Launch - emplacement du rappel `pageBottom` | 0 | La fonction `_satellite.pageBottom()` doit être présente pour que les balises fonctionnent. Ajoutez le script intégré juste avant la balise `</body>` de fermeture pour garantir le bon fonctionnement de la gestion dynamique des balises. Remarque : il est recommandé d’utiliser la balise comme dernière balise du `<body>`. S’il est détecté dans la balise `<body>`, il est possible qu’il fonctionne, mais comme il ne s’agit pas d’une bonne pratique, il peut fonctionner incorrectement ou entraîner des résultats inattendus ou indésirables. | Ajoutez le script intégré juste avant la balise `</body>` de fermeture pour garantir le bon fonctionnement de la gestion dynamique des balises. <br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - Auto-hébergé | 0 | La bibliothèque de balises est hébergée sur l’instance Adobe Akamai à l’adresse `assets.adobedtm.com`. L’auto-hébergement est l’approche recommandée pour le chargement des balises, car elle permet de mieux contrôler les performances du site web par le biais du contrôle du cache, de réduire les dépendances de scripts tiers et de mieux contrôler le processus de publication. Les bibliothèques de balises peuvent être hébergées et gérées via votre propre hébergement web ou votre réseau CDN. | Basculez vers une approche d’auto-hébergement pour charger les balises sur une page. Bien que l’hébergement via le réseau CDN Akamai fonctionne dans la plupart des cas, l’auto-hébergement améliore les performances des pages. <br><br>Informations supplémentaires :<ul><li>[ Guide de démarrage rapide des balises ](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Déploiement asynchrone](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch : doit être déployé de manière asynchrone. | 0 | Les balises doivent être déployées de manière asynchrone pour des performances optimales. | Incluez le paramètre `async` dans le script intégré pour garantir la fonctionnalité de balises appropriée <br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target - Contenu dans les `mboxDefault` | 0 | Le contenu doit exister dans les `mboxDefault` lors de l’utilisation de `at.js`. | Vérifiez que le contenu est disponible. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=fr) |

{style="table-layout:auto"}
