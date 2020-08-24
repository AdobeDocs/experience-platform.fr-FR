---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions diverses
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 79%

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
