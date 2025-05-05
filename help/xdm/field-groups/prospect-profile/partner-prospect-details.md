---
title: Groupe de champs Détails du projet partenaire (exemple)
description: Découvrez le groupe de champs Détails du projet partenaire (exemple) (XDM) .
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# [!UICONTROL Détails du projet partenaire (exemple)] groupe de champs

[!UICONTROL Partner Prospect Details (Sample)] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le [!UICONTROL Partner Prospect Details (Sample)] fournit un exemple de structure pour divers détails liés au profil d’un prospect. Ce cadre simplifie le processus d’organisation et de gestion de diverses informations liées aux prospects.

Ce groupe de champs étend la [classe Individual Prospect Profile](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) dans le contexte d’un partenaire.

![Schéma du groupe de champs [!UICONTROL Détails du projet partenaire (exemple)].](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | Chaîne | Age au sein du foyer. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | Chaîne | Préférences ou implication dans les vêtements/accessoires. |
| [!UICONTROL vélo] | `bicycling` | Chaîne | Intérêt ou implication dans les activités de vélo. |
| [!UICONTROL cableTv] | `cableTv` | Chaîne | Indique l’engagement avec la télévision par câble. |
| [!UICONTROL domestitics] | `domestics` | Chaîne | Préférences ou engagement dans les activités nationales. |
| [!UICONTROL électronique] | `electronics` | Chaîne | L’intérêt ou l’engagement dans les appareils électroniques. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Chaîne | Préférences ou implication dans les aliments/boissons. |
| [!UICONTROL chaussures] | `footwear` | Chaîne | Intérêt ou implication dans les chaussures. |
| [!UICONTROL healthFoods] | `healthFoods` | Chaîne | Préférences ou implication dans les aliments pour la santé. |
| [!UICONTROL randonnée] | `hiking` | Chaîne | Intérêt ou implication dans les activités de randonnée. |
| [!UICONTROL householdId] | `householdId` | Chaîne | Identifiant unique du foyer. |
| [!UICONTROL individualId] | `individualId` | Chaîne | Identifiant unique de l’individu. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | Chaîne | L&#39;inférence d&#39;être détenteur de carte. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | Chaîne | L’idée d’être détenteur de carte de crédit Premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | Chaîne | Indicateur du niveau correspondant. |
| [!UICONTROL BuyerRating] | `buyerRating` | Chaîne | Évaluation liée au comportement d’achat. |
| [!UICONTROL DonorRating] | `donorRating` | Chaîne | Évaluation liée au comportement des donneurs. |
| [!UICONTROL InvestmentRating] | `investmentRating` | Chaîne | Évaluation liée au comportement d’investissement. |
| [!UICONTROL ResponderRating] | `responderRating` | Chaîne | Évaluation liée au comportement du participant. |
| [!UICONTROL &rbrace;DépensesVelocity] | `spendingVelocity` | Chaîne | La vitesse ou le taux de dépenses. |
| [!UICONTROL DépensesVolume] | `spendingVolume` | Chaîne | Montant ou volume des dépenses. |
| [!UICONTROL recordId] | `recordId` | Chaîne | Identifiant unique de l’enregistrement. |
| [!UICONTROL RésidenceId] | `residenceId` | Chaîne | Identifiant unique de la résidence. |
|  | `sailing` | Chaîne | Indique l’intérêt ou l’implication dans les activités de navigation. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Chaîne | Indique les préférences ou l’engagement dans les produits de vacances. |
| [!UICONTROL skiing] | `skiing` | Chaîne | Indique l’intérêt ou l’implication dans les activités de ski. |
| [!UICONTROL tennis] | `tennis` | Chaîne | Indique l’intérêt ou l’implication dans les activités de tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Chaîne | Indique l’engagement avec les achats à la télévision. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) sur le référentiel XDM public.
