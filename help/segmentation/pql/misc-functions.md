---
solution: Experience Platform
title: Fonctions diverses de PQL
description: La fonction suivante est une fonction diverse pour Profile Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
TQID: https://experienceleague.adobe.com/Faf7-3YJ2i5AbzAPx4kkI3KpfwyQ-1UwaTF9ElDaw-w
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 117
ht-degree: 69%

---

# Fonctions diverses

La fonction suivante est une fonction diverse pour [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Let

La fonction `let` permet à une expression d&#39;être stockée en tant que variable et d&#39;être utilisé ultérieurement dans une requête.

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
