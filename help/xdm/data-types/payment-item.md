---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;champs;schémas;schémas;élément de paiement;type de données;type de données;type de données
solution: Experience Platform
title: Type de données de l’élément de paiement
description: Découvrez le type de données du modèle de données d’expérience (XDM) des éléments de paiement.
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 20%

---

# Type de données [!UICONTROL Article de paiement]

[!UICONTROL Article de paiement] est un type de données XDM (Experience Data Model) standard qui décrit un paiement associé à une commande qui définit le type de paiement, le montant et la devise associée.

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux de commande. Toutes les instances doivent se conformer à l’expression régulière `^[A-Z]{3}$`. Par exemple, `USD` et `EUR`. |
| `paymentAmount` | Double | Valeur du paiement. |
| `paymentType` | Chaîne | Mode de paiement pour cette commande. Les valeurs d’énumération acceptées sont les suivantes : <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Chaîne | Identifiant de transaction unique pour cet élément de paiement. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
