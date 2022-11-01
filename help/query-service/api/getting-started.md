---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;requête
solution: Experience Platform
title: Guide de l’API Query Service
topic-legacy: query templates
description: L’API Query Service permet aux développeurs d’interroger leurs données Adobe Experience Platform à l’aide de SQL standard. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 4f85f38e4870f0c2429a3a2a50bd7f95075c6be4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 53%

---

# Guide de l’API [!DNL Query Service]

Ce guide de développement décrit les étapes à suivre pour effectuer diverses opérations dans Adobe Experience Platform [!DNL Query Service] API.

## Prise en main

Ce guide nécessite une compréhension pratique des divers services Adobe Experience Platform impliqués dans l’utilisation de la [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Permet d’interroger des jeux de données et de capturer les requêtes résultantes sous forme de nouveaux jeux de données dans [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour utiliser correctement [!DNL Query Service] à l’aide de l’API.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans cette documentation pour les exemples d’appels API, consultez la section sur [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le [!DNL Experience Platform] guide de dépannage.

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Platform], comme indiqué ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées à [!DNL Platform] Les API requièrent un en-tête qui spécifie le nom de l’environnement de test dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des environnements de test dans [!DNL Experience Platform], reportez-vous à la section [documentation sur les environnements de test](../../sandboxes/home.md).

## Exemples d’appels API

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à commencer à lancer des appels au [!DNL Query Service] API. Les documents suivants passent en revue les différents appels API que vous pouvez effectuer à l’aide de la variable [!DNL Query Service] API. Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

- [Requêtes](queries.md)
- [Paramètres de connexion](connection-parameters.md)
- [Requêtes planifiées](scheduled-queries.md)
- [Exécutions pour les requêtes planifiées](runs-scheduled-queries.md)
- [Modèles de requête](query-templates.md)
- [Abonnements aux alertes](./alert-subscriptions.md)

## Étapes suivantes

Maintenant que vous avez appris à lancer des appels à l’aide de la variable [!DNL Query Service] API, vous pouvez créer vos propres requêtes non interactives. Pour plus d’informations sur la création de requêtes, veuillez lire le [guide de référence SQL](../sql/overview.md).
