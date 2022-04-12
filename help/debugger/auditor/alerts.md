---
title: Référence du test d’alerte
description: Découvrez comment l’Auditor teste les alertes dans Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 36%

---

# Référence du test d’alerte

Cette référence fournit des informations supplémentaires sur la manière dont la fonction Auditor de Adobe Experience Platform Debugger exécute des tests d’alerte.

>[!NOTE]
>
>Pour plus d’informations sur les tests d’Auditor dans Platform Debugger, voir la section [présentation de la fonctionnalité auditor](./overview.md).

Les alertes indiquent les problèmes que vous devez connaître, mais qui n’affectent pas votre score. Il s’agit de recommandations de bonnes pratiques qui, dans certains cas, peuvent ne pas s’appliquer à votre mise en œuvre.

| Test | Poids | Critères | Recommandation |
| --- | --- | --- | --- |
| Advertising Cloud : balise de conversion correcte implémentée | 0 | Vérifiez si c’est la balise de conversion appropriée qui est utilisée.<br><br>**Avertissement**: L’utilisation des balises de conversion obsolètes de TubeMogul peut entraîner une perte de données. | Mettez à niveau vos pixels de conversion vers les nouvelles balises de conversion image seule Advertising Cloud. Cela peut être réalisé facilement à l’aide de la fonction [Extension de balise Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud : balise JS correcte utilisée | 0 | Advertising Cloud doit utiliser les dernières balises JavaScript. | Mettez à niveau votre JavaScript Advertising Cloud vers la dernière version. L’utilisation de versions JavaScript obsolètes peut entraîner la perte de fonctionnalités. Pour ce faire, utilisez la méthode [Extension de balise Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud : balise image seule | 0 | Le format de pixel d’image Advertising Cloud doit correspondre à l’un des formats recommandés suivants : <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Mettez à niveau vos pixels Advertising Cloud vers les nouvelles balises image seule Advertising Cloud, afin de complètement tirer parti de la fonctionnalité d’Advertising Cloud. Cela peut être réalisé facilement à l’aide de la fonction [Extension de balise Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud : pixels de segment, synchronisation DSP activée | 0 | Vérifiez si le pixel du segment TubeMogul contient un paramètre de synchronisation DSP, et demandez que ce paramètre soit ajouté au pixel. Le paramètre de synchronisation DSP est déterminé par l’utilisation d’un paramètre de chaîne de requête. Pour résumer : <ul><li>SI la balise est déclenchée sur l’une des méthodes suivantes :<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>ET la balise contient le paramètre d’URL `sid=`</li><li>ALORS vérifiez si le paramètre d’URL `cs=0` ou `cs=1` existe et, si ce n’est pas le cas, vous devez : `cs=1` à ces pixels afin que les taux de correspondance de l’audience puissent s’améliorer.</li></ul> | Ajout du paramètre d’URL `cs=1` à vos pixels Advertising Cloud afin que DSP synchronisation puisse se produire, ce qui augmente les taux de correspondance de l’audience. Cela peut être réalisé facilement avec la méthode [Extension de balise Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Service Experience Cloud ID : utiliser une seule AdobeOrg | 0 | Dans une implémentation ECID normale, une seule AdobeOrg doit être utilisée. | Vérifiez que plusieurs identifiants AdobeOrg existent pour cette implémentation. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch - `pageBottom` placement du rappel | 0 | Le `_satellite.pageBottom()` doit être présente pour que les balises fonctionnent. Ajouter le script intégré juste avant la fermeture `</body>` pour garantir le bon fonctionnement de DTM. Remarque : Il est recommandé que la balise soit la dernière balise dans `<body>`. Si elle se trouve dans la variable `<body>` , il a une chance de fonctionner, mais comme ce n’est pas la bonne pratique, il peut fonctionner incorrectement ou avec des résultats inattendus ou non souhaités. | Ajouter le script intégré juste avant la fermeture `</body>` pour garantir le bon fonctionnement de DTM. <br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch : auto-hébergement | 0 | La bibliothèque de balises est hébergée sur l’instance Akamai d’Adobe à l’adresse `assets.adobedtm.com`. L’auto-hébergement est l’approche recommandée pour le chargement des balises, car elle permet un meilleur contrôle des performances du site web grâce au contrôle du cache, la réduction des dépendances des scripts tiers et un meilleur contrôle du processus de publication. Les bibliothèques de balises peuvent être hébergées et gérées via votre propre hébergement web ou CDN. | Le passage à l’auto-hébergement est l’approche permettant de charger des balises sur une page. Bien que l’hébergement de par le biais du réseau de diffusion de contenu Akamai fonctionne dans la plupart des cas, l’auto-hébergement améliore les performances des pages. <br><br>Informations supplémentaires:<ul><li>[Guide de démarrage rapide des balises](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Déploiement asynchrone](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch : doit être déployé de manière asynchrone | 0 | Les balises doivent être déployées de manière asynchrone pour des performances optimales. | Inclure la variable `async` dans le script intégré afin d’assurer le bon fonctionnement des balises. <br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target - Contenu dans `mboxDefault` | 0 | Le contenu doit exister dans `mboxDefault` lors de l’utilisation de `at.js`. | Vérifiez que le contenu est disponible. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
