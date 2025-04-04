---
title: Référence de test de présence de balise
description: Découvrez comment l’auditeur teste la présence de balises dans Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 17%

---

# Référence de test de présence de balise

Cette référence fournit plus d’informations sur la manière dont la fonction d’auditeur d’Adobe Experience Platform Debugger teste la présence de balises.

>[!NOTE]
>
>Pour plus d’informations sur les tests de l’auditeur dans Experience Platform Debugger, consultez la [présentation des fonctionnalités de l’auditeur](./overview.md).

Les tests de présence de balises évaluent si certaines balises existent sur la page et si elles se trouvent au bon endroit dans le code de votre page.

| Test | Poids | Critères | Recommandation |
| --- | --- | --- | --- |
| Advertising Cloud - Présence du code | 5 | La balise Advertising Cloud n’est pas disponible dans le modèle DOM. | Implémentez la balise Advertising Cloud à l’aide de l’extension de balise [Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Pixel de segment implémenté | 5 | Mettez à niveau vos pixels de segment Advertising Cloud vers les nouvelles balises image seule Advertising Cloud. L’utilisation de balises de segment AMO obsolètes peut entraîner une perte de données. | Implémentez le pixel de segment Advertising Cloud à l’aide de l’extension de balises [ Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - Chargé dans DOM | 5 | La balise Adobe Analytics n’a pas été détectée. | Installez la dernière version d’Analytics. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=fr) |
| Launch - Bibliothèque chargée | 5 | Un objet `global _satellite` est introuvable dans le DOM, ce qui signifie que la bibliothèque de balises n’est pas installée ou ne s’exécute pas. | Vérifiez que la bibliothèque de balises est implémentée sur la page et n’est pas bloquée par les activités de script suivantes. |
| Launch - Ne comporte pas plusieurs scripts incorporés | 5 | Les sites de production ne doivent charger qu’un seul code incorporé par page. | Vérifiez que seule la bibliothèque de production est en cours de chargement sur la page. |
| Launch - `pageBottom` rappel existe dans `<body>` | 5 | Le rappel `_satellite.pageBottom()` obligatoire est introuvable dans le `<body>` de la page. Ce test échoue si l’appel de `pageBottom` est introuvable sur la page ou s’il se trouve dans la balise `<head>` (ou à un autre emplacement inattendu). Il ne sera transmis que si `pageBottom` se trouve quelque part dans la balise `<body>`. | Ajoutez le script intégré juste avant la balise `</body>` de fermeture pour garantir le bon fonctionnement des balises.<br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch : le rappel `pageBottom` ne doit pas exister en cas de déploiement asynchrone | 5 | Le rappel `_satellite.pageBottom()` a été trouvé sur la page, ce qui ne devrait pas être le cas lorsque les balises sont déployées de manière asynchrone. | Supprimez le script `_satellite.pageBottom()` pour activer la fonctionnalité de balises appropriée. <br><br>[Informations supplémentaires](../../tags/ui/client-side/asynchronous-deployment.md) |
| Service Experience Cloud ID : présence du code | 5 | Le code du service Experience Cloud ID est introuvable. L’utilisation d’Experience Cloud ID (ECID) est vivement recommandée pour vous assurer de tirer le meilleur parti de vos solutions Experience Cloud et elle est essentielle à la gestion des identifiants dans les solutions Experience Cloud. | Installez la version la plus récente d’ECID.<br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) |
| Service Experience Cloud ID : présence du cookie | 5 | Le cookie `AMCV_` est introuvable. Vous devez instancier un objet visiteur à partir du code `VisitorAPI.js`. | S’il s’agit d’une implémentation de balises, vérifiez que l’ID d’organisation Adobe est correctement saisi dans l’outil ECID. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Service Experience Cloud ID : présence de la valeur MID | 5 | La valeur MID est introuvable dans le cookie `AMCV_`. | Testez à nouveau pour vérifier la latence de l’API ECID. Si le problème persiste, contactez l’Assistance clientèle d’Adobe. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Cible - Présence du code | 5 | Adobe Target doit être défini dans le DOM. | Installez la version la plus récente de Target (at.js). <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - Bibliothèque chargée en `<head>` | 4 | La bibliothèque Target doit être chargée dans la balise `<head>`. | Vérifiez que la bibliothèque Target est chargée dans la balise `<head>`. <br><br>[Informations supplémentaires](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
