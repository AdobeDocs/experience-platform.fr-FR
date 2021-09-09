---
title: Présentation des journaux d’audit
description: Découvrez comment les journaux d’audit vous permettent de voir qui a effectué les actions dans Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: df269a30251cb17e337ec25787d6a1eed41e9c0b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 5%

---

# Journaux d’audit (version bêta)

>[!IMPORTANT]
>
>La fonctionnalité des journaux d’audit de Adobe Experience Platform est actuellement en version bêta. Les fonctionnalités décrites dans cette documentation peuvent faire l’objet de modifications.

Afin d’accroître la transparence et la visibilité des activités exécutées dans le système, Adobe Experience Platform vous permet de contrôler l’activité des utilisateurs pour divers services et fonctionnalités sous la forme de &quot;journaux d’audit&quot;. Ces journaux constituent un journal d’audit qui peut vous aider à résoudre les problèmes liés à Platform et à aider votre entreprise à se conformer efficacement aux politiques de gestion des données d’entreprise et aux exigences réglementaires.

En un sens simple, un journal d’audit indique à **qui** a effectué **l’action** et **quand**. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’e-mail de l’utilisateur qui a exécuté l’action et des attributs supplémentaires liés au type d’action.

Ce document couvre les journaux d’audit dans Platform, y compris la manière de les afficher et de les gérer dans l’interface utilisateur ou l’API.

## Types d’événement capturés par les journaux d’audit

Le tableau suivant décrit les actions sur lesquelles les ressources sont enregistrées par les journaux d’audit :

| Ressource | Actions |
| --- | --- |
| [Environnement de test](../../../sandboxes/home.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Réinitialiser</li><li>Supprimer</li></ul> |
| [Jeu de données](../../../catalog/datasets/overview.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li><li>Activez pour [Real-time Customer Profile](../../../profile/home.md)</li></ul> |
| [Schéma](../../../xdm/schema/composition.md) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Groupe de champs](../../../xdm/schema/composition.md#field-group) | <ul><li>Créez</li><li>Mise à jour </li><li>Supprimer</li></ul> |
| [Destination](../../../destinations/home.md) | <ul><li>Activer</li></ul> |

## Accès aux journaux d’audit

Lorsque la fonction est activée pour votre organisation, les journaux d’audit sont automatiquement collectés au fur et à mesure de l’activité. Vous n’avez pas besoin d’activer manuellement la collecte des journaux.

Pour afficher et exporter les journaux d’audit, vous devez disposer de l’autorisation de contrôle d’accès &quot;Afficher les journaux d’audit&quot; (disponible dans la catégorie &quot;Gouvernance des données&quot;). Pour savoir comment gérer les autorisations individuelles pour les fonctionnalités de Platform, consultez la [documentation sur le contrôle d’accès](../../../access-control/home.md).

## Gestion des journaux d’audit dans l’interface utilisateur

Vous pouvez afficher les journaux d’audit pour différentes fonctionnalités Experience Platform dans l’espace de travail **[!UICONTROL Audits]** de l’interface utilisateur de Platform. L’espace de travail affiche une liste des journaux enregistrés, triés par défaut de la plus récente à la moins récente.

![Tableau de bord des journaux d’audit](../../images/audit-logs/audits.png)

Le système affiche uniquement les journaux d’audit de l’année précédente. Les journaux qui dépassent cette limite sont automatiquement supprimés du système.

Sélectionnez un événement dans la liste pour afficher ses détails dans le rail de droite.

![Détails de l’événement](../../images/audit-logs/select-event.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## Gestion des journaux d’audit dans l’API

Toutes les actions que vous pouvez effectuer dans l’interface utilisateur peuvent également être effectuées à l’aide d’appels API. Pour plus d’informations, consultez le [document de référence sur l’API](https://www.adobe.io/experience-platform-apis/references/audit-query/) .

## Gestion des journaux d’audit pour Adobe Admin Console

Pour savoir comment gérer les journaux d’audit pour les activités dans Adobe Admin Console, reportez-vous au [document](https://helpx.adobe.com/enterprise/using/audit-logs.html) suivant.

## Étapes suivantes

Ce guide explique comment gérer les journaux d’audit dans Experience Platform. Pour plus d’informations sur la surveillance des activités de Platform, consultez la documentation sur [Observability Insights](../../../observability/home.md) et [la surveillance de l’ingestion des données](../../../ingestion/quality/monitor-data-ingestion.md).
