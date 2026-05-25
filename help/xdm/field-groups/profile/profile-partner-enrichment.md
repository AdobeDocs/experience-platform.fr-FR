---
title: Groupe De Champs Enrichissement Du Partenaire De Profil (Exemple)
description: Découvrez le groupe de champs de schéma Enrichissement du partenaire de profil (exemple) .
exl-id: 02f7c358-3cf9-45cb-a5c5-e2cb1f140d93
TQID: https://experienceleague.adobe.com/s8gEz35cvyxrhdjGRM7pGLq-v7jwbjr-2Ew7D7Gh-v4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 218
ht-degree: 15%

---

# [!UICONTROL Profile Partner Enrichment (Sample)] groupe de champs de schéma

[!UICONTROL Profile Partner Enrichment (Sample)] groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Utilisez ce groupe de champs pour fournir des données supplémentaires liées aux enrichissements pilotés par les partenaires pour les profils clients.

![Diagramme du groupe de champs [!UICONTROL Profile Partner Enrichment (Sample)].](../../images/field-groups/profile-partner-enrichment-sample.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | chaîne | Tranche d’âge au sein du ménage. |
| [!UICONTROL apparelAccessories] | `apparelAccessories` | chaîne | Données sur les vêtements et accessoires. |
| [!UICONTROL bicycling] | `bicycling` | chaîne | Informations relatives au vélo. |
| [!UICONTROL cableTv] | `cableTv` | chaîne | Informations relatives à la télévision par câble. |
| [!UICONTROL domestics] | `domestics` | chaîne | Données nationales. |
| [!UICONTROL electronics] | `electronics` | chaîne | Informations relatives à l’électronique. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | chaîne | Données sur les aliments et les boissons. |
| [!UICONTROL footwear] | `footwear` | chaîne | Informations relatives aux chaussures. |
| [!UICONTROL healthFoods] | `healthFoods` | chaîne | Données sur les aliments sains. |
| [!UICONTROL hiking] | `hiking` | chaîne | Informations sur la randonnée. |
| [!UICONTROL householdId] | `householdId` | chaîne | ID unique d’un foyer. |
| [!UICONTROL individualId] | `individualId` | chaîne | ID unique d’une personne. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | chaîne | Informations déduites sur le titulaire de carte. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | chaîne | Détails du titulaire de carte Premium déduits. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | chaîne | Faire correspondre les données d&#39;indicateur de niveau. |
| [!UICONTROL BuyerRating] | `buyerRating` | chaîne | Informations sur la note de l&#39;acheteur. |
| [!UICONTROL DonorRating] | `donorRating` | chaîne | Détails de l’évaluation du donateur. |
| [!UICONTROL InvestmentRating] | `investmentRating` | chaîne | Données d’évaluation des investissements. |
| [!UICONTROL ResponderRating] | `responderRating` | chaîne | Informations d’évaluation du répondeur. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | chaîne | Détails sur la vitesse de dépense. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | chaîne | Informations sur le volume de dépenses. |
| [!UICONTROL recordId] | `recordId` | chaîne | Identifiant d’enregistrement unique. |
| [!UICONTROL residenceId] | `residenceId` | chaîne | ID unique de la résidence. |
| [!UICONTROL sailing] | `sailing` | chaîne | Données relatives à la navigation. |
| [!UICONTROL seasonalHolidayProducts] | `seasonalHolidayProducts` | chaîne | Informations sur les produits de vacances saisonnières. |
| [!UICONTROL skiing] | `skiing` | chaîne | Données relatives au ski. |
| [!UICONTROL tennis] | `tennis` | chaîne | Informations relatives au tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | chaîne | Informations sur les acheteurs de télévision. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) sur le référentiel XDM public.
