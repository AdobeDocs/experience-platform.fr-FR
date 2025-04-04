---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;requête
solution: Experience Platform
title: Guide de l’API Query Service
description: L’API Query Service permet aux développeurs d’interroger leurs données Adobe Experience Platform à l’aide de SQL standard. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 100%

---

# Guide de l’API [!DNL Query Service]

Ce guide de développement décrit les étapes à suivre pour effectuer diverses opérations dans l’API [!DNL Query Service] d’Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique des divers services Adobe Experience Platform impliqués dans l’utilisation de [!DNL Query Service].

- [[!DNL Query Service]](../home.md) : permet de soumettre des requêtes aux jeux de données et de capturer les requêtes résultantes sous forme de nouveaux jeux de données dans [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour utiliser correctement [!DNL Query Service] à l’aide de l’API.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans cette documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Exemples d’appels API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt(e) à commencer à lancer des appels à l’API [!DNL Query Service]. Les documents suivants décrivent les différents appels API que vous pouvez effectuer à l’aide de l’API [!DNL Query Service]. Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

- [Requêtes](queries.md)
- [Paramètres de connexion](connection-parameters.md)
- [Requêtes planifiées](scheduled-queries.md)
- [Exécutions pour les requêtes planifiées](runs-scheduled-queries.md)
- [Modèles de requête](query-templates.md)
- [Requêtes accélérées](./accelerated-queries.md)
- [Abonnements aux alertes](./alert-subscriptions.md)

## Étapes suivantes

Maintenant que vous avez appris à lancer des appels à l’aide de l’API [!DNL Query Service], vous pouvez créer vos propres requêtes non interactives. Pour plus d’informations sur la création de requêtes, veuillez lire le [guide de référence SQL](../sql/overview.md).
