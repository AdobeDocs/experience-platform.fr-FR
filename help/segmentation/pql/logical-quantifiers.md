---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Quantificateurs logiques
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Fonctions de quantificateur logique

Des quantificateurs logiques peuvent être utilisés pour affirmer des conditions avec des tableaux dans le langage  de (PQL). Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Existe

La `exists` fonction détermine l&#39;existence d&#39;un élément dans un tableau, à condition qu&#39;elle satisfasse à la condition fournie.

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Description |
| ---------- | ----------- |
| `{VARIABLE}` | Nom d’une variable. |
| `{EXPRESSION}` | Tableau en cours de vérification. |
| `{CONDITION}` | Un  facultatif  qui les valeurs du tableau renvoyées. |

**Exemple**

Le PQL suivant reçoit tous les  dont le prix est supérieur à 50 $ ou dont le SKU est &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Pour tous

La `forall` fonction détermine tous les éléments d’un tableau qui répondent à toutes les conditions données.

**Format**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Description |
| ---------- | ----------- |
| `{VARIABLE}` | Nom d’une variable. |
| `{EXPRESSION}` | Tableau en cours de vérification. |
| `{CONDITION}` | Un  facultatif  qui les valeurs du tableau renvoyées. |

**Exemple**

Le PQL suivant reçoit tous les  dont le prix est supérieur à 50 $ et dont le SKU est &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Étapes suivantes

Maintenant que vous avez appris les quantificateurs logiques, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).
