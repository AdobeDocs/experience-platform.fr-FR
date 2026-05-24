---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;élément de paiement;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'élément de paiement
description: Découvrez le type de données Modèle de données d'expérience des articles de paiement (XDM).
exl-id: d25a358b-73c1-468b-a9c5-808385689932
TQID: https://experienceleague.adobe.com/lxki-3fVq4DqBDEX1eyRiYsUq81pqOzkoBBghlkxI0Q
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 159
ht-degree: 23%

---

# Type de données [!UICONTROL Payment Item]

[!UICONTROL Payment Item] est un type de données XDM (modèle de données d’expérience) standard qui décrit un paiement associé à une commande qui définit le type de paiement, le montant et la devise associée.

![image de l’élément de paiement](../images/data-types/payment-item.PNG){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `currencyCode` | Chaîne | Code de devise ISO 4217 utilisé pour les totaux des commandes. Toutes les instances doivent être conformes au `^[A-Z]{3}$` d’expression régulière. Par exemple, `USD` et `EUR`. |
| `paymentAmount` | Double | Valeur du paiement. |
| `paymentType` | Chaîne | Mode de paiement pour cette commande. Les valeurs d’énumération acceptées sont les suivantes : <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | Chaîne | Identifiant de transaction unique pour cet élément de paiement. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
