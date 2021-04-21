---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; élément de paiement ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données de l'élément de paiement
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Payment Item Experience Data Model).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 24%

---

# [!UICONTROL Type ] d&#39;élément de paiement

[!UICONTROL Les ] éléments de paiement sont un type de données XDM (Experience Data Model) standard qui décrit un paiement associé à une commande qui définit le type de paiement, le montant et la devise associée.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux des commandes. Toutes les instances doivent se conformer à l&#39;expression régulière `^[A-Z]{3}$`. Par exemple `USD` et `EUR`. |
| `paymentAmount` | Double | Valeur du paiement. |
| `paymentType` | Chaîne | Mode de paiement pour cette commande. Les valeurs d’énumération acceptées sont les suivantes : <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Chaîne | Identifiant de transaction unique pour cet élément de paiement. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
