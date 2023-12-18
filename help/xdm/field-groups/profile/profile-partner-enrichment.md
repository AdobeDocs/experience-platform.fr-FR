---
title: Groupe de champs Enrichissement du partenaire de profil (exemple)
description: Découvrez le groupe de champs Enrichissement du partenaire de profil (exemple) .
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---


# [!UICONTROL Enrichissement du partenaire de profil (exemple)] groupe de champs de schéma

[!UICONTROL Enrichissement du partenaire de profil (exemple)] est un groupe de champs de schéma standard pour la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Utilisez ce groupe de champs pour fournir des données supplémentaires liées aux enrichissements pilotés par les partenaires pour les profils client.

![Un diagramme de [!UICONTROL Enrichissement du partenaire de profil (exemple)] groupe de champs.](../../images/field-groups/profile-partner-enrichment-sample.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | chaîne | La tranche d’âge au sein du foyer. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | chaîne | Données sur les vêtements et accessoires. |
| [!UICONTROL vélo] | `bicycling` | chaîne | Informations sur le vélo. |
| [!UICONTROL cableTv] | `cableTv` | chaîne | Informations relatives à la télévision par câble. |
| [!UICONTROL intérieurs] | `domestics` | chaîne | Données nationales. |
| [!UICONTROL électronique] | `electronics` | chaîne | Informations relatives à l’électronique. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | chaîne | Données sur les aliments et les boissons. |
| [!UICONTROL chaussures] | `footwear` | chaîne | Informations relatives aux chaussures. |
| [!UICONTROL healthFoods] | `healthFoods` | chaîne | Données sur les aliments pour la santé. |
| [!UICONTROL randonnée] | `hiking` | chaîne | Informations sur la randonnée. |
| [!UICONTROL householdId] | `householdId` | chaîne | Identifiant unique d’un foyer. |
| [!UICONTROL individualId] | `individualId` | chaîne | L’identifiant unique d’un individu. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | chaîne | Informations sur les titulaires de carte déduites. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | chaîne | Informations sur les titulaires de carte Premium déduites. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | chaîne | Correspondance des données d’indicateur de niveau. |
| [!UICONTROL BuyerRating] | `buyerRating` | chaîne | Informations sur la notation des acheteurs. |
| [!UICONTROL DonorRating] | `donorRating` | chaîne | Détails de la notation des donateurs. |
| [!UICONTROL Évaluation des investissements] | `investmentRating` | chaîne | Données de notation des investissements. |
| [!UICONTROL ResponderRating] | `responderRating` | chaîne | Informations d’évaluation des réponses. |
| [!UICONTROL Dépenses - Vitesse] | `spendingVelocity` | chaîne | Informations détaillées sur la vitesse. |
| [!UICONTROL Volume des dépenses] | `spendingVolume` | chaîne | Informations sur le volume des dépenses. |
| [!UICONTROL recordId] | `recordId` | chaîne | Identifiant d’enregistrement unique. |
| [!UICONTROL RésidenceId] | `residenceId` | chaîne | Identifiant unique de la résidence. |
| [!UICONTROL navigation] | `sailing` | chaîne | Données relatives à la navigation. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | chaîne | Informations sur les produits des vacances saisonnières. |
| [!UICONTROL ski] | `skiing` | chaîne | Données liées au ski. |
| [!UICONTROL tennis] | `tennis` | chaîne | Informations relatives au tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | chaîne | Informations sur les acheteurs de télévision. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) sur le référentiel XDM public.
