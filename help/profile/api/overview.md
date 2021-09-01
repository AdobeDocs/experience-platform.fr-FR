---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;profil unifié;profil unifié;unifié;profil;unifié;profil;rtcp;activer le profil;activer le profil
title: Guide de l’API Real-time Customer Profile
description: L’API Real-time Customer Profile permet aux développeurs d’explorer et d’utiliser les données de profil, notamment d’afficher les profils, de créer et de mettre à jour des stratégies de fusion, d’exporter ou d’échantillonner des données de profil, ainsi que de supprimer les données de profil qui ne sont plus requises ou qui ont été ajoutées par erreur. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: b2ae2b4ca2efe606aa148e06ca988a6285bedfee
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 27%

---

# Guide de l’API [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] offre une vue d’ensemble de chaque client dans Adobe Experience Platform. [!DNL Profile] vous permet de consolider diverses données clients provenant de plusieurs canaux, comme les données en ligne, hors ligne, CRM et tierces, en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

L’API [!DNL Real-time Customer Profile] comprend plusieurs points de terminaison, décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points de terminaison disponibles et les opérations CRUD, consultez le [swagger de référence de l’API Real-time Customer Profile](https://www.adobe.com/go/profile-apis-en).

Pour obtenir un guide sur l’utilisation des données [!DNL Real-time Customer Profile] dans l’interface utilisateur [!DNL Experience Platform], reportez-vous au [Guide d’utilisation du profil](../ui/user-guide.md).

## (Alpha) Attributs calculés {#computed-attributes}

>[!IMPORTANT]
>
>La fonctionnalité des attributs calculés est une version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent faire l’objet de modifications.

Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation.

Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Ces valeurs d’attribut calculées peuvent ensuite être visualisées dans un profil, utilisées pour créer un segment ou accessibles via plusieurs modèles d’accès différents.

Vous pouvez créer, afficher, modifier et supprimer des attributs calculés à l’aide du point de terminaison `config/computedAttributes`. Pour savoir comment utiliser les attributs calculés, consultez la [présentation des attributs calculés](../computed-attributes/overview.md). Pour les opérations d’API, consultez le [guide de point d’entrée de l’API des attributs calculés](../computed-attributes/ca-api.md).

## Projections de périphérie {#edge-projections}

Adobe Experience Platform permet de personnaliser en temps réel les expériences client en rendant les données facilement accessibles sur des serveurs situés stratégiquement, appelés « périphéries ». L’API [!DNL Real-time Customer Profile] fournit des points de terminaison pour utiliser les périphéries par le biais de composants appelés &quot;projections&quot;. Cela inclut des configurations de projection permettant de définir quelles données doivent être projetées sur chaque périphérie, ainsi que des destinations de projection permettant de déterminer la direction d’une projection. Pour plus d’informations sur l’utilisation des projections de périphérie, consultez le [guide des configurations de projection et des points de terminaison de destinations](edge-projections.md).

## Entités (accès au [!DNL Profile]) {#entities}

Grâce à Adobe Experience Platform, vous pouvez accéder aux données [!DNL Real-time Customer Profile] à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées &quot;profils&quot;, à l’aide de l’API, suivez les étapes décrites dans le [guide des points d’entrée des entités](entities.md). Pour accéder aux profils à l’aide de l’interface utilisateur [!DNL Platform], consultez le [Guide de l’utilisateur du profil](../ui/user-guide.md).

## Tâches d’exportation (exportation de [!DNL Profile]) {#profile-export}

[!DNL Real-time Customer Profile] les données peuvent être exportées vers un jeu de données pour un traitement ultérieur, par exemple pour l’exportation de segments d’audience en vue de l’activation ou d’attributs de profil pour la création de rapports. Les tâches d’exportation pour les segments ciblés font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Pour en savoir plus, consultez le [guide de point de terminaison des tâches d’exportation de segmentation](../../profile/api/export-jobs.md). Pour obtenir des instructions détaillées sur la création et la gestion des tâches d’exportation pour les attributs de profil, consultez le [guide de point de terminaison des tâches d’exportation](export-jobs.md).

## Stratégies de fusion {#merge-policies}

Lorsque vous rassemblez des données provenant de plusieurs sources dans [!DNL Experience Platform], les stratégies de fusion sont les règles utilisées par [!DNL Platform] pour déterminer la priorité des données et les données qui seront combinées pour créer des profils client individuels. À l’aide de l’API [!DNL Real-time Customer Profile], vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation. Pour utiliser des stratégies de fusion à l’aide de l’API, consultez le [guide de point de terminaison des stratégies de fusion](merge-policies.md).

Pour en savoir plus sur les stratégies de fusion et leur rôle dans Platform, commencez par lire la [présentation des stratégies de fusion](../merge-policies/overview.md).

## Prévisualisation des exemples de statut (prévisualisation du [!DNL Profile]) {#profile-preview}

Lorsque des données sont ingérées dans Platform, un exemple de tâche est exécuté pour mettre à jour le nombre de profils et d’autres mesures liées aux données de Real-time Customer Profile. Les résultats de cet exemple de tâche peuvent être visualisés à l’aide du point de terminaison `/previewsamplestatus`, qui fait partie de l’API Real-time Customer Profile. Ce point de terminaison peut également être utilisé pour répertorier les distributions de profil par jeu de données et espace de noms d’identité, ainsi que pour générer plusieurs rapports afin de mieux comprendre la composition de la banque de profils de votre entreprise.  Pour commencer à utiliser le point d’entrée `/profilepreviewstatus`, reportez-vous au [guide d’aperçu du point d’entrée d’état ](preview-sample-status.md).

## Tâches de système Profile {#profile-system-jobs}

Les données activées pour le profil qui sont ingérées dans [!DNL Platform] sont stockées dans [!DNL Data Lake] ainsi que dans l’entrepôt de données [!DNL Real-time Customer Profile]. Il peut parfois être nécessaire de supprimer un jeu de données ou un lot du magasin [!DNL Profile] pour supprimer les données dont vous n’avez plus besoin ou qui ont été ajoutées par erreur. Pour ce faire, il est nécessaire d’utiliser l’API afin de créer une balise [!DNL Profile System Job], également appelée &quot;[!DNL delete request]&quot;, qui peut être modifiée, surveillée ou supprimée si nécessaire. Pour savoir comment utiliser les requêtes de suppression à l’aide du point de terminaison `/system/jobs` de l’API [!DNL Real-time Customer Profile], suivez les étapes décrites dans le [guide de terminaison des tâches du système de profil](profile-system-jobs.md).

## Étapes suivantes {#next-steps}

Pour commencer à lancer des appels à l’aide de l’API [!DNL Real-time Customer Profile], lisez le [guide de prise en main](getting-started.md) , puis sélectionnez l’un des guides des points de terminaison pour savoir comment utiliser des points de terminaison spécifiques [!DNL Profile]. Pour utiliser les données [!DNL Profile] à l’aide de l’interface utilisateur [!DNL Experience Platform], consultez le [guide d’utilisation de Real-time Customer Profile](../ui/user-guide.md).
