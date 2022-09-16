---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;commande;type de données;type de données;type de données
solution: Experience Platform
title: Type de données de commande
topic-legacy: overview
description: Ce document fournit un aperçu du type de données du modèle de données d’expérience de commande (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 30%

---

# [!UICONTROL Commande] type de données

[!UICONTROL Commande] est un type de données XDM (Experience Data Model) standard qui décrit la commande placée pour une liste de produits.

<img src="../images/data-types/order.PNG" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `payments` | Tableau de [[!UICONTROL Éléments de paiement]](./payment-item.md) | Liste des paiements pour cette commande. |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux des commandes. Toutes les instances doivent se conformer à l’expression régulière `^[A-Z]{3}$`. Par exemple `USD` et `EUR`. |
| `priceTotal` | Double | Prix total de cette commande une fois toutes les remises et taxes appliquées. |
| `purchaseID` | Chaîne | Identifiant unique attribué par le vendeur pour cet achat ou ce contrat. Étant donné que cet identifiant est défini par le vendeur, il n’y a aucune garantie que l’identifiant est unique. |
| `purchaseOrderNumber` | Chaîne | Identifiant unique attribué par l’acheteur pour cet achat ou ce contrat. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
