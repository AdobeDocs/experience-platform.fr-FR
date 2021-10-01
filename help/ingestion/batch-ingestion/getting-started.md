---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Prise en main de l’API Data Ingestion
type: Documentation
description: Le guide de prise en main de l’API Data Ingestion décrit les concepts clés et les fonctionnalités de base que vous devez connaître avant de commencer à ingérer des données dans Experience Platform à l’aide d’API.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 648923a0a124767f530bea09519449f76d576b5e
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 43%

---

# Prise en main de l’API Data Ingestion {#getting-started}

À l’aide des points de terminaison de l’API Data Ingestion, vous pouvez effectuer des opérations CRUD de base afin d’ingérer des données dans Adobe Experience Platform.

L’utilisation des guides de l’API nécessite une compréhension pratique de plusieurs services Adobe Experience Platform impliqués dans l’utilisation des données. Avant d’utiliser l’API Data Ingestion, consultez la documentation relative aux services suivants :

* [Ingestion par lots](./overview.md) : vous permet d’ingérer des données dans Adobe Experience Platform sous forme de fichiers de lots.
* [[!DNL Real-time Customer Profile]](../home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une  [!DNL Platform] instance unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à des points de terminaison de l’API [!DNL Profile].

## Lecture d&#39;exemples d&#39;appels API

La documentation de l’API Data Ingestion fournit des exemples d’appels API pour démontrer comment formater correctement les requêtes. Il s&#39;agit notamment de chemins d&#39;accès, d&#39;en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis) pour lancer des appels vers des points de terminaison [!DNL Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).
