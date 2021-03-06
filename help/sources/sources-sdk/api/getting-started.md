---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Prise en main du SDK de sources (version bêta)
topic-legacy: developer guide
description: Ce document présente les informations prérequises que vous devez connaître avant de tenter de créer une source à l’aide du SDK Sources.
hide: true
hidefromtoc: true
exl-id: ba131442-ff20-4854-87fe-918aa313382d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 57%

---

# Prise en main du SDK de sources (version bêta)

>[!IMPORTANT]
>
>Le SDK Sources est actuellement en version Beta et votre organisation n’y a peut-être pas encore accès. Les fonctionnalités décrites dans cette documentation peuvent changer.

Le SDK Sources vous permet d’intégrer votre propre source REST pour importer des données dans Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels au [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Conditions préalables

Pour utiliser le SDK Sources, vous devez vous assurer que vous avez accès à un environnement de test d’organisation IMS fourni avec les sources Adobe Experience Platform.

Ce guide nécessite également une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Lecture d’exemples d’appels API

Le SDK Sources et [!DNL Flow Service] La documentation des API fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources de Platform, y compris celles appartenant à [!DNL Flow Service], sont isolés dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans Platform, voir [documentation sandbox](../../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Étapes suivantes

Pour commencer à créer une source avec le SDK Sources, consultez le tutoriel sur [création d’une source](./create.md).
