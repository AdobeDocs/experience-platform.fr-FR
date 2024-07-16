---
title: Type de données d’expédition
description: Découvrez le type de données du modèle de données d’expérience d’expédition (XDM).
exl-id: c3a58e46-c80e-4896-b21c-47dc5a6c869b
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 19%

---

# Type de données [!UICONTROL Shipping]

[!UICONTROL Expédition] est un type de données XDM (Experience Data Model) standard qui fournit des détails sur l’envoi d’un ou de plusieurs produits. Il contient des détails sur la logistique et des détails concernant la livraison des articles commandés.


![Schéma du type de données [!UICONTROL Shipping].](../images/data-types/shipping.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------|-----------------------|-----------|------------------------------------------------------|
| [!UICONTROL Méthode d’expédition] | `shippingMethod` | Chaîne | Mode d’expédition choisi par le client. |
| [!UICONTROL Montant de livraison] | `shippingAmount` | nombre | Montant que le client a dû payer pour l’expédition. |
| [!UICONTROL Code de devise] | `currencyCode` | Chaîne | Code de devise alphabétique ISO 4217 utilisé pour la tarification du produit. |
| [!UICONTROL Destination de livraison] | `shippingDestination` | Chaîne | Destination de livraison spécifiée par l’utilisateur (par exemple, accueil, magasin, etc.). |
| [!UICONTROL Date d’expédition] | `shipDate` | Chaîne | Date à laquelle un ou plusieurs articles d’une commande sont expédiés. |
| [!UICONTROL Adresse de livraison] | `address` | [[!UICONTROL address]](./address.md) | Adresse de livraison. |
| [!UICONTROL Numéro de suivi] | `trackingNumber` | nombre | Numéro de tracking fourni par le transporteur. |
| [!UICONTROL URL de tracking] | `trackingURL` | Chaîne | URL permettant de suivre l’état de livraison d’un article de commande. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json)
