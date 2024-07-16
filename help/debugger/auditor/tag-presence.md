---
title: Référence du test de présence de balises
description: Découvrez comment l’Auditor teste la présence de balises dans Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 17%

---

# Référence du test de présence de balise

Cette référence fournit des informations supplémentaires sur la manière dont la fonction d’audit dans les tests d’Adobe Experience Platform Debugger pour la présence de balises.

>[!NOTE]
>
>Pour plus d’informations sur les tests d’Auditor dans Platform Debugger, consultez la [présentation des fonctionnalités d’Auditor](./overview.md).

Les tests de présence de balises évaluent si certaines balises existent sur la page et si elles se trouvent au bon endroit dans le code de votre page.

| Test | Poids | Critères | Recommandation |
| --- | --- | --- | --- |
| Advertising Cloud - Présence du code | 5 | La balise Advertising Cloud n’est pas disponible dans le modèle DOM. | Implémentez la balise Advertising Cloud à l’aide de l’ [extension de balise Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud : pixel de segment implémenté | 5 | Mettez à niveau vos pixels de segment Advertising Cloud vers les nouvelles balises image seule Advertising Cloud. L’utilisation de balises de segment AMO obsolètes peut entraîner une perte de données. | Implémentez le pixel de segment Advertising Cloud à l’aide de l’ [extension de balise Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - Chargé dans DOM | 5 | La balise Adobe Analytics n’a pas été détectée. | Installez la dernière version d’Analytics. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr) |
| Launch : bibliothèque chargée | 5 | Un objet `global _satellite` est introuvable dans le modèle DOM, ce qui signifie que la bibliothèque de balises n’est pas installée ou ne s’exécute pas. | Vérifiez que la bibliothèque de balises est implémentée sur la page et n’est pas bloquée par les activités de script suivantes. |
| Launch : ne comporte pas plusieurs scripts d’intégration | 5 | Les sites de production ne doivent charger qu’un seul code incorporé par page. | Vérifiez que seule la bibliothèque de production est en cours de chargement sur la page. |
| Launch : `pageBottom` le rappel existe dans `<body>` | 5 | Le rappel `_satellite.pageBottom()` requis est introuvable dans la balise `<body>` de la page. Ce test échoue si l’appel `pageBottom` est introuvable sur la page ou s’il se trouve dans la balise `<head>` (ou à un autre emplacement inattendu). Elle ne sera transmise que si `pageBottom` se trouve quelque part dans la balise `<body>`. | Ajoutez le script intégré juste avant la balise `</body>` de fermeture afin d’assurer le bon fonctionnement des balises.<br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch : le rappel `pageBottom` ne doit pas exister lors du déploiement asynchrone | 5 | Le rappel `_satellite.pageBottom()` a été trouvé sur la page, ce qui ne doit pas être le cas lorsque les balises sont déployées de manière asynchrone. | Supprimez le script `_satellite.pageBottom()` pour activer la fonctionnalité de balises appropriée. <br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Service d’ID d’Experience Cloud : présence du code | 5 | Le code du service Experience Cloud ID est introuvable. Il est vivement recommandé d’utiliser des identifiants Experience Cloud (ECID) pour tirer le meilleur parti de vos solutions Experience Cloud et pour gérer les identifiants dans toutes les solutions Experience Cloud. | Installez la dernière version d’ECID.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) |
| Service d’ID d’Experience Cloud : présence du cookie | 5 | Le cookie `AMCV_` est introuvable. Vous devez instancier un objet visiteur à partir du code `VisitorAPI.js`. | S’il s’agit d’une implémentation de balises, vérifiez que l’ID AdobeOrg est correctement saisi dans l’outil ECID. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Service d’ID d’Experience Cloud : présence de la valeur MID | 5 | La valeur MID est introuvable dans le cookie `AMCV_`. | Testez à nouveau pour vérifier la latence de l’API ECID. Si la condition persiste, contactez l’assistance clientèle Adobe. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target : présence du code | 5 | Adobe Target doit être défini dans le modèle DOM. | Installez la dernière version de Target (at.js). <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target : bibliothèque chargée dans `<head>` | 4 | La bibliothèque Target doit être chargée dans la balise `<head>` . | Vérifiez que la bibliothèque Target est chargée dans la balise `<head>`. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
