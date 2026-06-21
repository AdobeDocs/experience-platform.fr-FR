---
title: Type de données d’expédition
description: Découvrez le type de données du modèle de données d’expérience d’expédition (XDM).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
TQID: https://experienceleague.adobe.com/s-0-gPkJuCWxtmGSTr3W0co82X64743FXraYpfJfF3A
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
source-wordcount: 203
ht-degree: 11%

---

# Type de données [!UICONTROL Expédition]

[!UICONTROL Expédition] est un type de données standard des modèles de données d’expérience (XDM) qui fournit des détails liés à l’expédition d’un ou de plusieurs produits. Il comprend des détails sur la logistique et les détails concernant la livraison des articles commandés.


![Diagramme du type de données [!UICONTROL Expédition].](../images/data-types/shipping.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Mode d’expédition] | `shippingMethod` | chaîne | Mode d’expédition choisi par le client. |
| [!UICONTROL Montant de l’expédition] | `shippingAmount` | nombre | Montant que le client a dû payer pour l’expédition. |
| [!UICONTROL Code de devise] | `currencyCode` | chaîne | Code de devise alphabétique ISO 4217 utilisé pour la tarification du produit. |
| [!UICONTROL Destination d’expédition] | `shippingDestination` | chaîne | Destination de livraison spécifiée par l’utilisateur (par exemple, domicile, magasin, etc.). |
| [!UICONTROL Date d’expédition] | `shipDate` | chaîne | Date à laquelle un ou plusieurs articles d&#39;une commande sont expédiés. |
| [!UICONTROL Adresse d’expédition] | `address` | [[!UICONTROL adresse]](./address.md) | Adresse d’expédition. |
| [!UICONTROL Numéro de suivi] | `trackingNumber` | nombre | Numéro de suivi fourni par le transporteur. |
| [!UICONTROL URL de tracking] | `trackingURL` | chaîne | URL permettant de suivre le statut d&#39;expédition d&#39;un article de commande. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
