---
title: Type de données de l’article remboursé
description: Découvrez le type de données Refund Item Experience Data Model (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 14%

---

# [!UICONTROL Article de remboursement] type de données

[!UICONTROL Article de remboursement] est un type de données XDM (Experience Data Model) standard qui décrit la capture des informations liées à un remboursement associé à une commande.

![Schéma du type de données Article remboursé.](../images/data-types/refund-item.png)

| Nom d’affichage | Propriété | Type de données | Description |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID de transaction] | `transactionID` | chaîne | Identifiant de transaction unique pour cet article de remboursement. |
| [!UICONTROL Montant remboursé] | `refundAmount` | nombre | La valeur du remboursement. |
| [!UICONTROL Raison du remboursement] | `refundReason` | chaîne | La raison pour laquelle un remboursement a été effectué. |
| [!UICONTROL Type de paiement remboursé] | `refundPaymentType` | chaîne | Mode de paiement pour cette commande. Les valeurs personnalisées sont autorisées. |
| [!UICONTROL Code de devise] | `currencyCode` | chaîne | Code de devise ISO 4217 utilisé pour cet article de remboursement. Par exemple : &quot;USD&quot;, &quot;EUR&quot;. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
