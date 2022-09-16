---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;transaction;type de données;type de données;type de données
title: Type de données de transaction
description: Ce document présente un aperçu du type de données XDM (Transaction Experience Data Model).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: afbbdfff4346ab5240927f5703d3a06676776ea8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 10%

---

# [!UICONTROL Transaction] type de données

[!UICONTROL Transaction] est un type de données XDM (Experience Data Model) standard qui décrit les détails d’une transaction monétaire.

![Structure des transactions](../images/data-types/transaction.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Devise]](./currency.md) | Décrit le montant de la devise échangée dans le cadre de la transaction. |
| `transactionDate` | [!UICONTROL DateTime] | Horodatage du moment où la transaction a eu lieu. |
| `transactionId` | [!UICONTROL Chaîne] | Identifiant unique de la transaction. |
| `transactionType` | [!UICONTROL Chaîne] | Type de transaction utilisé par le visiteur. |

{style=&quot;table-layout:auto&quot;}
