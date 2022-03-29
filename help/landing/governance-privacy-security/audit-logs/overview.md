---
title: Présentation des journaux d’audit
description: Découvrez comment les journaux d’audit vous permettent de voir qui a effectué les actions dans Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d726576a4d1f29d83f3b7cf72c9f5c5d4ff114d3
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 8%

---

# Journaux d’audit

Afin d’accroître la transparence et la visibilité des activités exécutées dans le système, Adobe Experience Platform vous permet de contrôler l’activité des utilisateurs pour divers services et fonctionnalités sous la forme de &quot;journaux d’audit&quot;. Ces journaux constituent un journal d’audit qui peut vous aider à résoudre les problèmes liés à Platform et à aider votre entreprise à se conformer efficacement aux politiques de gestion des données d’entreprise et aux exigences réglementaires.

En un sens simple, un journal d’audit indique : **who** performance **what** et **when**. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’e-mail de l’utilisateur qui a exécuté l’action et des attributs supplémentaires liés au type d’action.

Ce document couvre les journaux d’audit dans Platform, y compris la manière de les afficher et de les gérer dans l’interface utilisateur ou l’API.

## Types d’événement capturés par les journaux d’audit {#category}

Le tableau suivant décrit les actions sur lesquelles les ressources sont enregistrées par les journaux d’audit :

| Ressource | Actions |
| --- | --- |
| [Jeu de données](../../../catalog/datasets/overview.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li><li>Activer pour [Real-time Customer Profile](../../../profile/home.md)</li><li>Désactiver pour Profile</li></ul> |
| [Schéma](../../../xdm/schema/composition.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li><li>Activation pour Profile</li></ul> |
| [Classe](../../../xdm/schema/composition.md#class) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Groupe de champs](../../../xdm/schema/composition.md#field-group) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Type de données](../../../xdm/schema/composition.md#data-type) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Environnement de test](../../../sandboxes/home.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Réinitialiser</li><li>Supprimer</li></ul> |
| [Destination](../../../destinations/home.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li><li>Activer</li><li>Désactiver</li><li>Activation du jeu de données</li><li>Suppression de jeux de données</li><li>Activation de profil</li><li>Suppression de profils</li></ul> |
| [Segment](../../../segmentation/home.md) | <ul><li>Créez</li><li>Supprimer</li><li>Activation de segment</li><li>Suppression de segment</li></ul> |
| [Stratégie de fusion](../../../profile/merge-policies/overview.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Attribut calculé](../../../profile/computed-attributes/overview.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Profil de produit](../../../access-control/home.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Compte (Adobe)](../../../access-control/home.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |

## Accès aux journaux d’audit

Lorsque la fonction est activée pour votre organisation, les journaux d’audit sont automatiquement collectés au fur et à mesure de l’activité. Vous n’avez pas besoin d’activer manuellement la collecte des journaux.

Pour afficher et exporter les journaux d’audit, vous devez disposer de la variable **[!UICONTROL Afficher le journal d’activité utilisateur]** l’autorisation de contrôle d’accès accordée (trouvée sous [!UICONTROL Gouvernance des données] catégorie). Pour savoir comment gérer les autorisations individuelles pour les fonctionnalités de Platform, reportez-vous à la section [documentation sur le contrôle d’accès](../../../access-control/home.md).

## Gestion des journaux d’audit dans l’interface utilisateur

Vous pouvez afficher les journaux d’audit pour différentes fonctionnalités d’Experience Platform dans le **[!UICONTROL Audits]** dans l’interface utilisateur de Platform. L’espace de travail affiche une liste des journaux enregistrés, triés par défaut de la plus récente à la moins récente.

![Tableau de bord des journaux d’audit](../../images/audit-logs/audits.png)

Les journaux d’audit sont conservés pendant 365 jours, après quoi ils seront supprimés du système. Par conséquent, vous ne pouvez revenir que pendant une période maximale de 365 jours.

Sélectionnez un événement dans la liste pour afficher ses détails dans le rail de droite.

![Détails de l’événement](../../images/audit-logs/select-event.png)

### Filtrage des journaux d’audit

>[!NOTE]
>
>Comme il s’agit d’une nouvelle fonctionnalité, les données affichées remontent uniquement à mars 2022. Selon la ressource sélectionnée, des données antérieures pourront être disponibles à partir de janvier 2022.


Sélectionnez l’icône d’entonnoir (![Icône Filtrer](../../images/audit-logs/icon.png)) pour afficher une liste de contrôles de filtre afin de limiter les résultats. Seuls les 1000 derniers enregistrements sont affichés, quels que soient les différents filtres sélectionnés.

![Filtres](../../images/audit-logs/filters.png)

Les filtres suivants sont disponibles pour les événements de contrôle dans l’interface utilisateur :

| Filtrer | Description |
| --- | --- |
| [!UICONTROL Catégorie] | Utiliser le menu déroulant pour filtrer les résultats affichés par [category](#category). |
| [!UICONTROL Action] | Filtrer par action. Actuellement uniquement [!UICONTROL Créer] et [!UICONTROL Supprimer] Les actions peuvent être filtrées. |
| [!UICONTROL Utilisateur] | Saisissez l’identifiant utilisateur complet (par exemple, `johndoe@acme.com`) pour filtrer par utilisateur. |
| [!UICONTROL État] | Filtrez selon si l’action a été autorisée (terminée) ou refusée en raison de l’absence de [contrôle d&#39;accès](../../../access-control/home.md) autorisations. |
| [!UICONTROL Date] | Sélectionnez une date de début et/ou une date de fin pour définir une période en fonction de laquelle filtrer les résultats. Les données peuvent être exportées avec une période de recherche arrière de 90 jours (par exemple, 2021-12-15 à 2022-03-15). Cela peut varier en fonction du type d’événement. |

Pour supprimer un filtre, sélectionnez le &quot;X&quot; sur l’icône de pilule du filtre en question, ou sélectionnez **[!UICONTROL Effacer tout]** pour supprimer tous les filtres.

![Effacer les filtres](../../images/audit-logs/clear-filters.png)

### Exportation des journaux d’audit

Pour exporter la liste actuelle des journaux d’audit, sélectionnez **[!UICONTROL Journal de téléchargement]**.

![Journal de téléchargement](../../images/audit-logs/download.png)

Dans la boîte de dialogue qui s’affiche, sélectionnez le format de votre choix (soit **[!UICONTROL CSV]** ou **[!UICONTROL JSON]**), puis sélectionnez **[!UICONTROL Télécharger]**. Le navigateur télécharge le fichier généré et l’enregistre sur votre ordinateur.

![Sélectionner le format de téléchargement](../../images/audit-logs/select-download-format.png)

## Gestion des journaux d’audit dans l’API

Toutes les actions que vous pouvez effectuer dans l’interface utilisateur peuvent également être effectuées à l’aide d’appels API. Voir [Document de référence d’API](https://www.adobe.io/experience-platform-apis/references/audit-query/) pour plus d’informations.

## Gestion des journaux d’audit pour Adobe Admin Console

Pour savoir comment gérer les journaux d’audit pour les activités dans Adobe Admin Console, reportez-vous aux sections suivantes : [document](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Étapes suivantes et ressources supplémentaires

Ce guide explique comment gérer les journaux d’audit dans Experience Platform. Pour plus d’informations sur la surveillance des activités de Platform, consultez la documentation sur [Observability Insights](../../../observability/home.md) et [surveillance de l’ingestion des données](../../../ingestion/quality/monitor-data-ingestion.md).

Pour mieux comprendre les journaux d’audit dans Experience Platform, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
