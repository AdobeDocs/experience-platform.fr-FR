---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur de l’API de Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---


# Guide du développeur de l’API de Profil client en temps réel

Le Profil client en temps réel vous permet de voir une vue holistique de chacun de vos clients individuels dans Adobe Experience Platform. Profil vous permet de consolider des données clients disparates provenant de plusieurs canaux, tels que des données en ligne, hors ligne, de gestion de la relation client et tierces, en une vue unifiée offrant un compte interactif horodaté de chaque interaction client.

## Prise en main {#getting-started}

L’API Profil client en temps réel vous permet d’effectuer des opérations CRUD de base sur des ressources de Profil, telles que la configuration d’attributs calculés, l’accès aux entités, l’exportation de données de Profil et la suppression de jeux de données ou de lots inutiles.

L’utilisation de ce guide du développeur nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation des données de Profil. Avant de commencer à utiliser l’API Profil client en temps réel, consultez la documentation relative aux services suivants :

* [Profil](../home.md)client en temps réel : Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Obtenez une meilleure vue de vos clients et de leur comportement en rapprochant les identités entre les périphériques et les systèmes.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Permet de créer des segments d’audience à partir des données du Profil client en temps réel.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les points de terminaison de l&#39;API de Profil.

### Lecture des exemples d’appels d’API

La documentation de l’API Profil client en temps réel fournit des exemples d’appels d’API pour montrer comment formater correctement les requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### En-têtes requis

La documentation de l’API exige également que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin d’effectuer des appels vers les points de terminaison de la plate-forme. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes avec une charge utile dans le corps de la requête (telles que les appels POST, PUT et PATCH) doivent inclure un `Content-Type` en-tête. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

## (Alpha) Attributs calculés

>[!IMPORTANT]
>La fonctionnalité d’attribut calculé est en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent être modifiées.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agrégat des valeurs sur tous les enregistrements et événements.

Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de profil ou dans un événement. Ces calculs vous permettent de répondre facilement aux questions relatives à des éléments tels que la valeur d’achat sur toute la durée de vie, le délai entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que les informations sont nécessaires.

Vous pouvez créer, vue, modifier et supprimer des attributs calculés à l’aide des `config/computedAttributes` points de terminaison. Pour savoir comment utiliser ces points de terminaison, consultez le sous-guide [des attributs](computed-attributes.md)calculés.

## Projections Edge

Adobe Experience Platform permet la personnalisation en temps réel des expériences client en rendant les données facilement accessibles sur des serveurs stratégiquement situés appelés &quot;arêtes&quot;. L’API Profil client en temps réel fournit des points de terminaison pour travailler avec les arêtes via des composants appelés &quot;projections&quot;. Cela inclut les configurations de projection pour déterminer quelles données doivent être projetées sur chaque bord, ainsi que les destinations de projection pour définir où acheminer une projection.

Pour obtenir des informations détaillées sur l&#39;utilisation des projections de bord, veuillez consulter le sous-guide [des projections de](edge-projections.md)bord.

## Entités

Adobe Experience Platform vous permet d’accéder aux données du Profil client en temps réel à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées &quot;profils&quot;, à l&#39;aide de l&#39;API, suivez les étapes décrites dans le sous-guide [](entities.md)Entités.

## Stratégies de fusion

Lorsque vous rassemblez des données provenant de plusieurs sources dans Experience Platform, les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer des profils clients individuels.

L’API Profil client en temps réel vous permet de créer des stratégies de fusion, de gérer des stratégies existantes et de définir une stratégie de fusion par défaut pour votre entreprise. Pour en savoir plus sur l’utilisation des stratégies de fusion à l’aide de l’API, consultez le sous-guide [Stratégies de](merge-policies.md)fusion.

Pour obtenir un guide sur l’utilisation des stratégies de fusion à l’aide de l’interface utilisateur de la plate-forme, consultez le guide [d’utilisateur](../ui/merge-policies.md)Fusionner les stratégies.

## Recherche de Profil

La recherche par Profil permet de rechercher et d’indexer des champs configurables contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche par Profil, consultez le sous-guide [de recherche](profile-search.md)

## Tâches du système de Profil

Les données ingérées dans Platform sont stockées dans Data Lake ainsi que dans le magasin de données du Profil client en temps réel. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot du magasin de Profils pour supprimer des données dont vous n&#39;avez plus besoin ou qui ont été ajoutées par erreur. Pour ce faire, il est nécessaire d&#39;utiliser l&#39;API pour créer une tâche Profil System, appelée &quot;demande de suppression&quot;, qui peut également être modifiée, surveillée ou supprimée si nécessaire.

Pour savoir comment utiliser les requêtes de suppression à l’aide des `/system/jobs` points de terminaison de l’API Profil client en temps réel, suivez les étapes décrites dans le sous-guide [des tâches du système de](profile-system-jobs.md)profil.

## Étapes suivantes

Pour commencer à passer des appels à l’aide de l’API Profil client en temps réel, sélectionnez l’un des sous-guides pour savoir comment utiliser des points de terminaison spécifiques liés au Profil. Pour en savoir plus sur l’utilisation des données de Profil à l’aide de l’interface utilisateur de la plate-forme, consultez le guide [d’utilisation du Profil client en temps](../ui/user-guide.md)réel.