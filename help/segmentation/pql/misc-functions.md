---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions diverses
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Fonctions diverses

La fonction suivante est une fonction diverse pour PQL (Profil Requête Language). Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Let

La `let` fonction permet à une expression d&#39;être stockée en tant que variable et d&#39;être utilisée ultérieurement dans une requête.

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Exemple**

La requête PQL suivante récupère toutes les sommes de totaux de produits avec la transaction en USD lorsque la somme est supérieure à 100 $ et inférieure à 1000 $.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Étapes suivantes

Maintenant que vous avez pris connaissance de diverses fonctions, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.
