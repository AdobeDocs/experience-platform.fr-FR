---
keywords: Experience Platform;accueil;rubriques populaires;query service;Query service;requête
solution: Experience Platform
title: Guide de l’API Query Service
topic-legacy: query templates
description: L’API Query Service permet aux développeurs d’interroger leurs données Adobe Experience Platform à l’aide de SQL standard. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 48%

---

# Guide de l’API [!DNL Query Service]

Ce guide de développement décrit les étapes à suivre pour effectuer diverses opérations dans l’API Adobe Experience Platform [!DNL Query Service].

## Prise en main

Ce guide nécessite une compréhension pratique des divers services Adobe Experience Platform impliqués dans l’utilisation de la [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Permet d’interroger des jeux de données et de capturer les requêtes résultantes sous forme de nouveaux jeux de données dans  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une  [!DNL Platform] instance unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour utiliser correctement [!DNL Query Service] à l’aide de l’API.

### Lecture d&#39;exemples d&#39;appels API

Ce guide fournit des exemples d&#39;appels API pour démontrer comment formater vos requêtes. Il s&#39;agit notamment de chemins d&#39;accès, d&#39;en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d’informations sur les conventions utilisées dans cette documentation pour les exemples d’appels API, consultez la section sur [la lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d&#39;abord suivre le [tutoriel d&#39;authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Platform], comme indiqué ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des environnements de test dans [!DNL Experience Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

## Exemples d’appels API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API [!DNL Query Service]. Les documents suivants passent en revue les différents appels API que vous pouvez effectuer à l’aide de l’API [!DNL Query Service]. Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

- [Requêtes](queries.md)
- [Paramètres de connexion](connection-parameters.md)
- [Requêtes planifiées](scheduled-queries.md)
- [Exécutions pour les requêtes planifiées](runs-scheduled-queries.md)
- [Modèles de requête](query-templates.md)

## Étapes suivantes

Maintenant que vous avez appris à lancer des appels à l’aide de l’API [!DNL Query Service], vous pouvez créer vos propres requêtes non interactives. Pour plus d’informations sur la création de requêtes, veuillez lire le [guide de référence SQL](../sql/overview.md).
