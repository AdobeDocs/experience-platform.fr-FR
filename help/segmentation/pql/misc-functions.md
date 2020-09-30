---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;miscellaneous functions;misc;
solution: Experience Platform
title: Fonctions diverses
topic: developer guide
description: La fonction suivante est une fonction diverse pour le langage de requête de profil (PQL).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 81%

---


# Fonctions diverses

The following function is a miscellaneous function for [!DNL Profile Query Language] (PQL). More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

## Let

La fonction `let` permet à une expression d’être stockée en tant que variable et d’être utilisé ultérieurement dans une requête.

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exemple**

La requête PQL suivante renvoie toutes les sommes des totaux des produits avec la transaction en USD lorsque la somme est supérieure à 100 USD et inférieure à 1000 USD.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions diverses, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
