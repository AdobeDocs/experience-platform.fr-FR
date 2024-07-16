---
solution: Experience Platform
title: Fonctions diverses de PQL
description: La fonction suivante est une fonction diverse pour Profile Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 69%

---

# Fonctions diverses

La fonction suivante est une fonction diverse pour [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

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
