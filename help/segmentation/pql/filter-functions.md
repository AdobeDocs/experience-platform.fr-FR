---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de filtre
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Fonctions de filtre

Les fonctions de filtre sont utilisées pour filtrer les données dans les tableaux dans le langage  de (PQL). Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Filtrer

La fonction `[]` (filter) permet d&#39;appliquer des  à un tableau et de renvoyer un sous-ensemble du tableau correspondant à la condition spécifiée.

**Format**

```sql
{ARRAY}[filter]
```

**Exemple**

Le PQL suivant obtient tous les  qui ont au moins un article de produit avec un SKU égal à &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Opérateur Haut

L’opérateur `^` (supérieur) vous permet de faire référence aux propriétés des niveaux supérieurs des  de.

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Description |
| -------- | ----------- |
| `{ARRAY}` | Tableau en cours de filtrage. |
| `{FILTER_1}` | Couche extérieure du filtrage. |
| `{FILTER_2}` | Couche interne du filtrage |
| `^{PROPERTY}` | Propriété qui est également filtrée. En raison de `^`cette variable, il vérifie une propriété en fonction de filter1. |

**Exemple**

Le PQL suivant reçoit tous les  qui ont au moins un article avec un SKU égal à &quot;PS&quot; **ou qui** ont une personne de sexe féminin.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Étapes suivantes

Maintenant que vous connaissez les fonctions de filtre, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).
