---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;Schéma;XDM;champs;schémas;Schémas;ordre;type de données;type de données;
solution: Experience Platform
title: Type de données de commande
description: Découvrez le type de données Modèle de données d’expérience des commandes (XDM) .
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
TQID: https://experienceleague.adobe.com/Z1P78jwJzXEmEOCtjSK9YoWkpK41BGJD9FNWfZPFQ2k
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
source-wordcount: 373
ht-degree: 17%

---

# Type de données [!UICONTROL Order]

[!UICONTROL Order] est un type de données XDM (modèle de données d’expérience) standard qui décrit la commande passée pour une liste de produits.

![Diagramme du type de données [!UICONTROL Order].](../images/data-types/order.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| Identifiant d’achat | `purchaseID` | Chaîne | Identifiant unique attribué par le vendeur à cet achat ou à ce contrat. Rien ne garantit que cet ID est unique, car il est défini par le vendeur. |
| Numéro de commande | `purchaseOrderNumber` | Chaîne | Identifiant unique attribué par l’acheteur à cet achat ou à ce contrat. |
| Liste de paiements | `payments` | Tableau de [[!UICONTROL Payment Items]](./payment-item.md) | Liste des paiements pour cette commande. Les paiements sont détaillés dans le cahier des charges [!UICONTROL Payment Items]. |
| Liste des remboursements | `refunds` | Tableau de [[!UICONTROL Refund Items]](./refund-item.md) | Liste des remboursements pour cette commande. Les restitutions sont détaillées dans le cahier des charges [!UICONTROL Refund Items]. |
| Informations sur le retour | `returns` | [[!UICONTROL Return Info]](./return.md) | La RMA (autorisation de renvoi de marchandises) a été émise. Les retours sont détaillés dans la spécification [!UICONTROL Return Info]. |
| Devise | `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux des commandes. Par exemple, `USD` et `EUR`. Toutes les instances doivent correspondre au modèle `^[A-Z]{3}$`. |
| Montant de la taxe | `taxAmount` | Nombre | Montant de la taxe payée par l&#39;acheteur dans le cadre du paiement final. |
| Montant de la remise | `discountAmount` | Nombre | Différence entre le prix normal et le prix spécial appliqué à l’ensemble de la commande, plutôt qu’à des produits individuels. |
| Prix total | `priceTotal` | Nombre | Prix total de cette commande une fois toutes les remises et taxes appliquées. |
| Type de commande | `orderType` | Chaîne | Type de commande qui a été passée. Les valeurs possibles sont `checkout` et `instant_purchase`. |
| Date de la dernière mise à jour | `lastUpdatedDate` | Chaîne | Heure à laquelle un enregistrement de commande particulier est mis à jour pour la dernière fois dans le système Commerce. Format : date-heure. |
| Date de création | `createdDate` | Chaîne | Date/heure de création d’une nouvelle commande dans le système Commerce. Format : date-heure. |
| Date d’annulation | `cancelDate` | Chaîne | Date/heure à laquelle l’acheteur a annulé une commande. Format : date-heure. |
| Montant total remboursé | `refundTotal` | Nombre | Montant total fourni dans ce remboursement sur la commande, combinant tous les articles remboursés et après application des remises, etc. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
