---
title: Parcourir les ordres de travail relatifs au nettoyage de données
description: Découvrez comment afficher et gérer les ordres de travail de nettoyage de données existants dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: c24aa700eb425770266bbee5c187e2e87b15a9ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 100%

---

# Parcourir les ordres de travail relatifs au nettoyage de données {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="Identifiants des ordres de travail"
>abstract="Lorsqu’une demande de nettoyage de données est envoyée au système, un ordre de travail est créé pour exécuter la tâche demandée. En d’autres termes, un ordre de travail représente un processus spécifique de nettoyage de données comprenant le statut actuel et d’autres détails connexes. Chaque ordre de travail est automatiquement doté d’un identifiant unique lors de sa création."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités de nettoyage de données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté Adobe Shield for Healthcare.

Lorsqu’une demande de nettoyage de données est envoyée au système, un ordre de travail est créé pour exécuter la tâche demandée. Un ordre de travail représente un processus spécifique d’hygiène des données, tel qu’une durée de vie planifiée (TTL) d’un jeu de données, qui comprend son statut actuel et d’autres détails connexes.

Ce guide explique comment afficher et gérer les ordres de travail existants dans l’interface utilisateur d’Adobe Experience Platform.

## Répertorier et filtrer les ordres de travail existants

Lorsque vous accédez pour la première fois à l’espace de travail **[!UICONTROL Nettoyage de données]** dans l’interface utilisateur, une liste des ordres de travail existants et les détails de base s’affichent.

![Image illustrant l’espace de travail [!UICONTROL Nettoyage de données] dans l’interface utilisateur de Platform](../images/ui/browse/work-order-list.png).

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Sélectionnez l’icône d’entonnoir (![image de l’icône d’entonnoir](../images/ui/browse/funnel-icon.png)) pour consulter une liste de filtres pour les ordres de travail affichés.

![Image des filtres d’ordres de travail affichés](../images/ui/browse/filters.png).

| Filtre | Description |
| --- | --- |
| [!UICONTROL Statut] | Filtre basé sur le statut actuel de l’ordre de travail. |
| [!UICONTROL Date de création] | Filtre basé sur la date à laquelle la demande relative à la durée de vie du jeu de données a été effectuée. |
| [!UICONTROL Date de suppression] | Filtre basé sur la date de suppression planifiée par la TTL. |
| [!UICONTROL Date de mise à jour] | Filtre basé sur la date de la dernière mise à jour de la TTL du jeu de données. Les créations et les expirations de TTL sont comptées comme des mises à jour. |

{style=&quot;table-layout:auto&quot;}

## Afficher les détails d’un ordre de travail

Sélectionnez l’identifiant d’un ordre de travail répertorié pour en afficher les détails.

![Image illustrant l’identifiant de l’ordre de travail sélectionné](../images/ui/browse/select-work-order.png).

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

La page de détails d’une TTL de jeu de données fournit des informations sur les attributs de base, notamment la date d’expiration prévue pour les jours restants avant la suppression. Dans le rail de droite, vous pouvez utiliser des commandes pour modifier ou annuler la TTL.

![Image illustrant la page de détails d’un ordre de travail de TTL de jeu de données](../images/ui/browse/ttl-details.png).

## Étapes suivantes

Ce guide explique comment afficher et gérer les ordres de travail de nettoyage de données existants dans l’interface utilisateur de Platform. Pour plus d’informations sur la création de vos propres ordres de travail, consultez le guide sur la [planification de la durée de vie (TTL) d’un jeu de données](./ttl.md).
