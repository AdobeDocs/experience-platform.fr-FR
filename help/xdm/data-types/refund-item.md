---
title: Type de données d'article remboursé
description: Découvrez le type de données Modèle de données d’expérience d’élément de remboursement (XDM).
exl-id: 9968d314-c6f3-49d9-b860-709d7478c43a
TQID: https://experienceleague.adobe.com/pBCWrK7q8XLQPXFAtg3jUPC6OiCYdSHnNo1mX-9IsaQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 11%

---

# Type de données [!UICONTROL Article remboursé]

[!UICONTROL Article remboursé] est un type de données standard du modèle de données d’expérience (XDM) qui décrit les informations relatives à un remboursement associé à une commande.

![Diagramme du type de données Article remboursé.](../images/data-types/refund-item.png)

| Nom d’affichage | Propriété | Type de données | Description |
|--------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------------|
| [!UICONTROL ID de transaction] | `transactionID` | chaîne | Identifiant de transaction unique pour cet article remboursé. |
| [!UICONTROL &#x200B; Montant du remboursement &#x200B;] | `refundAmount` | nombre | Valeur du remboursement. |
| [!UICONTROL Motif du remboursement] | `refundReason` | chaîne | Motif pour lequel un remboursement a été émis. |
| [!UICONTROL Type de paiement du remboursement] | `refundPaymentType` | chaîne | Mode de paiement pour cette commande. Les valeurs personnalisées sont autorisées. |
| [!UICONTROL Code de devise] | `currencyCode` | chaîne | Code de devise ISO 4217 utilisé pour cet élément de remboursement. Par exemple : « USD », « EUR ». |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/refunditem.schema.json)
