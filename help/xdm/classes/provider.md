---
title: Classe de fournisseur
description: Découvrez la classe Fournisseur dans le modèle de données d’expérience (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
TQID: https://experienceleague.adobe.com/D6d4ICCmnIq95CldmroXFy-GmYPMIJjDtr85znlH7to
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 148
ht-degree: 4%

---

# Classe [!UICONTROL Provider]

Dans le modèle de données d’expérience (XDM), la classe [!UICONTROL Provider] capture l’ensemble minimal de propriétés qui définissent une entité commerciale de fournisseur (comme un fournisseur de soins de santé ou un fournisseur d’assurance).

![Structure de classe](../images/classes/provider.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `providerName` | [[!UICONTROL &#x200B; Nom de la personne &#x200B;]](../data-types/person-name.md) | Nom du fournisseur. |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de déterminer l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’ID uniques si vous le souhaitez. |
| `providerId` | [!UICONTROL Chaîne] | Identifiant unique du fournisseur. |

{style="table-layout:auto"}

La classe peut être étendue avec le groupe de champs [[!UICONTROL Prestataire de soins de santé] &#x200B;](../field-groups/provider/healthcare-provider.md) pour décrire plus de détails sur un prestataire de soins de santé.
