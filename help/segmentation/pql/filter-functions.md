---
solution: Experience Platform
title: Fonctions de filtre PQL
description: Les fonctions de filtrage sont utilisées pour filtrer les données dans les tableaux de Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
TQID: https://experienceleague.adobe.com/GeQYYItaeubvmw814w0Ecn0A0sc9M-1ehl1zGbcoTeM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 211
ht-degree: 66%

---

# Fonctions de filtre

Les fonctions de filtrage sont utilisées pour filtrer les données dans les tableaux d’[!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Filtre

La fonction `[]` (filtre) permet d’appliquer des filtres à un tableau et de renvoyer un sous-ensemble du tableau qui correspond à la condition spécifiée. Par conséquent, cette fonction renvoie un tableau.

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

La requête PQL suivante récupère tous les événements qui contiennent au moins un produit avec un SKU égal à « PS » **ou** qui contiennent une personne dont le genre est « féminin ».

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Étapes suivantes

Maintenant que vous connaissez les fonctions de filtre, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
