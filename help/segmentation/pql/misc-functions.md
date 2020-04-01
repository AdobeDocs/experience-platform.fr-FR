---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions diverses
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480

---


# Fonctions diverses

La fonction suivante est une fonction diverse pour le  de langue  (PQL). Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Laisser

La `let` fonction permet à un  d&#39;être stocké en tant que variable et d&#39;être utilisé ultérieurement dans un .

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exemple**

Le PQL suivant obtient toutes les sommes des totaux des produits avec la transaction en USD lorsque la somme est supérieure à 100 $ et inférieure à 1000 $.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Étapes suivantes

Maintenant que vous avez appris les différentes fonctions, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).
