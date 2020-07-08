---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Prise en main de l’API Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: d1656635b6d082ce99f1df4e175d8dd69a63a43a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Prise en main de l’API Profil client en temps réel {#getting-started}

L’API Profil client en temps réel vous permet d’effectuer des opérations CRUD de base sur des ressources de Profil, telles que la configuration d’attributs calculés, l’accès aux entités, l’exportation de données de Profil et la suppression de jeux de données ou de lots inutiles.

L&#39;utilisation du guide du développeur nécessite une compréhension pratique des différents services d&#39;Adobe Experience Platform impliqués dans l&#39;utilisation des données de Profil. Avant de commencer à utiliser l’API Profil client en temps réel, consultez la documentation relative aux services suivants :

* [Profil](../home.md)client en temps réel : Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Obtenez une meilleure vue de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes.
* [Service](../../segmentation/home.md)de segmentation des Adobes Experience Platform : Permet de créer des segments d’audience à partir des données du Profil client en temps réel.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance Platform unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les points de terminaison de l&#39;API de Profil.

## Lecture des exemples d’appels d’API

La documentation de l’API Profil client en temps réel fournit des exemples d’appels d’API pour montrer comment formater correctement les requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

## En-têtes requis

La documentation de l’API exige également que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin d’effectuer des appels vers les points de terminaison Platform. Le didacticiel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans les appels d&#39;API Experience Platform, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de l&#39;Experience Platform sont isolées dans des sandbox virtuels spécifiques. Les requêtes aux API Platform nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes avec une charge utile dans le corps de la requête (telles que les appels POST, PUT et PATCH) doivent inclure un `Content-Type` en-tête. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API Profil client en temps réel, sélectionnez l’un des guides de points de terminaison disponibles.