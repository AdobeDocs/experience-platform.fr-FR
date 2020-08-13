---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide de développement de l’API Real-time Customer Profile
topic: guide
translation-type: tm+mt
source-git-commit: 84789a8e6e8c1f0fc91d0b54ba29d449963c3117
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 30%

---


# [!DNL Real-time Customer Profile] Guide du développeur d’API

[!DNL Real-time Customer Profile] offre une vue d’ensemble de chaque client dans Adobe Experience Platform. [!DNL Profile] vous permet de consolider diverses données clients provenant de plusieurs canaux, comme les données en ligne, hors ligne, CRM et tierces, en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

L’ [!DNL Real-time Customer Profile] API comprend plusieurs points de terminaison, décrits ci-dessous. Consultez les guides des points de terminaison individuels pour plus de détails et consultez le guide [de](getting-started.md) prise en main pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, consultez la page de swagger [Référence de l’API de Profil client en temps](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)réel.

Pour obtenir un guide sur l’utilisation des [!DNL Real-time Customer Profile] données dans l’ [!DNL Experience Platform] interface utilisateur, reportez-vous au guide [d’utilisation du](../ui/user-guide.md)Profil.

## (Alpha) Attributs calculés {#computed-attributes}

>[!IMPORTANT]
>
>La fonctionnalité des attributs calculés est une version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent faire l’objet de modifications.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agréger des valeurs sur tous les enregistrements et tous les événements. Chaque attribut calculé contient une expression, ou « règle », qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil ou dans un événement. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. You can create, view, edit, and delete computed attributes using the `config/computedAttributes` endpoint. Pour savoir comment utiliser ce point de terminaison, consultez le guide [des attributs](computed-attributes.md)calculés.

## Projections de périphérie {#edge-projections}

Adobe Experience Platform permet de personnaliser en temps réel les expériences client en rendant les données facilement accessibles sur des serveurs situés stratégiquement, appelés « périphéries ». The [!DNL Real-time Customer Profile] API provides endpoints for working with edges through components called &quot;projections.&quot; Cela inclut des configurations de projection permettant de définir quelles données doivent être projetées sur chaque périphérie, ainsi que des destinations de projection permettant de déterminer la direction d’une projection. Pour obtenir des informations détaillées sur l&#39;utilisation des projections de bord, veuillez consulter le guide [des configurations de](edge-projections.md)projection et des points de terminaison de destination.

## Entités ([!DNL Profile] accès) {#entities}

Through Adobe Experience Platform you can access [!DNL Real-time Customer Profile] data using RESTful APIs or the user interface. To learn how to access entities, more commonly known as &quot;profiles&quot;, using the API, follow the steps outlined in the [entities endpoint guide](entities.md). Pour accéder aux profils à l’aide de l’ [!DNL Platform] interface utilisateur, reportez-vous au guide [d’utilisation du](../ui/user-guide.md)Profil.

## Exportation de tâches ([!DNL Profile] exportation) {#profile-export}

[!DNL Real-time Customer Profile] les données peuvent être exportées dans un jeu de données en vue d’un traitement ultérieur, par exemple pour exporter des segments d’audience en vue d’une activation ou des attributs de profil en vue d’un rapports. Les tâches d’exportation pour les segments d’audience font partie de l’ [!DNL Adobe Experience Platform Segmentation Service] API. Pour en savoir plus, consultez le guide [des points de terminaison des tâches d’exportation de](../../profile/api/export-jobs.md) segmentation. Pour obtenir des instructions détaillées sur la création et la gestion des tâches d’exportation pour les attributs de profil, consultez le guide [de points de terminaison des tâches d’](export-jobs.md)exportation.

## Stratégies de fusion {#merge-policies}

When bringing data from multiple sources together in [!DNL Experience Platform], merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create individual customer profiles. Using the [!DNL Real-time Customer Profile] API, you can create new merge policies, manage existing policies, and set a default merge policy for your organization. To learn more about working with merge policies using the API, please visit the [merge policies endpoint guide](merge-policies.md).

For a guide to working with merge policies using the [!DNL Platform] UI, please see the [merge policies user guide](../ui/merge-policies.md).

## Etat de l’exemple de prévisualisation ([!DNL Profile] prévisualisation) {#profile-preview}

Les données activées pour le Profil étant ingérées dans l’Experience Platform, elles sont stockées dans le magasin de données du Profil. À mesure que le nombre d’enregistrements dans la banque de Profils augmente ou diminue, une tâche d’exemple est exécutée qui comprend des informations sur le nombre de fragments de profil et de profils fusionnés présents dans la banque de données. L&#39;API de Profil vous permet de prévisualisation du dernier exemple réussi, ainsi que de la distribution de profil de liste par jeu de données et par espace de nommage d&#39;identité. Pour commencer à utiliser le `/profilepreviewstatus` point de terminaison, reportez-vous au guide [de l’exemple de point de terminaison de l’état de la](preview-sample-status.md)prévisualisation.

## Tâches de système Profile {#profile-system-jobs}

Data ingested into [!DNL Platform] is stored in the [!DNL Data Lake] as well as the [!DNL Real-time Customer Profile] data store. Occasionally it may be necessary to delete a dataset or batch from the [!DNL Profile] store in order to remove data that you no longer require or that was added in error. This requires using the API to create a [!DNL Profile System Job], known as a &quot;[!DNL delete request]&quot;, that can also be, modified, monitored, or deleted if required. To learn how to work with delete requests using the `/system/jobs` endpoint in the [!DNL Real-time Customer Profile] API, follow the steps outlined in the [profile system jobs endpoint guide](profile-system-jobs.md).

## Étapes suivantes {#next-steps}

Pour commencer à lancer des appels à l’aide de l’ [!DNL Real-time Customer Profile] API, lisez le guide de [prise en main](getting-started.md) , puis sélectionnez l’un des guides de points de terminaison pour savoir comment utiliser des points de terminaison [!DNL Profile]liés. Pour utiliser [!DNL Profile] les données à l’aide de l’ [!DNL Experience Platform] interface utilisateur, reportez-vous au guide [d’utilisation du Profil client en temps](../ui/user-guide.md)réel.