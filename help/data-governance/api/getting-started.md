---
keywords: Experience Platform;accueil;rubriques populaires;DULE;dule
solution: Experience Platform
title: Prise en main de l’API Policy Service
description: L’API Policy Service vous permet de créer et de gérer diverses ressources liées à la gouvernance des données d’Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API Policy Service.
role: Developer
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 95%

---

# Prise en main de l’API [!DNL Policy Service]

L’API [!DNL Policy Service] vous permet de créer et de gérer diverses ressources liées à la gouvernance des données d’Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API [!DNL Policy Service].

## Conditions préalables

L’utilisation du guide de développement nécessite une compréhension pratique des différents services [!DNL Experience Platform] impliqués dans l’utilisation des fonctionnalités de gouvernance des données. Avant de commencer à travailler avec les [!DNL Policy Service API], consultez la documentation relative aux services suivants :

* [Gouvernance des données](../home.md) : cadre selon lequel [!DNL Experience Platform] applique la conformité d’utilisation des données.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sandbox](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Policy Service] inclut des exemples d’appels d’API expliquant comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis) pour lancer des appels vers des points d’entrée [!DNL Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources d’[!DNL Experience Platform], y compris celles liées à la gouvernance des données, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Ressources de base ou personnalisées

Dans l’API [!DNL Policy Service], toutes les politiques et actions marketing sont nommées ressources `core` ou `custom`.

Les ressources `core` sont celles définies et gérées par Adobe, tandis que les ressources `custom` sont celles créées et gérées par votre organisation. Ces dernières sont donc uniques et visibles uniquement par votre organisation. Les opérations de liste et de recherche (`GET`) sont donc les seules opérations autorisées sur les ressources `core`, alors que les opérations de liste, de recherche et de mise à jour (`POST`, `PUT`, `PATCH` et `DELETE`) sont disponibles pour les ressources `custom`.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API Policy Service, sélectionnez l’un des guides de point d’entrée disponibles.
