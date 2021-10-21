---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; api ;
solution: Experience Platform
title: Prise en main de l’API du service de segmentation
topic-legacy: developer guide
description: La documentation suivante fournit des informations supplémentaires que vous devez connaître pour travailler avec l’API de segmentation.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 47%

---

# Prise en main de l’API du service de segmentation {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des segments et de générer des publics dans Adobe Experience Platform à partir de votre [!DNL Real-time Customer Profile] données.

Le guide du développeur nécessite une compréhension pratique des différents [!DNL Experience Platform] services impliqués dans l&#39;utilisation [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permet de créer des segments d’audience à partir de [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client. Pour tirer le meilleur parti de la segmentation, assurez-vous que vos données sont assimilées en tant que profils et événements en fonction de [meilleures pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).
- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour travailler avec le [!DNL Segmentation] API.

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Segmentation Service] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s&#39;agit notamment de chemins d&#39;accès, d&#39;en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis) pour lancer des appels vers des points de terminaison [!DNL Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les demandes [!DNL Platform] Les API nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la section [sandbox présentation de la documentation](../../sandboxes/home.md).

## Étapes suivantes

Pour effectuer des appels à l’aide de la [!DNL Segmentation Service] API, sélectionnez l’un des repères de point de terminaison disponibles à l’aide de la navigation de gauche ou dans le noeud [présentation du guide du développeur](./overview.md)
