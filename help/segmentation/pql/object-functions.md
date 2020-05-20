---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions d'objet
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 5%

---


# Fonctions d&#39;objet

Les offres PQL (Profil Requête Language) simplifient l’interaction avec les objets. Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## Est nul

La `isNull` fonction détermine si une référence d’objet n’existe pas.

**Format**

```sql
{OBJECT}.isNull()
```

**Exemple**

La requête PQL suivante vérifie si l’adresse de domicile de la personne n’existe pas.

```sql
person.homeAddress.isNull()
```

## N’est pas nul

La `isNotNull` fonction détermine s’il existe une référence d’objet.

**Format**

```sql
{OBJECT}.isNotNull()
```

**Exemple**

La requête PQL suivante vérifie si l&#39;adresse de domicile de la personne existe.

```sql
person.homeAddress.isNotNull()
```

## Étapes suivantes

Maintenant que vous avez pris connaissance des fonctions d’objet, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.