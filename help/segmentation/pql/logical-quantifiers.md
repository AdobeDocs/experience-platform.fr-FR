---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: Quantificateurs logiques
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 87%

---


# Fonctions de quantificateur logique

Logical quantifiers can be used to assert conditions with arrays in [!DNL Profile Query Language] (PQL). More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

## Existe

La fonction `exists` détermine la présence d’un élément dans un tableau à condition qu’il remplisse la condition indiquée.

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Description |
| ---------- | ----------- |
| `{VARIABLE}` | Un nom de variable. |
| `{EXPRESSION}` | Le tableau en cours de vérification. |
| `{CONDITION}` | Une expression facultative qui filtre les valeurs du tableau renvoyé. |

**Exemple**

La requête PQL suivante récupère tous les événements dont le prix est supérieur à 50 $ ou qui ont un SKU « PS ».

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Pour tous

La fonction `forall` détermine tous les éléments d’un tableau qui répondent à toutes les conditions données.

**Format**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Description |
| ---------- | ----------- |
| `{VARIABLE}` | Un nom de variable. |
| `{EXPRESSION}` | Le tableau en cours de vérification. |
| `{CONDITION}` | Une expression facultative qui filtre les valeurs du tableau renvoyé. |

**Exemple**

La requête PQL suivante récupère tous les événements dont le prix est supérieur à 50 $ et qui ont un SKU « PS ».

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Étapes suivantes

Maintenant que vous en savez plus sur les quantificateurs logiques, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
