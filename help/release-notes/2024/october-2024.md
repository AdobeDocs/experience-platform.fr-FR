---
title: Notes de mise à jour d’octobre 2024 d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2024 pour Adobe Experience Platform.
source-git-commit: a381bdc45ee9c3c7ffb32bb7a7ec43a1233d1556
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 36%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 29 octobre 2024**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Segmentation Service](#segmentation-service)
- [Sandbox](#sandboxes)
- [Sources](#sources)

<!-- ## Dashboards {#dashboards}

Experience Platform provides multiple dashboards through which you can view important insights about your organization's data, as captured during daily snapshots.

**New or updated features**

| Feature | Description |
| --- | --- |
| Data Distiller Templates | Explore multiple templates to gain structured insights into audience data. Use dashboards like **Advanced [!UICONTROL Audience Overlaps]**, **[!UICONTROL Audience Comparison]**, **[!UICONTROL Audience Trends]**, and **[!UICONTROL Audience Identity Overlaps]** to make data-driven decisions, optimize segmentation, and enhance engagement strategies. See the [Data Distiller Templates guide](../../dashboards/sql-insights-query-pro-mode/templates/overview.md) for more details. |
| Advanced Audience Overlaps | Quickly analyze audience intersections for specific audiences or view all overlaps to uncover valuable insights across your entire audience set. Use these insights to refine segmentation, reduce redundant messaging, and create more targeted campaigns for improved marketing efficiency. See the [Advanced Audience Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md) for more details. |
| Audience Comparison enhancements | View a side-by-side comparison of key metrics between different audience groups using the **Audience Comparison** dashboard. With this dashboard you can select specific time frames and KPIs, such as audience size and identity composition, to make more informed decisions about audience segmentation and targeting strategies. Read the [Audience Comparison guide](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md) for more information. |
| Audience Trends Visualization | Analyze audience metrics over time with the **[!UICONTROL Audience Trends]** dashboard. Visualize trends for audience size, number of identities, and number of single identity profiles to help you monitor audience evolution, measure growth, and refine your engagement strategies. See the [Audience Trends guide](../../dashboards/sql-insights-query-pro-mode/templates/trends.md) for more details. |
| Identity Overlaps Analysis | Analyze identity overlaps in selected audiences with the **[!UICONTROL Audience Identity Overlaps]** dashboard. View identity trends and breakdowns to understand how different identity types relate within your audience, enhancing identity stitching and improving customer segmentation accuracy. Refer to the [Audience Identity Overlaps guide](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md) for more details. |

{style="table-layout:auto"}

For more information on dashboards, including how to grant access permissions and create custom widgets, begin by reading the [dashboards overview](../../dashboards/home.md). -->

## Collecte de données {#collection}

Adobe Experience Platform fournit une suite de technologies qui vous permet de collecter des données d’expérience client côté client et de les envoyer à l’Edge Network Experience Platform où elles peuvent être enrichies, transformées et distribuées vers des destinations Adobe ou non Adobe.

**Nouvelles fonctionnalités**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Balises et extensions | Vue JSON Adobe Analytics | Vous pouvez désormais utiliser l’extension de balises Adobe Analytics pour examiner les eVars, les props et les paramètres d’événement au format JSON, qui peuvent désormais être inclus dans l’extension du SDK Web et exportés en vue de leur modification. Vous pouvez également charger ou copier ces données et les stocker sur votre appareil. Pour plus d’informations, consultez la [documentation de l’extension Adobe Analytics](../../tags/extensions/client/analytics/overview.md) . |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de la collecte de données](../../collection/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| ----------- | ----------- |
| [Prise en charge de l’exportation de tableaux disponible en général](../../destinations/ui/export-arrays-calculated-fields.md) | Tous les clients peuvent désormais utiliser l’option **[!UICONTROL Ajouter un champ calculé]** lors de l’activation d’audiences *vers des destinations basées sur des fichiers* pour exporter des tableaux entiers ou des éléments de tableaux. Notez que vous devez toujours utiliser la fonction `array_to_string` pour aplatir le tableau en une chaîne dans le fichier cible. <br> ![ Ajoutez une sélection de champ calculée avec des fonctions et des champs.](../2024/assets/october/array-export.gif "Ajoutez un champ calculé avec une sélection de la fonction array_to_string et du tableau des organisations."){width="250" align="center" zoomable="yes"} |
| [ Améliorations de la précision des rapports pour les destinations de diffusion en continu ](/help/destinations/ui/export-datasets.md) | Depuis octobre 2024, Adobe met à jour une mise à jour afin d’accroître la précision des rapports pour les destinations de diffusion en continu. Cette amélioration garantit un meilleur alignement entre l’Experience Platform et les rapports sur les plateformes de destination. <br> Avant cette mise à jour, **[!UICONTROL Identités ayant échoué]** incluait toutes les tentatives d’activation. Après cette mise à jour, seule la dernière reprise d’activation est incluse dans le nombre total. <br> Cette amélioration s’applique actuellement à la [destination de correspondance client Google](../../destinations/catalog/advertising/google-customer-match.md), mais sera progressivement déployée vers d’autres destinations de diffusion en continu Experience Platform. Suite à cette amélioration, les utilisateurs de la [destination de correspondance du client Google](../../destinations/catalog/advertising/google-customer-match.md) peuvent constater une baisse attendue de leur nombre **[!UICONTROL identités ayant échoué]**. |
| Incidences flexibles de l’évaluation de l’audience sur l’[activation de l’audience par lots](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Si vous exécutez l’ [évaluation d’audience flexible](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation) sur des audiences déjà configurées pour être activées après l’évaluation des segments, les audiences seront activées dès que la tâche d’évaluation d’audience flexible sera terminée, quelles que soient les tâches d’activation quotidiennes précédentes. <br> Cela peut entraîner l’exportation d’audiences plusieurs fois par jour, en fonction de vos actions. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| [!BADGE Disponibilité limitée]{type=Informative} Évaluation flexible de l’audience | L’évaluation flexible des audiences vous permet de créer rapidement de nouvelles audiences à la demande pour des communications sensibles au temps. Vous trouverez plus d’informations sur cette nouvelle fonctionnalité dans la [documentation d’Audience Portal](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [vue d’ensemble de la segmentation](../../segmentation/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Partage de modules d’outils Sandbox | Vous pouvez désormais utiliser l’outil d’environnement de test pour exporter et importer facilement des configurations d’environnement de test entre les environnements de test de différentes organisations. Deux catégories de packages partagés sont désormais disponibles :<br><ul><li>**[Package privé](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages) :** Utilisez le partage de package privé avec les organisations qui ont approuvé la demande de partage de l’organisation source.</li><li>**[Package public](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages) :** les packages publics peuvent être partagés sans validation supplémentaire et sont facilement importés à l’aide de la charge utile du package.</li></ul><br>Pour plus d&#39;informations sur ces fonctionnalités, consultez le guide sur le [partage de modules dans toutes les organisations](../../sandboxes/ui/sharing-packages-across-orgs.md). |
| [Partage de modules](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) dans l’API d’outils Sandbox | Utilisez l’API de l’outil de test pour envoyer des requêtes à deux nouveaux points de terminaison, `/handshake` et `/transfer` pour le partage entre les organisations, la récupération et la création de requêtes de partage de package. Une requête supplémentaire a été ajoutée au point de terminaison `/packages` pour récupérer la charge utile d’un module. |

{style="table-layout:auto"}

Pour plus d’informations sur les environnements de test, consultez la [présentation des environnements de test](../../sandboxes/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge du filtrage des entités d’activité standard dans [!DNL Marketo Engage] | Vous pouvez utiliser l’API [!DNL Flow Service] pour filtrer les entités d’activité standard lors de l’ingestion de données provenant de votre source [!DNL Marketo Engage]. Pour plus d’informations, consultez le guide sur le [filtrage [!DNL Marketo] données d’activité standard](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage) . |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).
