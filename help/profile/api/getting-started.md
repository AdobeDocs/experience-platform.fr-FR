---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API
title: Prise en main de l’API Profil client en temps réel
topic: guide
type: Documentation
description: Le guide de prise en main de l’API de Profil décrit les concepts clés et les fonctionnalités de base que vous devez connaître pour utiliser les points de terminaison de l’API de Profil client en temps réel afin d’effectuer des opérations CRUD de base sur les données de Profil.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 28%

---


# Prise en main de l’API [!DNL Real-time Customer Profile] {#getting-started}

Les points de terminaison de l’API Profil client en temps réel vous permettent d’effectuer des opérations CRUD de base sur des données de Profil, telles que la configuration d’attributs calculés, l’accès aux entités, l’exportation de données de Profil et la suppression de jeux de données ou de lots inutiles.

L&#39;utilisation du guide du développeur nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l&#39;utilisation de [!DNL Profile] données. Avant de commencer à travailler avec l&#39;API [!DNL Real-time Customer Profile], consultez la documentation relative aux services suivants :

* [[!DNL Real-time Customer Profile]](../home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Obtenez une meilleure vue de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md) : permet de créer des segments d’audience à partir de données Real-time Customer Profile.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
* [[!DNL Sandboxes]](../../sandboxes/home.md):  [!DNL Experience Platform] fournit des sandbox virtuels qui partitionnent une  [!DNL Platform] instance unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les points de terminaison de l&#39;API [!DNL Profile].

## Lecture d’exemples d’appels API

La documentation de l&#39;API [!DNL Real-time Customer Profile] fournit des exemples d&#39;appels d&#39;API pour montrer comment formater correctement les requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en) pour lancer des appels vers des points de terminaison [!DNL Platform] Le didacticiel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

## Étapes suivantes

Pour commencer à effectuer des appels à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile], sélectionnez l&#39;un des guides de points de terminaison disponibles.