---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; Service de segmentation ; api ;
solution: Experience Platform
title: Prise en main de l’API du service de segmentation
topic-legacy: developer guide
description: La documentation suivante fournit des informations supplémentaires dont vous avez besoin pour travailler avec l’API de segmentation.
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 30%

---

# Prise en main de l’API du service de segmentation {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des segments et de générer des audiences dans Adobe Experience Platform à partir de vos données [!DNL Real-time Customer Profile].

Le guide du développeur exige une compréhension pratique des différents services [!DNL Experience Platform] liés à l&#39;utilisation de [!DNL Segmentation Service].

- [[!DNL Segmentation]](../home.md): Permet de créer des segments d’audience à partir de  [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Sandbox](../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour utiliser l&#39;API [!DNL Segmentation] avec succès.

## Lecture d’exemples d’appels API

La documentation de l&#39;API [!DNL Segmentation Service] fournit des exemples d&#39;appels d&#39;API pour montrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en) pour lancer des appels vers des points de terminaison [!DNL Platform] Le didacticiel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur l&#39;utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation d&#39;aperçu des sandbox](../../sandboxes/home.md).

## Étapes suivantes

Pour effectuer des appels à l&#39;aide de l&#39;API [!DNL Segmentation Service], sélectionnez l&#39;un des guides de points de terminaison disponibles à l&#39;aide du volet de navigation de gauche ou dans le [guide du développeur présentation](./overview.md)
