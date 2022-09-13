---
title: Parcourir les ordres de travail relatifs au nettoyage de données
description: Découvrez comment afficher et gérer les ordres de travail de nettoyage de données existants dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: f246a014de7869b627a677ac82e98d4556065010
workflow-type: tm+mt
source-wordcount: '616'
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
>Actuellement, les fonctionnalités de nettoyage de données d’Adobe Experience Platform sont uniquement disponibles pour les organisations qui ont acheté Healthcare Shield.

Lorsqu’une demande de nettoyage de données est envoyée au système, un ordre de travail est créé pour exécuter la tâche demandée. Un ordre de travail représente un processus spécifique de nettoyage de données (par exemple, l’expiration planifiée d’un jeu de données), qui comprend le statut actuel et d’autres détails connexes.

Ce guide explique comment afficher et gérer les ordres de travail existants dans l’interface utilisateur d’Adobe Experience Platform.

## Répertorier et filtrer les ordres de travail existants

Lorsque vous accédez pour la première fois à l’espace de travail **[!UICONTROL Nettoyage de données]** dans l’interface utilisateur, une liste des ordres de travail existants et les détails de base s’affichent.

![Image illustrant l’espace de travail [!UICONTROL Nettoyage de données] dans l’interface utilisateur de Platform](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Sélectionnez l’icône d’entonnoir (![image de l’icône d’entonnoir](../images/ui/browse/funnel-icon.png)) pour consulter une liste de filtres pour les ordres de travail affichés.

![Image des filtres d’ordres de travail affichés](../images/ui/browse/filters.png)

| Filtre | Description |
| --- | --- |
| [!UICONTROL Statut] | Filtre basé sur le statut actuel de l’ordre de travail :<ul><li>**[!UICONTROL Terminé]** : le traitement est terminé.</li><li>**[!UICONTROL En attente]** : le traitement a été créé mais n’a pas encore été exécuté. Une [demande relative à l’expiration du jeu de données](./dataset-expiration.md) suppose que ce statut est antérieur à la date de suppression planifiée. Une fois la date de suppression atteinte, le statut est mis à jour vers [!UICONTROL Exécution], sauf si le traitement est annulé au préalable.</li><li>**[!UICONTROL Exécution]** : la demande relative à l’expiration du jeu de données a commencé et est en cours de traitement.</li><li>**[!UICONTROL Annulé]** : le traitement a été annulé dans le cadre d’une demande d’utilisateur manuelle.</li></ul> |
| [!UICONTROL Date de création] | Filtre basé sur le moment où l’ordre de travail a été effectué. |
| [!UICONTROL Date d’expiration] | Filtrez les demandes relatives à l’expiration du jeu de données en fonction de la date de suppression planifiée pour le jeu de données en question. |
| [!UICONTROL Date de mise à jour] | Filtrez les demandes relatives à l’expiration du jeu de données en fonction de la date de la dernière mise à jour de l’ordre de travail. Les créations et les expirations sont comptées comme des mises à jour. |

{style=&quot;table-layout:auto&quot;}

## Afficher les détails d’un ordre de travail {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Statut par service"
>abstract="Les demandes liées à l’hygiène des données sont traitées indépendamment par plusieurs services d’Experience Platform. Cette section décrit le statut actuel du traitement de la requête pour chaque service respectif. Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène de données."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Nombre d’identités"
>abstract="Nombre d’identités qui ont été demandées à être supprimées dans le cadre de cet ordre de travail. Les identités incluses dans le nombre n’existent pas nécessairement dans les jeux de données affectés. Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène de données."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Réponse de suppression du client"
>abstract="Lorsqu’un processus de suppression d’un client reçoit une réponse du système, ces messages s’affichent sous la section **[!UICONTROL Résultat]**. Si un problème se produit alors qu’un ordre de travail est en cours de traitement, tous les messages d’erreur pertinents s’affichent dans cette section pour vous aider à résoudre le problème. Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène de données."

Sélectionnez l’identifiant d’un ordre de travail répertorié pour en afficher les détails.

![Image illustrant l’identifiant de l’ordre de travail sélectionné](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details {#consumer-delete}

The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details {#dataset-expiration} -->

La page de détails d’une expiration de jeu de données fournit des informations sur les attributs de base, notamment la date d’expiration prévue pour les jours restants avant la suppression. Dans le rail de droite, vous pouvez utiliser des commandes pour modifier ou annuler l’expiration.

![Image illustrant la page de détails d’un ordre de travail d’expiration de jeu de données](../images/ui/browse/ttl-details.png)

## Étapes suivantes

Ce guide explique comment afficher et gérer les ordres de travail de nettoyage de données existants dans l’interface utilisateur de Platform. Pour plus d’informations sur la création de vos propres ordres de travail, consultez le guide sur la [planification de l’expiration d’un jeu de données](./dataset-expiration.md).
