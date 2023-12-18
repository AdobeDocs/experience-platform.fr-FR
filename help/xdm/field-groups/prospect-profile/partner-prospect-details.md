---
title: Groupe de champs Détails du projet partenaire (exemple)
description: Découvrez le groupe de champs Détails du projet partenaire (exemple) (XDM) .
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 9%

---

# [!UICONTROL Détails du projet partenaire (exemple)] groupe de champs

[!UICONTROL Détails du projet partenaire (exemple)] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). La variable [!UICONTROL Détails du projet partenaire (exemple)] fournit un exemple de structure pour divers détails liés au profil d’un prospect. Ce cadre simplifie le processus d’organisation et de gestion de diverses informations liées aux prospects.

Ce groupe de champs étend la [Classe Individual Prospect Profile](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) dans le contexte d’un partenaire.

![Un diagramme de [!UICONTROL Détails du projet partenaire (exemple)] groupe de champs.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | chaîne | Age au sein du foyer. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | chaîne | Préférences ou implication dans les vêtements/accessoires. |
| [!UICONTROL vélo] | `bicycling` | chaîne | Intérêt ou implication dans les activités de vélo. |
| [!UICONTROL cableTv] | `cableTv` | chaîne | Indique l’engagement avec la télévision par câble. |
| [!UICONTROL intérieurs] | `domestics` | chaîne | Préférences ou engagement dans les activités nationales. |
| [!UICONTROL électronique] | `electronics` | chaîne | L’intérêt ou l’engagement dans les appareils électroniques. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | chaîne | Préférences ou implication dans les aliments/boissons. |
| [!UICONTROL chaussures] | `footwear` | chaîne | Intérêt ou implication dans les chaussures. |
| [!UICONTROL healthFoods] | `healthFoods` | chaîne | Préférences ou implication dans les aliments pour la santé. |
| [!UICONTROL randonnée] | `hiking` | chaîne | Intérêt ou implication dans les activités de randonnée. |
| [!UICONTROL householdId] | `householdId` | chaîne | Identifiant unique du foyer. |
| [!UICONTROL individualId] | `individualId` | chaîne | Identifiant unique de l’individu. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | chaîne | L&#39;inférence d&#39;être détenteur de carte. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | chaîne | L’idée d’être détenteur de carte de crédit Premium. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | chaîne | Indicateur du niveau correspondant. |
| [!UICONTROL BuyerRating] | `buyerRating` | chaîne | Évaluation liée au comportement d’achat. |
| [!UICONTROL DonorRating] | `donorRating` | chaîne | Évaluation liée au comportement des donneurs. |
| [!UICONTROL Évaluation des investissements] | `investmentRating` | chaîne | Évaluation liée au comportement d’investissement. |
| [!UICONTROL ResponderRating] | `responderRating` | chaîne | Évaluation liée au comportement du participant. |
| [!UICONTROL Dépenses - Vitesse] | `spendingVelocity` | chaîne | La vitesse ou le taux de dépenses. |
| [!UICONTROL Volume des dépenses] | `spendingVolume` | chaîne | Montant ou volume des dépenses. |
| [!UICONTROL recordId] | `recordId` | chaîne | Identifiant unique de l’enregistrement. |
| [!UICONTROL RésidenceId] | `residenceId` | chaîne | Identifiant unique de la résidence. |
| [!UICONTROL navigation] | `sailing` | chaîne | Indique l’intérêt ou l’implication dans les activités de navigation. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | chaîne | Indique les préférences ou l’engagement dans les produits de vacances. |
| [!UICONTROL ski] | `skiing` | chaîne | Indique l’intérêt ou l’implication dans les activités de ski. |
| [!UICONTROL tennis] | `tennis` | chaîne | Indique l’intérêt ou l’implication dans les activités de tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | chaîne | Indique l’engagement avec les achats à la télévision. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) sur le référentiel XDM public.
