---
solution: Experience Platform
title: Prise en main de l’API des balises unifiées
description: La documentation suivante fournit des informations supplémentaires dont vous avez besoin pour travailler avec l’API des balises unifiées.
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 44%

---

# Prise en main de l’API des balises unifiées {#getting-started}

L’API Balises unifiées vous permet de classer et de gérer vos objets commerciaux dans Adobe Experience Platform.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour travailler avec l’API des balises unifiées.

## Lecture d’exemples d’appels API

La documentation de l’API des balises unifiées fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage de l’Experience Platform.

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour lancer des appels vers des points d’entrée Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Étapes suivantes

Pour lancer des appels à l’aide de l’API des balises unifiées, sélectionnez l’un des guides de point de terminaison disponibles à l’aide du volet de navigation de gauche ou dans la [présentation du guide de développement](./overview.md)
