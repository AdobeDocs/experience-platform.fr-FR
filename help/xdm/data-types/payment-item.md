---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;élément de paiement;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'élément de paiement
description: Découvrez le type de données Modèle de données d'expérience des articles de paiement (XDM).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 19%

---

# Type de données [!UICONTROL Élément de paiement]

[!UICONTROL Élément de paiement] est un type de données standard du modèle de données d’expérience (XDM) qui décrit un paiement associé à une commande qui définit le type de paiement, le montant et la devise associée.

![image de l’élément de paiement](../images/data-types/payment-item.PNG){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux des commandes. Toutes les instances doivent être conformes au `^[A-Z]{3}$` d’expression régulière. Par exemple, `USD` et `EUR`. |
| `paymentAmount` | Double | Valeur du paiement. |
| `paymentType` | Chaîne | Mode de paiement pour cette commande. Les valeurs d’énumération acceptées sont les suivantes : <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Chaîne | Identifiant de transaction unique pour cet élément de paiement. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
