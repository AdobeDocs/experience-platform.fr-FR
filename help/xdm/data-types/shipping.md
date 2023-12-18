---
title: Type de données d’expédition
description: Découvrez le type de données du modèle de données d’expérience d’expédition (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 11%

---

# [!UICONTROL Expédition] type de données

[!UICONTROL Expédition] est un type de données XDM (Experience Data Model) standard qui fournit des détails relatifs à l’envoi d’un ou de plusieurs produits. Il contient des détails sur la logistique et des détails concernant la livraison des articles commandés.


![Un diagramme de [!UICONTROL Expédition] type de données.](../images/data-types/shipping.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Mode d’expédition] | `shippingMethod` | chaîne | Mode d’expédition choisi par le client. |
| [!UICONTROL Montant de l&#39;expédition] | `shippingAmount` | nombre | Le montant que le client a dû payer pour l’expédition. |
| [!UICONTROL Code de devise] | `currencyCode` | chaîne | Code de devise alphabétique ISO 4217 utilisé pour évaluer le produit. |
| [!UICONTROL Destination de livraison] | `shippingDestination` | chaîne | Destination de livraison spécifiée par l’utilisateur (par exemple, accueil, magasin, etc.). |
| [!UICONTROL Date d’expédition] | `shipDate` | chaîne | Date à laquelle un ou plusieurs articles d’une commande sont expédiés. |
| [!UICONTROL Adresse d’expédition] | `address` | [[!UICONTROL address]](./address.md) | Adresse de livraison. |
| [!UICONTROL Numéro de suivi] | `trackingNumber` | nombre | Numéro de tracking fourni par le transporteur. |
| [!UICONTROL URL de tracking] | `trackingURL` | chaîne | URL permettant de suivre l’état de livraison d’un article de commande. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
