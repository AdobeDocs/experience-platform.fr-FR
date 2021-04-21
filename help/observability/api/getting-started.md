---
keywords: Experience Platform ; accueil ; rubriques populaires ; plage de dates
solution: Experience Platform
title: Prise en main de l’API Observability Insights
topic-legacy: developer guide
description: L’API Observability Insights vous permet de récupérer des données de mesure pour différentes fonctionnalités Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant de tenter d'appeler l'API Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 24%

---

# Prise en main de l’API [!DNL Observability Insights]

L&#39;API [!DNL Observability Insights] vous permet de récupérer des données de mesure pour différentes fonctionnalités Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant de tenter d&#39;appeler l&#39;API [!DNL Observability Insights].

## Lecture d’exemples d’appels API

La documentation de l&#39;API [!DNL Observability Insights] fournit des exemples d&#39;appels d&#39;API pour montrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, consultez la section sur la façon de lire des exemples d&#39;appels d&#39;API dans le [guide de dépannage Experience Platform](../../landing/troubleshooting.md).

## En-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu. Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Étapes suivantes

Pour commencer à lancer des appels à l&#39;aide de l&#39;API [!DNL Observability Insights], passez au guide du point de terminaison [metrics](./metrics.md).
