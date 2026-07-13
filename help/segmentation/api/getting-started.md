---
keywords: Experience Platform;accueil;rubriques populaires;segmentation;Segmentation;Segmentation Service;api;
solution: Experience Platform
title: Prise en main de l’API Segmentation Service
description: La documentation suivante fournit des informations supplémentaires que vous devez connaître pour travailler avec l’API Segmentation.
role: Developer
exl-id: 41c0e50b-afed-45b8-85d7-a0c84ae090f5
TQID: https://experienceleague.adobe.com/kGC36J1XMUpGXX20QtrYucHr8vE9um4ymq4-71L1T-Q
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12bid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 18c3bd1c361dc9e284ede73aa84d188b76ef45c0
workflow-type: tm+mt
source-wordcount: 360
ht-degree: 63%

---

# Prise en main de l’API Segmentation Service {#getting-started}

Adobe Experience Platform [!DNL Segmentation Service] vous permet de créer des audiences par le biais de définitions de segment ou d’autres sources dans Adobe Experience Platform à partir de vos données [!DNL Real-Time Customer Profile].

Le guide de développement nécessite une compréhension pratique des différents services de [!DNL Experience Platform] impliqués dans l’utilisation de [!DNL Segmentation Service].

- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md) : permet de créer des audiences à partir de données [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).
- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
- [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour utiliser correctement l’API [!DNL Segmentation].

## Lecture d&#39;exemples d&#39;appels API

La documentation de l’API [!DNL Segmentation Service] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](/help/landing/api-authentication.md) pour lancer des appels vers des points d’entrée [!DNL Experience Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Étapes suivantes

Pour lancer des appels à l’aide de l’API [!DNL Segmentation Service], sélectionnez l’un des guides de point d’entrée disponibles à l’aide du volet de navigation de gauche ou dans la présentation du guide de développement [](./overview.md)


