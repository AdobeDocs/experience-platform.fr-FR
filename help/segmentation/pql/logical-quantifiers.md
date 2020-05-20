---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Quantificateurs logiques
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 5%

---


# Fonctions de quantificateur logique

Des quantificateurs logiques peuvent être utilisés pour affirmer des conditions avec des tableaux dans le langage PQL (Profil Requête Language). Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

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
| `{CONDITION}` | expression facultative qui filtres les valeurs du tableau renvoyées. |

**Exemple**

La requête PQL suivante récupère tous les événements dont le prix est supérieur à 50 $ ou dont le SKU est &quot;PS&quot;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Pour tous

La `forall` fonction détermine tous les éléments d&#39;un tableau qui répondent à toutes les conditions données.

**Format**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Description |
| ---------- | ----------- |
| `{VARIABLE}` | Nom d’une variable. |
| `{EXPRESSION}` | Tableau en cours de vérification. |
| `{CONDITION}` | expression facultative qui filtres les valeurs du tableau renvoyées. |

**Exemple**

La requête PQL suivante récupère tous les événements dont le prix est supérieur à 50 $ et dont le SKU est &quot;PS&quot;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Étapes suivantes

Maintenant que vous avez découvert les quantificateurs logiques, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.
