---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de mappage
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 6%

---


# Fonctions de mappage

Les offres PQL (Profil Requête Language) facilitent l’interaction avec les cartes. Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Get

La `get` fonction est utilisée pour récupérer la valeur d’un mappage pour une clé donnée.

**Format**

```sql
{MAP}.get({STRING})
```

**Exemple**

La requête PQL suivante obtient la valeur de la carte d’identité de la clé `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Clés

La `keys` fonction est utilisée pour récupérer toutes les clés d’une carte donnée.

**Format**

```sql
{MAP}.keys()
```

**Exemple**

La requête PQL suivante récupère toutes les clés de la carte `identityMap`.

```sql
identityMap.keys()
```

## Valeurs

La `values` fonction est utilisée pour récupérer toutes les valeurs d’une carte donnée.

**Format**

```sql
{MAP}.values()
```

**Exemple**

La requête PQL suivante récupère toutes les valeurs de la carte `identityMap`.

```sql
identityMap.values()
```

## Étapes suivantes

Maintenant que vous avez pris connaissance des fonctions de carte, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.
