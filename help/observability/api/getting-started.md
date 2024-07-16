---
keywords: Experience Platform;accueil;rubriques populaires;période
solution: Experience Platform
title: Prise en main de l’API Observability Insights
description: L’API Observability Insights vous permet de récupérer des données de mesure pour différentes fonctionnalités de Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels vers l’API Observability Insights.
exl-id: 3b120bd6-155d-467e-b98e-05478f8a4cc5
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 51%

---

# Prise en main de l’API [!DNL Observability Insights]

L’API [!DNL Observability Insights] vous permet de récupérer des données de mesure pour différentes fonctionnalités de Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API [!DNL Observability Insights].

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Observability Insights] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la lecture d’exemples d’appels API dans le [guide de dépannage Experience Platform](../../landing/troubleshooting.md).

## En-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu. Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API [!DNL Observability Insights], passez au [guide de point de terminaison de mesures](./metrics.md).
