---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de filtre
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 87%

---


# Fonctions de filtre

Filter functions are used to filter data within arrays in [!DNL Profile Query Language] (PQL). More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

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
