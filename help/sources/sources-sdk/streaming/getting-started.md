---
title: Prise en main des sources en libre-service (SDK de diffusion en continu)
description: Ce document présente les informations prérequises que vous devez connaître avant de tenter de créer une source à l’aide de sources en libre-service (SDK de diffusion).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Version bêta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 34%

---

# Prise en main des sources en libre-service (SDK de diffusion en continu)

>[!NOTE]
>
>Le SDK de diffusion en continu des sources en libre-service est en version bêta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Les sources en libre-service (SDK de diffusion en continu) vous permettent d’intégrer votre propre source pour importer des données en continu dans Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant de lancer des appels à l’ [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Aperçu général de la configuration

Le processus étape par étape de configuration de votre source dans Experience Platform est décrit ci-dessous :

### Intégration

* [ Créez une spécification de connexion pour le SDK de diffusion en continu ](create.md).
* [Mettez à jour la spécification de flux de diffusion en continu avec votre nouvel ID de spécification de connexion](update-flow-specs.md).
* [Testez et envoyez votre source de diffusion en continu](submit.md).

### Documentation

* Pour commencer à documenter votre source, consultez la [présentation sur la création de documentation pour les sources en libre-service](../documentation/doc-overview.md).
* Lisez le guide sur [l’utilisation de l’interface web GitHub](../documentation/github.md) pour savoir comment créer de la documentation à l’aide de GitHub.
* Lisez le guide sur [l’utilisation d’un éditeur de texte](../documentation/text-editor.md) pour savoir comment créer de la documentation à l’aide de votre ordinateur local.
* [Utilisez le modèle de documentation de l’API du SDK de diffusion en continu pour documenter votre source dans l’API ](streaming-template-api.md).
* [Utilisez le modèle de documentation de l’interface utilisateur du SDK de diffusion en continu pour documenter votre source dans l’interface utilisateur ](streaming-template-ui.md).

Vous pouvez également télécharger les modèles de documentation ci-dessous :

* [Modèle de documentation d’API](../assets/streaming/streaming-template-api.zip)
* [Modèle de documentation de l’interface utilisateur](../assets/streaming/streaming-template-ui.zip)

## Conditions préalables

>[!IMPORTANT]
>
>Pour envoyer des mises à jour, la source intégrée à Experience Platform doit pouvoir prendre en charge un webhook auquel un point de terminaison peut être abonné.

Pour utiliser des sources en libre-service (SDK de diffusion en continu), vous devez vous assurer que vous avez accès à une organisation d’environnement de test configurée avec des sources Adobe Experience Platform.

Ce guide nécessite également une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Lecture d’exemples d’appels API

La documentation des sources en libre-service (SDK de diffusion en continu) et de l’API [!DNL Flow Service] fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources de Platform, y compris celles appartenant à [!DNL Flow Service], sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans Platform, consultez la [documentation sur les environnements de test](../../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Étapes suivantes

Pour commencer à créer une source avec des sources en libre-service (SDK de diffusion en continu), consultez le tutoriel sur la [création d’une source](./create.md).
