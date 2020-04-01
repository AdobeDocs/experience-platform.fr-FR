---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur d’API  client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Guide du développeur d’API  client en temps réel

Le  Client en temps réel vous permet de voir un holistique de chacun de vos clients individuels dans Adobe Experience Platform. Les  de vous permettent de consolider les données clients disparates issues de plusieurs  de, telles que les données en ligne, hors ligne, CRM et tierces, dans uncompte unifié offrant un compte d’activité horodaté de chaque interaction client.

## Prise en main {#getting-started}

Grâce à l’API  client en temps réel, vous pouvez effectuer des opérations CRUD de base sur des ressources de , telles que la configuration d’attributs calculés, l’accès aux entités, l’exportation de données de la base de données et la suppression de jeux ou de lots de données inutiles.

L’utilisation de ce guide du développeur nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation des données  des. Avant de commencer à travailler avec l’API  client en temps réel, consultez la documentation pour les services suivants :

* [](../home.md)du client en temps réel : Fournit un client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Obtenez un meilleur de votre client et de son comportement en rapprochant les identités entre les périphériques et les systèmes.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Permet de créer  segments  à partir de données de client en temps réel.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
* [Sandbox](../../sandboxes/home.md): Experience Platform fournit des sandbox virtuels qui partitionnent une instance de plateforme unique en un  virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels vers des points de fin d’API .

### Lecture des exemples d’appels d’API

La documentation de l’API  client en temps réel fournit des exemples d’appels d’API pour démontrer comment formater correctement les requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### En-têtes obligatoires

La documentation de l’API exige également que vous ayez suivi le didacticiel [d’](../../tutorials/authentication.md) authentification afin d’effectuer des appels vers les points de fin de plateforme. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

* Autorisation : Porteur `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Les demandes d’API de plateforme nécessitent un en-tête qui spécifie le nom du sandbox dans lequel l’opération aura lieu :

* x-sandbox-name : `{SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes avec une charge utile dans le corps de la requête (telles que les appels POST, PUT et PATCH) doivent inclure un `Content-Type` en-tête. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

## (Alpha) Attributs calculés

>[!IMPORTANT]
>La fonctionnalité d’attribut calculé est en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent être modifiées.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et  de . Les attributs calculés fonctionnent au niveau  du, ce qui signifie que vous pouvez  des valeurs de sur tous les enregistrements et tous les.

Chaque attribut calculé contient un  de , ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de ou dans un. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat sur la durée de vie, le délai entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que les informations sont nécessaires.

Vous pouvez créer, , modifier et supprimer des attributs calculés à l’aide des `config/computedAttributes` points de fin. Pour savoir comment utiliser ces points de fin, consultez le sous-guide [des attributs](computed-attributes.md)calculés.

## Projections Edge

Adobe Experience Platform permet la personnalisation en temps réel des expériences client en rendant les données facilement accessibles sur des serveurs stratégiquement situés appelés &quot;arêtes&quot;. L’API  client en temps réel fournit des points de terminaison pour travailler avec les bords via des composants appelés &quot;projections&quot;. Cela inclut les configurations de projection pour déterminer quelles données doivent être projetées sur chaque bord, ainsi que les destinations de projection pour définir où acheminer une projection.

Pour obtenir des renseignements détaillés sur l&#39;utilisation des projections de bord, veuillez consulter le sous-guide [des projections de](edge-projections.md)bord.

## Entités

Adobe Experience Platform vous permet d’accéder aux données de client en temps réel à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées &quot;&quot;, à l’aide de l’API, suivez les étapes décrites dans le sous-guide [](entities.md)Entités.

## Stratégies de fusion

Lorsque vous rassemblez des données provenant de plusieurs sources dans Experience Platform, les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer la priorité des données et les données qui seront combinées pour créer des  clients individuels.

Grâce à l’API  client en temps réel, vous pouvez créer de nouvelles stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Pour en savoir plus sur l’utilisation des stratégies de fusion à l’aide de l’API, consultez le sous-guide [Stratégies de](merge-policies.md)fusion.

Pour obtenir un guide sur l’utilisation des stratégies de fusion à l’aide de l’interface utilisateur de la plate-forme, consultez le guide [d’utilisation des stratégies de](../ui/merge-policies.md)fusion.

## de recherche

La recherche de  permet de rechercher et d’indexer des champs configurables contenus dans diverses sources de données et de les renvoyer en temps quasi réel. Pour commencer à utiliser la recherche , reportez-vous au sous-guide de [recherche](profile-search.md)

## Tâches  système

Les données ingérées dans Platform sont stockées dans Data Lake, ainsi que dans le magasin de données  du client en temps réel. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot du magasin de  pour supprimer des données dont vous n’avez plus besoin ou qui ont été ajoutées par erreur. Pour ce faire, vous devez utiliser l’API pour créer une tâche système de , connue sous le nom de &quot;demande de suppression&quot;, qui peut également être, modifiée, surveillée ou supprimée si nécessaire.

Pour savoir comment utiliser les demandes de suppression à l’aide des `/system/jobs` points de fin de l’API de client en temps réel, suivez les étapes décrites dans le sous-guide [des tâches du système de ](profile-system-jobs.md).

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API  client en temps réel, sélectionnez l’un des sous-guides afin d’apprendre à utiliser des points de terminaison spécifiques liés aux  de. Pour en savoir plus sur l’utilisation des données de  à l’aide de l’interface utilisateur de la plateforme, consultez le guide [d’utilisation du de clients en temps](../ui/user-guide.md)réel.