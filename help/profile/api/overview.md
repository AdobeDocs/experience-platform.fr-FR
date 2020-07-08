---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide de développement de l’API Real-time Customer Profile
topic: guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 2%

---


# Guide de développement de l’API Real-time Customer Profile

Le Profil client en temps réel vous permet de voir une vue holistique de chacun de vos clients individuels dans l’Adobe Experience Platform. Profil vous permet de consolider des données clients disparates provenant de plusieurs canaux, tels que des données en ligne, hors ligne, de gestion de la relation client et tierces, en une vue unifiée offrant un compte interactif horodaté de chaque interaction client.

L’API Profil client en temps réel comprend plusieurs points de terminaison, décrits ci-dessous. Consultez les guides des points de terminaison individuels pour plus de détails et consultez le guide [de](getting-started.md) prise en main pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, reportez-vous à la page swagger [de référence des API de Profil client en temps](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)réel.

## (Alpha) Attributs calculés

>[!IMPORTANT]
>
>
>La fonctionnalité d’attribut calculé est en alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent être modifiées.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agrégat des valeurs sur tous les enregistrements et événements. Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de profil ou dans un événement. Ces calculs vous permettent de répondre facilement aux questions relatives à des éléments tels que la valeur d’achat sur toute la durée de vie, le délai entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que les informations sont nécessaires. Vous pouvez créer, vue, modifier et supprimer des attributs calculés à l’aide du point de `config/computedAttributes` terminaison. Pour savoir comment utiliser ce point de terminaison, consultez le guide [des attributs](computed-attributes.md)calculés.

## Projections Edge

L’Adobe Experience Platform permet la personnalisation en temps réel des expériences client en rendant les données facilement accessibles sur des serveurs stratégiquement situés appelés &quot;arêtes&quot;. L’API Profil client en temps réel fournit des points de terminaison pour travailler avec les arêtes via des composants appelés &quot;projections&quot;. Cela inclut les configurations de projection pour déterminer quelles données doivent être projetées sur chaque bord, ainsi que les destinations de projection pour définir où acheminer une projection. Pour obtenir des informations détaillées sur l&#39;utilisation des projections de bord, veuillez consulter le guide [des configurations de](edge-projections.md)projection et des points de terminaison de destination.

## Entités

Grâce à l’Adobe Experience Platform, vous pouvez accéder aux données du Profil client en temps réel à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées &quot;profils&quot;, à l&#39;aide de l&#39;API, suivez les étapes décrites dans le guide [des points de terminaison](entities.md)entités. Pour accéder aux profils à l’aide de l’interface utilisateur de Platform, reportez-vous au guide [d’utilisation du](../ui/user-guide.md)Profil.

## Stratégies de fusion

Lorsque vous rassemblez des données provenant de plusieurs sources dans l’Experience Platform, les stratégies de fusion sont les règles que Platform utilise pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer des profils clients individuels. L’API Profil client en temps réel vous permet de créer des stratégies de fusion, de gérer des stratégies existantes et de définir une stratégie de fusion par défaut pour votre entreprise. Pour en savoir plus sur l’utilisation des stratégies de fusion à l’aide de l’API, consultez le guide [des points de terminaison des stratégies de](merge-policies.md)fusion.

Pour obtenir un guide sur l’utilisation des stratégies de fusion à l’aide de l’interface utilisateur de Platform, consultez le guide [d’utilisation](../ui/merge-policies.md)Fusionner les stratégies.

## Tâches du système de Profil

Les données ingérées dans Platform sont stockées dans le lac Data ainsi que dans la banque de données du Profil client en temps réel. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot du magasin de Profils pour supprimer des données dont vous n&#39;avez plus besoin ou qui ont été ajoutées par erreur. Pour ce faire, il est nécessaire d&#39;utiliser l&#39;API pour créer une tâche Profil System, appelée &quot;demande de suppression&quot;, qui peut également être modifiée, surveillée ou supprimée si nécessaire. Pour savoir comment utiliser les requêtes de suppression à l’aide du `/system/jobs` point de terminaison dans l’API Profil client en temps réel, suivez les étapes décrites dans le guide [des points de terminaison des tâches du système de](profile-system-jobs.md)profil.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API Profil client en temps réel, lisez le guide [de prise en main de la](getting-started.md) prise en main, puis sélectionnez l’un des guides de points de terminaison pour savoir comment utiliser des points de terminaison spécifiques liés au Profil. Pour en savoir plus sur l’utilisation des données de Profil à l’aide de l’interface utilisateur de Platform, consultez le guide [d’utilisation du Profil client en temps](../ui/user-guide.md)réel.