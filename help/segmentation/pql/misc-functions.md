---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;pql;PQL;langage de requête de profil;fonctions diverses;divers
solution: Experience Platform
title: Fonctions diverses PQL
topic-legacy: developer guide
description: La fonction suivante est une fonction diverse pour le langage de requête de profil (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 68%

---

# Fonctions diverses

La fonction suivante est une fonction diverse pour [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur les autres fonctions PQL dans la section [[!DNL Profile Query Language] aperçu](./overview.md).

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
