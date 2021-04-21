---
keywords: Experience Platform ; accueil ; rubriques populaires ; service de requête ; service de Requête ; requête
solution: Experience Platform
title: Guide de l'API requête Service
topic-legacy: query templates
description: L’API Requête Service permet aux développeurs de requête de leurs données Adobe Experience Platform à l’aide de SQL standard. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 39%

---

# [!DNL Query Service] Guide des API

Ce guide du développeur décrit les étapes à suivre pour effectuer diverses opérations dans l&#39;API Adobe Experience Platform [!DNL Query Service].

## Prise en main

Ce guide nécessite une compréhension pratique des divers services Adobe Experience Platform impliqués dans l’utilisation de la [!DNL Query Service].

- [[!DNL Query Service]](../home.md): Permet de requête des jeux de données et de capturer les requêtes résultantes sous forme de nouveaux jeux de données dans  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour utiliser [!DNL Query Service] avec succès avec l&#39;API.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans cette documentation pour les exemples d&#39;appels d&#39;API, consultez la section [comment lire des exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Platform], comme indiqué ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur l&#39;utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation d&#39;aperçu des sandbox](../../sandboxes/home.md).

## Exemples d’appels API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l&#39;API [!DNL Query Service]. Les documents suivants passent en revue les différents appels d&#39;API que vous pouvez effectuer à l&#39;aide de l&#39;API [!DNL Query Service]. Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

- [Requêtes](queries.md)
- [Paramètres de connexion](connection-parameters.md)
- [Requêtes planifiées](scheduled-queries.md)
- [Exécutions pour les requêtes planifiées](runs-scheduled-queries.md)
- [Modèles de requête](query-templates.md)

## Étapes suivantes

Maintenant que vous avez appris à passer des appels à l&#39;aide de l&#39;API [!DNL Query Service], vous pouvez créer vos propres requêtes non interactives. Pour plus d’informations sur la création de requêtes, veuillez lire le [guide de référence SQL](../sql/overview.md).
