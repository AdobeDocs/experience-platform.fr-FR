---
solution: Experience Platform
title: Fonctions de filtre PQL
description: Les fonctions de filtre sont utilisées pour filtrer les données dans des tableaux dans Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 80%

---

# Fonctions de filtre

Les fonctions de filtre sont utilisées pour filtrer les données dans des tableaux dans [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Filtrer

La fonction `[]` (filtrer) permet d’appliquer des filtres à un tableau et de renvoyer un sous-ensemble du tableau correspondant à la condition spécifiée.

**Format**

```sql
{ARRAY}[filter]
```

**Exemple**

La requête PQL suivante récupère tous les événements qui contiennent au moins un produit avec un SKU égal à « PS ».

```sql
xEvent[productListItems[SKU="PS"]]
```

## Opérateur « haut »

L’opérateur `^` (« haut ») vous permet de faire référence aux propriétés des niveaux supérieurs des filtres.

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Description |
| -------- | ----------- |
| `{ARRAY}` | Le tableau en cours de filtrage. |
| `{FILTER_1}` | La couche extérieure du filtrage. |
| `{FILTER_2}` | La couche intérieure du filtrage. |
| `^{PROPERTY}` | La propriété également en cours de filtrage. En raison du `^`, une propriété est en cours de vérification en fonction du filtre1. |

**Exemple**

La requête PQL suivante récupère tous les événements qui contiennent au moins un produit avec un SKU égal à « PS » **ou** qui contiennent un individu de sexe féminin.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Étapes suivantes

Maintenant que vous connaissez les fonctions de filtre, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
