---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Prise en main de l’API Segmentation Service
description: La documentation suivante fournit des informations supplémentaires dont vous avez besoin pour travailler avec l’API Segmentation.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 56%

---

# Prise en main de l’API Segmentation Service {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des segments et de générer des audiences dans Adobe Experience Platform à partir de vos [!DNL Real-Time Customer Profile] data.

Le guide de développement nécessite une compréhension pratique des différentes [!DNL Experience Platform] services impliqués dans l’utilisation [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permet de créer des segments d’audience à partir de [!DNL Real-Time Customer Profile] data.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour travailler avec le [!DNL Segmentation] API.

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Segmentation Service] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour lancer des appels vers des points de terminaison [!DNL Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuelles spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de la sandbox dans laquelle l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Étapes suivantes

Pour effectuer des appels à l’aide de la fonction [!DNL Segmentation Service] , sélectionnez l’un des guides de point de terminaison disponibles à l’aide du volet de navigation de gauche ou dans le [présentation du guide de développement](./overview.md)
