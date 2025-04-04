---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Prise en main de l’API Data Ingestion
type: Documentation
description: Le guide de prise en main de l’API Data Ingestion décrit les concepts clés et les fonctionnalités de base que vous devez connaître avant de commencer à ingérer des données dans Experience Platform à l’aide d’API.
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 53%

---

# Prise en main de l’API Data Ingestion {#getting-started}

À l’aide des points d’entrée de l’API Data Ingestion, vous pouvez effectuer des opérations CRUD de base pour ingérer des données dans Adobe Experience Platform.

L’utilisation des guides d’API nécessite une compréhension pratique de plusieurs services Adobe Experience Platform impliqués dans l’utilisation des données. Avant d’utiliser l’API Data Ingestion, consultez la documentation relative aux services suivants :

* [Ingestion par lots](./overview.md) : vous permet d’ingérer des données dans Adobe Experience Platform sous forme de fichiers de lots.
* [[!DNL Real-Time Customer Profile]](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
* [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de passer avec succès des appels vers des points d’entrée d’API [!DNL Profile].

## Lecture d’exemples d’appels API

La documentation de l’API Data Ingestion fournit des exemples d’appels API pour démontrer comment formater correctement les requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour lancer des appels vers des points d’entrée [!DNL Experience Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Les requêtes [!DNL Experience Platform] API nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).
