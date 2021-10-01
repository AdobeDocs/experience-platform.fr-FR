---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Prise en main de l’API Segmentation Service
topic-legacy: developer guide
description: La documentation suivante fournit des informations supplémentaires dont vous avez besoin pour travailler avec l’API Segmentation.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 50%

---

# Prise en main de l’API Segmentation Service {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des segments et de générer des audiences dans Adobe Experience Platform à partir de vos données [!DNL Real-time Customer Profile].

Le guide de développement nécessite une compréhension pratique des différents services [!DNL Experience Platform] impliqués dans l’utilisation de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permet de créer des segments d’audience à partir de  [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour travailler avec l’API [!DNL Segmentation].

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Segmentation Service] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s&#39;agit notamment de chemins d&#39;accès, d&#39;en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis) pour lancer des appels vers des points de terminaison [!DNL Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des environnements de test dans [!DNL Experience Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

## Étapes suivantes

Pour lancer des appels à l’aide de l’API [!DNL Segmentation Service], sélectionnez l’un des guides de point de terminaison disponibles à l’aide du volet de navigation de gauche ou dans la [présentation du guide de développement](./overview.md)
