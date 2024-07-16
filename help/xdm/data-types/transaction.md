---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;transaction;type de données;type de données;type de données
title: Type de données de transaction
description: Découvrez le type de données du modèle de données d’expérience de transaction (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 7%

---

# Type de données [!UICONTROL Transaction]

[!UICONTROL Transaction] est un type de données XDM (Experience Data Model) standard qui décrit les détails d’une transaction monétaire.

![Structure de transaction](../images/data-types/transaction.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Devise]](./currency.md) | Décrit le montant de la devise échangée dans le cadre de la transaction. |
| `transactionDate` | [!UICONTROL DateTime] | Horodatage de la date de la transaction. |
| `transactionId` | [!UICONTROL Chaîne] | Identifiant unique de la transaction. |
| `transactionType` | [!UICONTROL Chaîne] | Type de transaction utilisé par le visiteur. |

{style="table-layout:auto"}
