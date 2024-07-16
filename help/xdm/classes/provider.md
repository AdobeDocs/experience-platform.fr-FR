---
title: Classe du fournisseur
description: Découvrez la classe Provider dans le modèle de données d’expérience (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 4%

---

# Classe [!UICONTROL Provider]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Provider] capture l’ensemble minimal de propriétés qui définissent une entité commerciale de fournisseur (telle qu’un fournisseur de soins de santé ou un fournisseur d’assurance).

![Structure de classe](../images/classes/provider.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Nom de personne]](../data-types/person-name.md) | Nom du fournisseur. |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Comme ce champ est généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `providerId` | [!UICONTROL Chaîne] | Identifiant unique du fournisseur. |

{style="table-layout:auto"}

La classe peut être étendue avec le groupe de champs [[!UICONTROL Fournisseur de soins de santé]](../field-groups/provider/healthcare-provider.md) pour décrire plus de détails sur un prestataire de soins de santé.
