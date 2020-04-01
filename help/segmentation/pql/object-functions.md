---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions d’objet
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Fonctions d’objet

 langage  de (PQL)  les fonctions del’algorithme pour simplifier l’interaction avec les objets. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Est nul

La `isNull` fonction détermine si une référence d’objet n’existe pas.

**Format**

```sql
{OBJECT}.isNull()
```

**Exemple**

Le PQL suivant vérifie si l’adresse de la personne n’existe pas.

```sql
person.homeAddress.isNull()
```

## N’est pas nul

La `isNotNull` fonction détermine s’il existe une référence à un objet.

**Format**

```sql
{OBJECT}.isNotNull()
```

**Exemple**

Le PQL suivant vérifie si l’adresse de la personne existe.

```sql
person.homeAddress.isNotNull()
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions des objets, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).