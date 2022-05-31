---
title: Parcourir les commandes de travail relatives à l’hygiène des données
description: Découvrez comment afficher et gérer les tâches d’hygiène des données existantes dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: c24aa700eb425770266bbee5c187e2e87b15a9ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 1%

---

# Parcourir les ordres de travail relatifs à l’hygiène des données {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID de l’ordre de travail"
>abstract="Lorsqu’une demande d’hygiène des données est envoyée au système, un ordre de travail est créé pour exécuter la tâche demandée. En d’autres termes, un ordre de travail représente un processus spécifique d’hygiène des données, qui inclut son état actuel et d’autres détails connexes. Chaque ordre de travail se voit automatiquement attribuer son propre identifiant unique lors de sa création."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont disponibles que pour les organisations qui ont acheté Adobe Shield pour les soins de santé.

Lorsqu’une demande d’hygiène des données est envoyée au système, un ordre de travail est créé pour exécuter la tâche demandée. Un ordre de travail représente un processus d’hygiène des données spécifique, tel qu’une heure d’activation planifiée (TTL) d’un jeu de données, qui inclut son état actuel et d’autres détails connexes.

Ce guide explique comment afficher et gérer les ordres de travail existants dans l’interface utilisateur de Adobe Experience Platform.

## Liste et filtrage des ordres de travail existants

Lorsque vous accédez pour la première fois à la variable **[!UICONTROL Hygiène des données]** dans l’interface utilisateur de , une liste des ordres de travail existants s’affiche avec leurs détails de base.

![Image montrant le [!UICONTROL Hygiène des données] espace de travail dans l’interface utilisateur de Platform](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Sélectionnez l’icône d’entonnoir (![Image de l’icône de l’entonnoir](../images/ui/browse/funnel-icon.png)) pour afficher une liste de filtres pour les ordres de travail affichés.

![Image des filtres de l&#39;ordre de travail affichés](../images/ui/browse/filters.png)

| Filtrer | Description |
| --- | --- |
| [!UICONTROL État] | Filtre basé sur l’état actuel de l’ordre de travail. |
| [!UICONTROL Date de création] | Filtrez selon la date à laquelle la requête TTL du jeu de données a été effectuée. |
| [!UICONTROL Date de suppression] | Filtre basé sur la date de suppression planifiée par la durée de vie (TTL). |
| [!UICONTROL Date de mise à jour] | Filtre basé sur la date de la dernière mise à jour du jeu de données TTL. Les créations et les expiations TTL sont comptabilisées comme des mises à jour. |

{style=&quot;table-layout:auto&quot;}

## Afficher les détails d’un ordre de travail

Sélectionnez l’identifiant d’un ordre de travail répertorié pour en afficher les détails.

![Image montrant l’identifiant de l’ordre de travail sélectionné](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

La page de détails d’un TTL de jeu de données fournit des informations sur ses attributs de base, y compris la date d’expiration planifiée les jours restants avant la suppression. Dans le rail de droite, vous pouvez utiliser des commandes pour modifier ou annuler la durée de vie (TTL).

![Image montrant la page de détails d’un ordre de travail TTL de jeu de données](../images/ui/browse/ttl-details.png)

## Étapes suivantes

Ce guide explique comment afficher et gérer les ordres de travail existants en matière d’hygiène des données dans l’interface utilisateur de Platform. Pour plus d’informations sur la création de vos propres ordres de travail, consultez le guide sur [planification de la durée de vie (TTL) d’un jeu de données](./ttl.md).
