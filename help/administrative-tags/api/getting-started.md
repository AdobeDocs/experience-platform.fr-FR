---
solution: Experience Platform
title: Prise en main de l’API des balises unifiées
description: La documentation suivante fournit des informations supplémentaires que vous devez connaître pour utiliser correctement l’API des balises unifiées.
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
TQID: https://experienceleague.adobe.com/NqOjMm0CoMKRcl5C2iHvvj0Lbl--Q6KSMyBNoEF7yRE
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 276
ht-degree: 39%

---

# Prise en main de l’API des balises unifiées {#getting-started}

L’API Balises unifiées vous permet de classer et de gérer vos objets métier dans Adobe Experience Platform.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour utiliser correctement l’API Balises unifiées.

## Lecture d&#39;exemples d&#39;appels API

La documentation de l’API Balises unifiées fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, voir la section concernant la [lecture d’exemples d’appels API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## En-têtes requis

La documentation de l’API exige également que vous ayez suivi le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) afin d’effectuer avec succès des appels vers des points d’entrée Experience Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Étapes suivantes

Pour lancer des appels à l’aide de l’API Balises unifiées, sélectionnez l’un des guides de point d’entrée disponibles à l’aide du volet de navigation de gauche ou dans la [présentation du guide de développement](./overview.md)
