---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;Schéma;XDM;champs;schémas;Schémas;transaction;type de données;type de données;
title: Type de données de transaction
description: Découvrez le type de données du modèle de données d’expérience des transactions (XDM).
exl-id: 47b7152f-a853-44f0-8962-e902631ad8a4
TQID: https://experienceleague.adobe.com/zlfRiaf0UxV3PPvE7LP-7zdXBPOaTLRsu7OxA7zR7cA
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 87
ht-degree: 4%

---

# Type de données [!UICONTROL Transaction]

[!UICONTROL Transaction] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les détails d’une transaction monétaire.

![Structure des transactions](../images/data-types/transaction.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `transactionAmount` | [[!UICONTROL Currency]](./currency.md) | Décrit le montant de la devise échangée dans le cadre de la transaction. |
| `transactionDate` | [!UICONTROL DateTime] | Date et heure du moment où la transaction a eu lieu. |
| `transactionId` | [!UICONTROL String] | Identifiant unique de la transaction. |
| `transactionType` | [!UICONTROL String] | Type de transaction utilisé par le visiteur ou la visiteuse. |

{style="table-layout:auto"}
