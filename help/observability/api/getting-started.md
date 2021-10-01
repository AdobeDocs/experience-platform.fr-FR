---
keywords: Experience Platform;accueil;rubriques populaires;période
solution: Experience Platform
title: Prise en main de l’API Observability Insights
topic-legacy: developer guide
description: L’API Observability Insights vous permet de récupérer des données de mesure pour différentes fonctionnalités de Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels vers l’API Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 52%

---

# Prise en main de l’API [!DNL Observability Insights]

L’API [!DNL Observability Insights] vous permet de récupérer des données de mesure pour différentes fonctionnalités de Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API [!DNL Observability Insights].

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Observability Insights] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s&#39;agit notamment de chemins d&#39;accès, d&#39;en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la lecture d’exemples d’appels API dans le [guide de dépannage Experience Platform](../../landing/troubleshooting.md).

## En-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu. Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API [!DNL Observability Insights], passez au guide de point de terminaison [mesures](./metrics.md).
