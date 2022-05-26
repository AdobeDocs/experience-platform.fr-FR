---
title: Parcourir les commandes de travail relatives à l’hygiène des données
description: Découvrez comment afficher et gérer les tâches d’hygiène des données existantes dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
hide: true
hidefromtoc: true
source-git-commit: e539ee73b04230ac6e3dc4801ce0f8446bec8de6
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---

# Parcourir les ordres de travail relatifs à l’hygiène des données

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID de l’ordre de travail"
>abstract="Lorsqu’une demande d’hygiène des données est envoyée au système, un ordre de travail est créé pour exécuter la tâche demandée. En d’autres termes, un ordre de travail représente un processus spécifique d’hygiène des données, qui inclut son état actuel et d’autres détails connexes. Chaque ordre de travail se voit automatiquement attribuer son propre identifiant unique lors de sa création."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/browse.html" text="Pour en savoir plus, consultez le guide de l’interface utilisateur de l’hygiène des données ."

>[!IMPORTANT]
>
>Actuellement, les fonctionnalités d’hygiène des données de Adobe Experience Platform ne sont disponibles que pour les organisations qui ont acheté Adobe Shield pour les soins de santé.

Lorsqu’une demande d’hygiène des données est envoyée au système, un ordre de travail est créé pour exécuter la tâche demandée. Un ordre de travail représente un processus spécifique d’hygiène des données (tel que la suppression des données des consommateurs), qui inclut son état actuel et d’autres détails connexes.

Ce guide explique comment afficher et gérer les ordres de travail existants dans l’interface utilisateur de Adobe Experience Platform.

## Liste et filtrage des ordres de travail existants

Lorsque vous accédez pour la première fois à la variable **[!UICONTROL Hygiène des données]** dans l’interface utilisateur de , une liste des ordres de travail existants s’affiche avec leurs détails de base.

![Image montrant le [!UICONTROL Hygiène des données] espace de travail dans l’interface utilisateur de Platform](../images/ui/browse/work-order-list.png)

La liste affiche uniquement les ordres de travail d’une catégorie à la fois. Sélectionner **[!UICONTROL Consommateur]** pour afficher la liste des tâches de suppression des clients, et **[!UICONTROL Jeu de données]** pour afficher une liste des plannings de durée de vie (TTL) pour les jeux de données.

![Image montrant le [!UICONTROL Jeu de données] tab](../images/ui/browse/dataset-tab.png)

Sélectionnez l’icône d’entonnoir (![Image de l’icône de l’entonnoir](../images/ui/browse/funnel-icon.png)) pour afficher une liste de filtres pour les ordres de travail affichés.

![Image des filtres de l&#39;ordre de travail affichés](../images/ui/browse/filters.png)

Selon l’onglet que vous affichez, différents filtres sont disponibles :

| Filtrer | Catégorie | Description |
| --- | --- | --- |
| [!UICONTROL État] | [!UICONTROL Consommateur] &amp; [!UICONTROL Jeu de données] | Filtre basé sur l’état actuel de l’ordre de travail. |
| [!UICONTROL Date de création] | [!UICONTROL Consommateur] | Filtre basé sur le moment où la demande de suppression du client a été effectuée. |
| [!UICONTROL Date de création] | [!UICONTROL Jeu de données] | Filtre basé sur le moment où la demande de suppression du client a été effectuée. |
| [!UICONTROL Date de suppression] | [!UICONTROL Jeu de données] | Filtre basé sur la date de suppression planifiée par la durée de vie (TTL). |
| [!UICONTROL Date de mise à jour] | [!UICONTROL Jeu de données] | Filtre basé sur la date de la dernière mise à jour du jeu de données TTL. Les créations et les expiations TTL sont comptabilisées comme des mises à jour. |

{style=&quot;table-layout:auto&quot;}

## Afficher les détails d’un ordre de travail

Sélectionnez l’identifiant d’un ordre de travail répertorié pour en afficher les détails.

![Image montrant l’identifiant de l’ordre de travail sélectionné](../images/ui/browse/select-work-order.png)

Selon le type d’ordre de travail sélectionné, différentes informations et différents contrôles sont fournis. Ces sont traités dans les sections ci-dessous.

### Détails de suppression des clients

<!-- (Not available for initial release)
>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."
-->

Les détails d’une requête de suppression de consommateur sont en lecture seule, affichant ses attributs de base, tels que son état actuel et le temps écoulé depuis l’exécution de la requête.

![Image montrant la page de détails d’un ordre de travail de suppression de client](../images/ui/browse/consumer-delete-details.png)

### Détails TTL du jeu de données

La page de détails d’un TTL de jeu de données fournit des informations sur ses attributs de base, y compris la date d’expiration planifiée les jours restants avant la suppression. Dans le rail de droite, vous pouvez utiliser des commandes pour modifier ou annuler la durée de vie (TTL).

![Image montrant la page de détails d’un ordre de travail TTL de jeu de données](../images/ui/browse/ttl-details.png)

## Étapes suivantes

Ce guide explique comment afficher et gérer les ordres de travail existants en matière d’hygiène des données dans l’interface utilisateur de Platform. Pour plus d&#39;informations sur la création de vos propres ordres de travail, consultez la documentation suivante :

* [Suppression d’un client](./delete-consumer.md)
* [Planification TTL d’un jeu de données](./ttl.md)
