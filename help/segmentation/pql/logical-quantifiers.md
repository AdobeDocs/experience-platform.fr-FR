---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Quantificateurs logiques
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 93%

---


# Fonctions de quantificateur logique

Logical quantifiers can be used to assert conditions with arrays in [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur les autres fonctions PQL dans la [présentation du langage de requête de profil](./overview.md).

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
