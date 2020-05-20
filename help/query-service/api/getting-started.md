---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide du développeur Requête Service
topic: query templates
translation-type: tm+mt
source-git-commit: 91104399e50bce03fed7c9196e6e83fc48a54d1c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Guide du développeur Requête Service

Ce guide du développeur décrit les étapes à suivre pour effectuer diverses opérations dans l’API Adobe Experience Platform Requête Service.

## Prise en main

Ce guide nécessite une bonne compréhension des différents services Adobe Experience Platform impliqués dans l’utilisation de Requête Service.

- [Requête Service](../home.md): Permet de requête des jeux de données et de capturer les requêtes résultantes en tant que nouveaux jeux de données dans la plateforme d’expérience.
- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour utiliser Requête Service avec succès à l’aide de l’API.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans cette documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme d’expérience, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API de plate-forme, comme indiqué ci-dessous :

- Autorisation : `Bearer {ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur l’utilisation de sandbox dans Experience Platform, voir la documentation [d’aperçu des](../../sandboxes/home.md)sandbox.

## Exemples d’appels d’API

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Requête Service. Les documents suivants passent en revue les différents appels d’API que vous pouvez effectuer à l’aide de l’API Requête Service. Chaque exemple d’appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

- [Requêtes](queries.md)
- [Paramètres de connexion](connection-parameters.md)
- [requêtes planifiées](scheduled-queries.md)
- [S’exécute pour les requêtes planifiées.](runs-scheduled-queries.md)
- [Modèles de Requête](query-templates.md)

## Étapes suivantes

Maintenant que vous avez appris à passer des appels à l’aide de l’API Requête Service, vous pouvez créer vos propres requêtes non interactives. Pour plus d&#39;informations sur la création de requêtes, consultez le guide [de référence](../sql/overview.md)SQL.