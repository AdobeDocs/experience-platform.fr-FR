---
keywords: Experience Platform;accueil;rubriques populaires;DULE;dule
solution: Experience Platform
title: Prise en main de l’API Policy Service
topic-legacy: developer guide
description: L’API Policy Service vous permet de créer et de gérer diverses ressources liées à la gouvernance des données Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API Policy Service.
exl-id: 5539976c-8433-45af-a147-2ab82ae308b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 36%

---

# Prise en main de l’API [!DNL Policy Service]

L&#39;API [!DNL Policy Service] vous permet de créer et de gérer diverses ressources liées à Adobe Experience Platform [!DNL Data Governance]. Ce document présente les concepts de base que vous devez connaître avant de tenter d&#39;appeler l&#39;API [!DNL Policy Service].

## Conditions préalables

L&#39;utilisation du guide du développeur nécessite une compréhension pratique des différents services [!DNL Experience Platform] impliqués dans l&#39;utilisation des capacités de gouvernance des données. Avant de commencer à travailler avec [!DNL Policy Service API], veuillez consulter la documentation relative aux services suivants :

* [[!DNL Data Governance]](../home.md): Cadre selon lequel  [!DNL Experience Platform] applique la conformité à l’utilisation des données.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
* [[!DNL Real-time Customer Profile]](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sandbox](../../sandboxes/home.md) :  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

## Lecture d’exemples d’appels API

La documentation de l&#39;API [!DNL Policy Service] fournit des exemples d&#39;appels d&#39;API pour montrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en) pour lancer des appels vers des points de terminaison [!DNL Platform] Le didacticiel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform], y compris celles appartenant à [!DNL Data Governance], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant une payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Ressources de base ou personnalisées

Dans l&#39;API [!DNL Policy Service], toutes les stratégies et actions marketing sont appelées ressources `core` ou `custom`.

`core` les ressources sont celles définies et maintenues par l&#39;Adobe, tandis que les  `custom` ressources sont celles créées et entretenues par votre organisation et sont donc uniques et visibles uniquement par votre organisation IMS. Les opérations de liste et de recherche (`GET`) sont donc les seules opérations autorisées sur les ressources `core`, alors que les opérations de liste, de recherche et de mise à jour (`POST`, `PUT`, `PATCH` et `DELETE`) sont disponibles pour les ressources `custom`.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API de service de stratégie, sélectionnez l’un des guides de points de terminaison disponibles.
