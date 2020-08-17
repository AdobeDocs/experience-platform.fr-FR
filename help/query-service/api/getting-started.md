---
keywords: Experience Platform;home;popular topics;query service;Query service;query
solution: Experience Platform
title: Guide de développement de Query Service
topic: query templates
description: Ce guide de développement décrit les étapes à suivre pour effectuer diverses opérations dans l’API Adobe Experience Platform Query Service.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 35%

---


# [!DNL Query Service] guide du développeur

This developer guide provides steps for performing various operations in the Adobe Experience Platform [!DNL Query Service] API.

## Prise en main

Ce guide nécessite une compréhension pratique des divers services Adobe Experience Platform impliqués dans l’utilisation de la [!DNL Query Service].

- [!DNL Query Service](../home.md): Permet de requête des jeux de données et de capturer les requêtes résultantes sous forme de nouveaux jeux de données dans [!DNL Experience Platform].
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et développer des applications d&#39;expérience numérique.

The following sections provide additional information that you will need to know in order to successfully use [!DNL Query Service] using the API.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in this documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in the [!DNL Experience Platform] troubleshooting guide.

### Collecte des valeurs des en-têtes requis

In order to make calls to [!DNL Experience Platform] APIs, you must first complete the [authentication tutorial](../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Platform] API calls, as shown below:

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox in which the operation will take place:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on working with sandboxes in [!DNL Experience Platform], see the [sandboxes overview documentation](../../sandboxes/home.md).

## Exemples d’appels API

Now that you understand what headers to use, you are ready to begin making calls to the [!DNL Query Service] API. The following documents walk through the various API calls you can make using the [!DNL Query Service] API. Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

- [Requêtes](queries.md)
- [Paramètres de connexion](connection-parameters.md)
- [Requêtes planifiées](scheduled-queries.md)
- [Exécutions pour les requêtes planifiées](runs-scheduled-queries.md)
- [Modèles de requête](query-templates.md)

## Étapes suivantes

Now that you have learned how to make calls using the [!DNL Query Service] API, you can create your own non-interactive queries. Pour plus d’informations sur la création de requêtes, veuillez lire le [guide de référence SQL](../sql/overview.md).