---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de mappage
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Fonctions de mappage

 langage  de (PQL)  fonctions delangage pour faciliter l’interaction avec les cartes. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Get

La `get` fonction est utilisée pour récupérer la valeur d’un mappage pour une clé donnée.

**Format**

```sql
{MAP}.get({STRING})
```

**Exemple**

Le PQL suivant obtient la valeur de la carte d’identité pour la clé `example@example.com`.

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

Le PQL suivant récupère toutes les clés de la carte `identityMap`.

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

Le PQL suivant récupère toutes les valeurs de la carte `identityMap`.

```sql
identityMap.values()
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions de carte, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).
