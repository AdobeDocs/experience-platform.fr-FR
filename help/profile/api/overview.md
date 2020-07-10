---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide de développement de l’API Real-time Customer Profile
topic: guide
translation-type: tm+mt
source-git-commit: c0b059d6654a98b74be5bc6a55f360c4dc2f216b
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 68%

---


# Guide de développement de l’API Real-time Customer Profile

Real-time Customer Profile offre une vue d’ensemble de chaque client dans Adobe Experience Platform. Profile vous permet de consolider diverses données clients provenant de plusieurs canaux, comme les données en ligne, hors ligne, CRM et tierces, en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

L’API Profil client en temps réel comprend plusieurs points de terminaison, décrits ci-dessous. Consultez les guides des points de terminaison individuels pour plus de détails et consultez le guide [de](getting-started.md) prise en main pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, reportez-vous à la page swagger [de référence des API de Profil client en temps](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)réel.

## (Alpha) Attributs calculés

>[!IMPORTANT]
>
>
>La fonctionnalité des attributs calculés est une version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent faire l’objet de modifications.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agréger des valeurs sur tous les enregistrements et tous les événements. Chaque attribut calculé contient une expression, ou « règle », qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil ou dans un événement. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. You can create, view, edit, and delete computed attributes using the `config/computedAttributes` endpoint. Pour savoir comment utiliser ce point de terminaison, consultez le guide [des attributs](computed-attributes.md)calculés.

## Projections de périphérie

Adobe Experience Platform permet de personnaliser en temps réel les expériences client en rendant les données facilement accessibles sur des serveurs situés stratégiquement, appelés « périphéries ». L’API Real-time Customer Profile fournit des points de terminaison pour utiliser les périphéries par le biais de composants appelés « projections ». Cela inclut des configurations de projection permettant de définir quelles données doivent être projetées sur chaque périphérie, ainsi que des destinations de projection permettant de déterminer la direction d’une projection. Pour obtenir des informations détaillées sur l&#39;utilisation des projections de bord, veuillez consulter le guide [des configurations de](edge-projections.md)projection et des points de terminaison de destination.

## Entités (accès au profil) {#entities}

Adobe Experience Platform vous permet d’accéder aux données de Real-time Customer Profile à l’aide des API RESTful ou de l’interface utilisateur. To learn how to access entities, more commonly known as &quot;profiles&quot;, using the API, follow the steps outlined in the [entities endpoint guide](entities.md). Pour accéder aux profils à l’aide de l’interface utilisateur de Platform, reportez-vous au guide [d’utilisation du](../ui/user-guide.md)Profil.

## Stratégies de fusion

Lorsque vous rassemblez des données provenant de plusieurs sources dans Experience Platform, les stratégies de fusion sont les règles utilisées par Platform pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer des profils clients individuels. Grâce à l’API Real-time Customer Profile, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation. To learn more about working with merge policies using the API, please visit the [merge policies endpoint guide](merge-policies.md).

Pour obtenir un guide sur l’utilisation des stratégies de fusion avec l’interface utilisateur de Platform, consultez le [guide d’utilisation des stratégies de fusion](../ui/merge-policies.md).

## Tâches de système Profile

Les données ingérées dans Platform sont stockées dans le lac de données, ainsi que dans la banque de données de Real-time Customer Profile. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot de la banque de profils pour supprimer les données devenues inutiles ou ajoutées par erreur. Pour ce faire, il est nécessaire d’utiliser l’API afin de créer une tâche de système Profile, appelée « requête de suppression », qui peut également être modifiée, surveillée ou supprimée si nécessaire. To learn how to work with delete requests using the `/system/jobs` endpoint in the Real-time Customer Profile API, follow the steps outlined in the [profile system jobs endpoint guide](profile-system-jobs.md).

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API Profil client en temps réel, lisez le guide [de prise en main de la](getting-started.md) prise en main, puis sélectionnez l’un des guides de points de terminaison pour savoir comment utiliser des points de terminaison spécifiques liés au Profil. Pour plus d’informations sur l’utilisation des données de Profile avec l’interface utilisateur de Platform, consultez le [guide d’utilisation de Real-time Customer Profile](../ui/user-guide.md).