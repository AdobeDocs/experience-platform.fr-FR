---
title: Classe du fournisseur
description: Ce document présente la classe Provider dans le modèle de données d’expérience (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 7%

---

# [!UICONTROL Fournisseur] class

Dans le modèle de données d’expérience (XDM), la variable [!UICONTROL Fournisseur] capture l’ensemble minimal de propriétés qui définissent une entité commerciale fournisseur (telle qu’un fournisseur de services de santé ou un fournisseur d’assurance).

![Structure de classe](../images/classes/provider.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nom de la personne]](../data-types/person-name.md) | Nom du fournisseur. |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `providerId` | [!UICONTROL Chaîne] | Identifiant unique du fournisseur. |

{style=&quot;table-layout:auto&quot;}

La classe peut être étendue à l’aide de la fonction [[!UICONTROL Fournisseur de soins de santé] groupe de champs](../field-groups/provider/healthcare-provider.md) pour décrire plus de détails sur un prestataire de soins.
