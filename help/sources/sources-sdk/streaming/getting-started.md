---
title: Prise en main des sources en libre-service (streaming de SDK)
description: Ce document présente les informations préalables que vous devez connaître avant d’essayer de créer une source à l’aide de sources en libre-service (streaming SDK).
exl-id: 6cc13279-ce0b-45bc-ad25-e2e6aafc2af0
badge: Beta
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 20%

---

# Prise en main des sources en libre-service (streaming de SDK)

>[!NOTE]
>
>La diffusion en continu de SDK par les sources en libre-service est en version bêta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Sources en libre-service (streaming SDK) vous permet d’intégrer votre propre source pour importer des données de streaming dans Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Aperçu général de la configuration

Le processus détaillé de configuration de votre source dans Experience Platform est décrit ci-dessous :

### Intégration

* [Créer une spécification de connexion pour la diffusion en continu de SDK](create.md).
* [Mettez à jour la spécification de flux de streaming avec votre nouvel identifiant de spécification de connexion](update-flow-specs.md).
* [Test et envoi de la source de streaming](submit.md).

### Documentation

* Pour commencer à documenter votre source, lisez la [présentation de la création de documentation pour les sources en libre-service](../documentation/doc-overview.md).
* Lisez le guide sur [à l’aide de l’interface web GitHub](../documentation/github.md) pour savoir comment créer de la documentation à l’aide de GitHub.
* Lisez le guide sur [à l’aide d’un éditeur de texte](../documentation/text-editor.md) pour savoir comment créer de la documentation à l’aide de votre ordinateur local.
* [Utilisez le modèle de documentation API Streaming SDK pour documenter votre source dans l’API](streaming-template-api.md).
* [Utilisez le modèle de documentation de l’interface utilisateur de streaming SDK pour documenter votre source dans l’interface utilisateur](streaming-template-ui.md).

Vous pouvez également télécharger les modèles de documentation ci-dessous :

* [Modèle de documentation de l’API](../assets/streaming/streaming-template-api.zip)
* [Modèle de documentation de l’interface utilisateur](../assets/streaming/streaming-template-ui.zip)

## Conditions préalables

>[!IMPORTANT]
>
>La source que vous intégrez à Experience Platform doit pouvoir prendre en charge un webhook auquel un point d’entrée peut être abonné pour envoyer des mises à jour.

Pour utiliser des sources en libre-service (streaming SDK), vous devez vous assurer que vous avez accès à une organisation de sandbox configurée avec des sources Adobe Experience Platform.

Ce guide nécessite également une connaissance pratique des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Lecture d’exemples d’appels API

La documentation des sources en libre-service (streaming SDK) et de l’API [!DNL Flow Service] fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API Experience Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Toutes les ressources d’Experience Platform, y compris celles appartenant à [!DNL Flow Service], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API Experience Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Experience Platform, consultez la [documentation sur les sandbox](../../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

* `Content-Type: application/json`

## Étapes suivantes

Pour commencer à créer une source avec des sources en libre-service (streaming SDK), consultez le tutoriel sur [la création d’une source](./create.md).
