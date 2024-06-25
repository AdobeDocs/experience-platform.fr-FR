---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;commande;type de données;type de données;type de données
solution: Experience Platform
title: Type de données de commande
description: Découvrez le type de données Order Experience Data Model (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 13%

---

# [!UICONTROL Commande] type de données

[!UICONTROL Commande] est un type de données XDM (Experience Data Model) standard qui décrit la commande placée pour une liste de produits.

![Un diagramme de [!UICONTROL Commande] type de données.](../images/data-types/order.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| Identifiant d’achat | `purchaseID` | Chaîne | Identifiant unique attribué par le vendeur pour cet achat ou ce contrat. Il n’existe aucune garantie que l’identifiant est unique, car il est défini par le vendeur. |
| Numéro de commande | `purchaseOrderNumber` | Chaîne | Identifiant unique attribué par l’acheteur pour cet achat ou ce contrat. |
| Liste de paiements | `payments` | Tableau de [[!UICONTROL Éléments de paiement]](./payment-item.md) | Liste des paiements pour cette commande. Les paiements sont présentés dans la section [!UICONTROL Éléments de paiement] spécification. |
| Liste des remboursements | `refunds` | Tableau de [[!UICONTROL Éléments remboursés]](./refund-item.md) | La liste des remboursements pour cette commande. Les remboursements sont présentés dans la section [!UICONTROL Éléments remboursés] spécification. |
| Infos sur le retour | `returns` | [[!UICONTROL Infos sur le retour]](./return.md) | La RMA (Return Merchandise Authorization) a été émise. Les retours sont détaillés dans la section [!UICONTROL Infos sur le retour] spécification. |
| Devise | `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux de commande. Exemples : `USD` et `EUR`. Toutes les instances doivent correspondre au modèle `^[A-Z]{3}$`. |
| Montant de la taxe | `taxAmount` | Nombre | Montant de l&#39;impôt payé par l&#39;acheteur dans le cadre du paiement final. |
| Montant de remise | `discountAmount` | Nombre | La différence entre le prix normal et le prix spécial appliqué à l&#39;ensemble de la commande, plutôt qu&#39;à des produits individuels. |
| Prix total | `priceTotal` | Nombre | Prix total de cette commande une fois toutes les remises et taxes appliquées. |
| Type de commande | `orderType` | Chaîne | Type de commande qui a été passée. Les valeurs possibles sont `checkout` et `instant_purchase`. |
| Date de la dernière mise à jour | `lastUpdatedDate` | Chaîne | Heure à laquelle un enregistrement de commande particulier est mis à jour pour la dernière fois dans le système commercial. Format : date et heure. |
| Date de création | `createdDate` | Chaîne | Heure/date de création d’une commande dans le système commercial. Format : date et heure. |
| Annuler la date | `cancelDate` | Chaîne | Date/heure à laquelle l’annulation d’une commande est initiée par l’acheteur. Format : date et heure. |
| Montant total remboursé | `refundTotal` | Nombre | Le montant total fourni dans ce remboursement sur la commande, combinant tous les articles remboursés et après toutes remises, etc. ont été appliquées. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
