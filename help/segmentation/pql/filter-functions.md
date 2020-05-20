---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de filtrage
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 4%

---


# Fonctions de filtrage

Les fonctions de filtre sont utilisées pour filtrer les données dans les tableaux dans le langage PQL (Profil Requête Language). Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Filtrer

La fonction `[]` (filter) permet d&#39;appliquer des filtres à un tableau et de renvoyer un sous-ensemble du tableau correspondant à la condition spécifiée.

**Format**

```sql
{ARRAY}[filter]
```

**Exemple**

La requête PQL suivante récupère tous les événements qui ont au moins un article de produit avec un SKU égal à &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Opérateur montant

L’opérateur `^` (supérieur) vous permet de faire référence aux propriétés des niveaux supérieurs des filtres.

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Description |
| -------- | ----------- |
| `{ARRAY}` | Tableau en cours de filtrage. |
| `{FILTER_1}` | Couche extérieure du filtrage. |
| `{FILTER_2}` | Couche interne du filtrage |
| `^{PROPERTY}` | Propriété qui fait également l’objet d’un filtrage. En raison de la `^`variable, il vérifie une propriété basée sur filter1. |

**Exemple**

La requête PQL suivante récupère tous les événements qui ont au moins un article avec un SKU égal à &quot;PS&quot; **ou qui** ont une personne dont le sexe est féminin.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Étapes suivantes

Maintenant que vous avez pris connaissance des fonctions de filtrage, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.
