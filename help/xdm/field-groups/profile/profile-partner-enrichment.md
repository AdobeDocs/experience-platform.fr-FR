---
title: Groupe de champs Enrichissement du partenaire de profil (exemple)
description: Découvrez le groupe de champs Enrichissement du partenaire de profil (exemple) .
exl-id: 02f7c358-3cf9-45cb-a5c5-e2cb1f140d93
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---

# [!UICONTROL Enrichissement du partenaire de profil (exemple)] groupe de champs de schéma

[!UICONTROL Enrichissement de partenaire de profil (échantillon)] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Utilisez ce groupe de champs pour fournir des données supplémentaires liées aux enrichissements pilotés par les partenaires pour les profils client.

![ Diagramme du groupe de champs [!UICONTROL Enrichissement de partenaire de profil (échantillon)].](../../images/field-groups/profile-partner-enrichment-sample.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | Chaîne | La tranche d’âge au sein du foyer. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | Chaîne | Données sur les vêtements et accessoires. |
| [!UICONTROL vélo] | `bicycling` | Chaîne | Informations sur le vélo. |
| [!UICONTROL cableTv] | `cableTv` | Chaîne | Informations relatives à la télévision par câble. |
| [!UICONTROL domestitics] | `domestics` | Chaîne | Données nationales. |
| [!UICONTROL électronique] | `electronics` | Chaîne | Informations relatives à l’électronique. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Chaîne | Données sur les aliments et les boissons. |
| [!UICONTROL chaussures] | `footwear` | Chaîne | Informations relatives aux chaussures. |
| [!UICONTROL healthFoods] | `healthFoods` | Chaîne | Données sur les aliments pour la santé. |
| [!UICONTROL randonnée] | `hiking` | Chaîne | Informations sur la randonnée. |
| [!UICONTROL householdId] | `householdId` | Chaîne | Identifiant unique d’un foyer. |
| [!UICONTROL individualId] | `individualId` | Chaîne | L’identifiant unique d’un individu. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | Chaîne | Informations sur les titulaires de carte déduites. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | Chaîne | Informations sur les titulaires de carte Premium déduites. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | Chaîne | Correspondance des données d’indicateur de niveau. |
| [!UICONTROL BuyerRating] | `buyerRating` | Chaîne | Informations sur la notation des acheteurs. |
| [!UICONTROL DonorRating] | `donorRating` | Chaîne | Détails de la notation des donateurs. |
| [!UICONTROL InvestmentRating] | `investmentRating` | Chaîne | Données de notation des investissements. |
| [!UICONTROL ResponderRating] | `responderRating` | Chaîne | Informations d’évaluation des réponses. |
| [!UICONTROL &rbrace;DépensesVelocity] | `spendingVelocity` | Chaîne | Informations détaillées sur la vitesse. |
| [!UICONTROL DépensesVolume] | `spendingVolume` | Chaîne | Informations sur le volume des dépenses. |
| [!UICONTROL recordId] | `recordId` | Chaîne | Identifiant d’enregistrement unique. |
| [!UICONTROL RésidenceId] | `residenceId` | Chaîne | Identifiant unique de la résidence. |
|  | `sailing` | Chaîne | Données relatives à la navigation. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Chaîne | Informations sur les produits des vacances saisonnières. |
| [!UICONTROL skiing] | `skiing` | Chaîne | Données liées au ski. |
| [!UICONTROL tennis] | `tennis` | Chaîne | Informations relatives au tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Chaîne | Informations sur les acheteurs de télévision. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) sur le référentiel XDM public.
