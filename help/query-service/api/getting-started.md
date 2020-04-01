---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Guide du développeur du service '
topic: query templates
translation-type: tm+mt
source-git-commit: 91104399e50bce03fed7c9196e6e83fc48a54d1c

---


# Guide du développeur du service 

Ce guide du développeur décrit les étapes à suivre pour effectuer diverses opérations dans l’API du service de Adobe Experience Platform.

## Prise en main

Ce guide nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation du service de  de.

- [Service](../home.md) : Permet de des jeux de données et de capturer le résultant  sous forme de nouveaux jeux de données dans la plateforme d’expérience.
- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
- [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir utiliser le service de  à l’aide de l’API.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans cette documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme d’expérience, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme, comme illustré ci-dessous :

- Autorisation : `Bearer {ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur l’utilisation de sandbox dans Experience Platform, voir la documentation [d’aperçu des](../../sandboxes/home.md)sandbox.

## Exemples d’appels d’API

Maintenant que vous comprenez les en-têtes à utiliser, vous êtes prêt à commencer à lancer des appels à l’API du service . Le suivant  les différents appels d’API que vous pouvez effectuer à l’aide de l’API de service . Chaque exemple d’appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

- [Requêtes](queries.md)
- [Paramètres de connexion](connection-parameters.md)
- [de planifié](scheduled-queries.md)
- [S’exécute pour les  planifiées](runs-scheduled-queries.md)
- [Modèle](query-templates.md)

## Étapes suivantes

Maintenant que vous avez appris à lancer des appels à l’aide de l’API du service , vous pouvez créer votre propre  non interactif. Pour plus d&#39;informations sur la création de  de, veuillez lire le guide [de référence](../sql/overview.md)SQL.