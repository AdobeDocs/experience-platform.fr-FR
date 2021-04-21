---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; commande ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données de commande
topic-legacy: overview
description: Ce document présente un aperçu du type de données du modèle de données d’expérience de commande (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 22%

---

# [!UICONTROL Type ] Orderdata

 Orderest un type de données XDM (Experience Data Model) standard qui décrit la commande passée pour une liste de produits.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `payments` | Tableau des [[!UICONTROL éléments de paiement]](./payment-item.md) | Liste des paiements pour cette commande. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux des commandes. Toutes les instances doivent se conformer à l&#39;expression régulière `^[A-Z]{3}$`. Par exemple `USD` et `EUR`. |
| `priceTotal` | Double | Prix total de cette commande une fois toutes les remises et taxes appliquées. |
| `purchaseID` | Chaîne | Identificateur unique attribué par le vendeur pour cet achat ou ce contrat. Étant donné que cette valeur est définie par le vendeur, il n’y a aucune garantie que l’ID est unique. |
| `purchaseOrderNumber` | Chaîne | Identificateur unique attribué par l&#39;acheteur pour cet achat ou ce contrat. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
