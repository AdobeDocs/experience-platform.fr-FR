---
title: Groupe De Champs Détails Du Prospect Partenaire (Exemple)
description: Découvrez le groupe de champs de schéma (XDM) des Détails du prospect partenaire (exemple).
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
TQID: https://experienceleague.adobe.com/8lScs-QTKmjm6qmrBkEw3URhc8OgpQtpaa-lipYBibk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 9%

---

# Groupe de champs [!UICONTROL Détails du prospect partenaire (exemple)]

[!UICONTROL Détails du prospect partenaire (exemple)] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). L’exemple [!UICONTROL Détails du prospect partenaire (Détails)] fournit un exemple de framework pour divers détails liés au profil d’un prospect. Ce cadre simplifie le processus d’organisation et de gestion de diverses informations relatives aux prospects.

Ce groupe de champs étend la classe [Profil de prospect individuel](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html?lang=fr) dans le contexte d’un partenaire.

![Diagramme du groupe de champs [!UICONTROL Détails du prospect partenaire (exemple)].](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | chaîne | Tranche d&#39;âge au sein du ménage. |
| [!UICONTROL vêtementsAccessoires] | `apparelAccessories` | chaîne | Préférences ou implication dans les vêtements/accessoires. |
| [!UICONTROL cyclisme] | `bicycling` | chaîne | Intérêt ou participation à des activités de cyclisme. |
| [!UICONTROL cableTv] | `cableTv` | chaîne | Indique un engagement avec la télévision par câble. |
| [!UICONTROL domestique] | `domestics` | chaîne | Préférences ou engagement dans des activités nationales. |
| [!UICONTROL électronique] | `electronics` | chaîne | Intérêt ou engagement dans les dispositifs électroniques. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | chaîne | Préférences ou implication dans les aliments/boissons. |
| [!UICONTROL chaussures] | `footwear` | chaîne | Intérêt ou participation dans la chaussure. |
| [!UICONTROL healthFoods] | `healthFoods` | chaîne | Préférences ou participation à des aliments sains. |
| [!UICONTROL randonnée] | `hiking` | chaîne | Intérêt ou participation à des activités de randonnée. |
| [!UICONTROL householdId] | `householdId` | chaîne | Identifiant unique du ménage. |
| [!UICONTROL individualId] | `individualId` | chaîne | Identifiant unique de l’individu. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | chaîne | L’inférence d’être titulaire d’une carte. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | chaîne | L&#39;inférence d&#39;être titulaire d&#39;une carte à prime. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | chaîne | Indicateur du niveau de correspondance. |
| [!UICONTROL BuyerRating] | `buyerRating` | chaîne | Une évaluation liée au comportement d’achat. |
| [!UICONTROL DonorRating] | `donorRating` | chaîne | Évaluation liée au comportement du donneur. |
| [!UICONTROL InvestmentRating] | `investmentRating` | chaîne | Une note liée au comportement d’investissement. |
| [!UICONTROL ResponderRating] | `responderRating` | chaîne | Évaluation liée au comportement du répondeur. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | chaîne | La vitesse ou le taux de dépenses. |
| [!UICONTROL SendingVolume] | `spendingVolume` | chaîne | Montant ou volume des dépenses. |
| [!UICONTROL recordId] | `recordId` | chaîne | Identifiant unique de l’enregistrement. |
| [!UICONTROL résidenceId] | `residenceId` | chaîne | Identifiant unique de la résidence. |
| [!UICONTROL voile] | `sailing` | chaîne | Indique l&#39;intérêt ou la participation aux activités nautiques. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | chaîne | Indique les préférences ou l’implication dans les produits de vacances. |
| [!UICONTROL ski] | `skiing` | chaîne | Indique l&#39;intérêt ou la participation aux activités de ski. |
| [!UICONTROL tennis] | `tennis` | chaîne | Indique l’intérêt ou l’implication dans les activités de tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | chaîne | Indique l’engagement avec les achats TV. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) sur le référentiel XDM public.
