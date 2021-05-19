---
keywords: Experience Platform ; profil ; profil client en temps réel ; résolution des problèmes ; API ; profil unifié ; Profil unifié ; unifié ; Profil ; rtcp ; activer le profil ; Activer le profil
title: Guide de l’API de Profil client en temps réel
description: L’API Profil client en temps réel permet aux développeurs d’explorer et d’utiliser des données de Profil, y compris des profils de vue, de créer et de mettre à jour des stratégies de fusion, d’exporter ou d’échantillonner des données de Profil et de supprimer des données de Profil qui ne sont plus requises ou qui ont été ajoutées par erreur. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 77bf6f4634987900bea1280290e8049120bb8856
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 19%

---

# [!DNL Real-time Customer Profile] Guide des API

[!DNL Real-time Customer Profile] offre une vue d’ensemble de chaque client dans Adobe Experience Platform. [!DNL Profile] vous permet de consolider diverses données clients provenant de plusieurs canaux, comme les données en ligne, hors ligne, CRM et tierces, en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

L&#39;API [!DNL Real-time Customer Profile] comprend plusieurs points de terminaison, décrits ci-dessous. Consultez les guides individuels des points de terminaison pour plus de détails et consultez le [guide de prise en main](getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, consultez la [swagger de référence d’API de Profil client en temps réel ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Pour obtenir un guide sur l&#39;utilisation des données [!DNL Real-time Customer Profile] dans l&#39;interface utilisateur [!DNL Experience Platform], consultez le [Profil user guide](../ui/user-guide.md).

## (Alpha) Attributs calculés {#computed-attributes}

>[!IMPORTANT]
>
>La fonctionnalité des attributs calculés est une version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent faire l’objet de modifications.

Les attributs calculés sont des fonctions utilisées pour agrégat des données au niveau du événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation.

Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de profil. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Ces valeurs d’attribut calculées peuvent ensuite être visualisées dans un profil, utilisées pour créer un segment ou accessibles via plusieurs modèles d’accès différents.

Vous pouvez créer, vue, modifier et supprimer des attributs calculés à l’aide du point de terminaison `config/computedAttributes`. Pour savoir comment utiliser les attributs calculés, consultez l&#39;[aperçu des attributs calculés](../computed-attributes/overview.md). Pour les opérations d’API, consultez le [guide du point de terminaison de l’API des attributs calculés](../computed-attributes/ca-api.md).

## Projections de périphérie {#edge-projections}

Adobe Experience Platform permet de personnaliser en temps réel les expériences client en rendant les données facilement accessibles sur des serveurs situés stratégiquement, appelés « périphéries ». L&#39;API [!DNL Real-time Customer Profile] fournit des points de terminaison pour travailler avec les arêtes via des composants appelés &quot;projections&quot;. Cela inclut des configurations de projection permettant de définir quelles données doivent être projetées sur chaque périphérie, ainsi que des destinations de projection permettant de déterminer la direction d’une projection. Pour obtenir des informations détaillées sur l&#39;utilisation des projections de bord, consultez le [guide des configurations de projection et des points de terminaison de destination](edge-projections.md).

## Entités ([!DNL Profile] accès) {#entities}

Grâce à Adobe Experience Platform, vous pouvez accéder aux données [!DNL Real-time Customer Profile] à l’aide des API RESTful ou de l’interface utilisateur. Pour savoir comment accéder aux entités, plus communément appelées &quot;profils&quot;, à l&#39;aide de l&#39;API, suivez les étapes décrites dans le [guide des points de terminaison d&#39;entités](entities.md). Pour accéder aux profils à l&#39;aide de l&#39;interface utilisateur [!DNL Platform], consultez le [Guide de l&#39;utilisateur du Profil](../ui/user-guide.md).

## Exporter des tâches ([!DNL Profile] export) {#profile-export}

[!DNL Real-time Customer Profile] les données peuvent être exportées dans un jeu de données en vue d’un traitement ultérieur, par exemple pour exporter des segments d’audience en vue d’une activation ou des attributs de profil en vue d’un rapports. Les tâches d’exportation pour les segments d’audience font partie de l’API [!DNL Adobe Experience Platform Segmentation Service]. Pour en savoir plus, consultez le [guide de point de terminaison des tâches d’exportation de segmentation](../../profile/api/export-jobs.md). Pour obtenir des instructions détaillées sur la création et la gestion des tâches d’exportation pour les attributs de profil, consultez le [guide de point de terminaison des tâches d’exportation](export-jobs.md).

## Stratégies de fusion {#merge-policies}

Lorsque vous rassemblez des données provenant de plusieurs sources dans [!DNL Experience Platform], les stratégies de fusion sont les règles que [!DNL Platform] utilise pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer des profils clients individuels. L&#39;API [!DNL Real-time Customer Profile] vous permet de créer des stratégies de fusion, de gérer des stratégies existantes et de définir une stratégie de fusion par défaut pour votre organisation. Pour en savoir plus sur l&#39;utilisation des stratégies de fusion à l&#39;aide de l&#39;API, consultez le [guide de point de terminaison des stratégies de fusion](merge-policies.md).

Pour obtenir un guide sur l&#39;utilisation des stratégies de fusion à l&#39;aide de l&#39;[!DNL Platform] interface utilisateur, consultez le [guide de l&#39;utilisateur des stratégies de fusion](../ui/merge-policies.md).

## État de l&#39;échantillon de prévisualisation ([!DNL Profile] prévisualisation) {#profile-preview}

Les données activées pour le Profil étant ingérées dans l’Experience Platform, elles sont stockées dans le magasin de données du Profil. À mesure que le nombre d’enregistrements dans la banque de Profils augmente ou diminue, une tâche d’exemple est exécutée qui comprend des informations sur le nombre de fragments de profil et de profils fusionnés présents dans la banque de données. L&#39;API de Profil vous permet de prévisualisation du dernier exemple réussi, ainsi que de la distribution de profil de liste par jeu de données et par espace de nommage d&#39;identité. Pour commencer à utiliser le point de terminaison `/profilepreviewstatus`, reportez-vous au [guide de l&#39;exemple de prévisualisation d&#39;état de point de terminaison](preview-sample-status.md).

## Tâches de système Profile {#profile-system-jobs}

Les données activées pour le profil qui sont ingérées dans [!DNL Platform] sont stockées dans [!DNL Data Lake] ainsi que dans la banque de données [!DNL Real-time Customer Profile]. Il peut parfois s&#39;avérer nécessaire de supprimer un jeu de données ou un lot du magasin [!DNL Profile] pour supprimer des données dont vous n&#39;avez plus besoin ou qui ont été ajoutées par erreur. Pour ce faire, l&#39;API doit être utilisée pour créer un [!DNL Profile System Job], également appelé &quot;[!DNL delete request]&quot;, qui peut être modifié, surveillé ou supprimé si nécessaire. Pour savoir comment utiliser les requêtes de suppression à l&#39;aide du point de terminaison `/system/jobs` de l&#39;API [!DNL Real-time Customer Profile], suivez les étapes décrites dans le guide de terminaison des tâches du système de profil ](profile-system-jobs.md).[

## Étapes suivantes {#next-steps}

Pour commencer à lancer des appels à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile], consultez le guide de prise en main [get started guide](getting-started.md), puis sélectionnez l&#39;un des guides de points de terminaison pour savoir comment utiliser des points de terminaison spécifiques [!DNL Profile]. Pour utiliser les données [!DNL Profile] à l&#39;aide de l&#39;interface utilisateur [!DNL Experience Platform], consultez le [Guide de l&#39;utilisateur du Profil client en temps réel](../ui/user-guide.md).
