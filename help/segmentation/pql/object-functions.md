---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions d’objet
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 91%

---


# Fonctions d’objet

[!DNL Profile Query Language] (PQL) offre des fonctions pour simplifier l’interaction avec les objets. Vous trouverez plus d’informations sur les autres fonctions PQL dans la [présentation du langage de requête de profil](./overview.md).

## Fonction isNull

La fonction `isNull` détermine si une référence d’objet n’existe pas.

**Format**

```sql
{OBJECT}.isNull()
```

**Exemple**

La requête PQL suivante vérifie si l’adresse de la personne n’existe pas.

```sql
person.homeAddress.isNull()
```

## Fonction isNotNull

La fonction `isNotNull` détermine si une référence d’objet existe.

**Format**

```sql
{OBJECT}.isNotNull()
```

**Exemple**

La requête PQL suivante vérifie si l’adresse de la personne existe.

```sql
person.homeAddress.isNotNull()
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions d’objet, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).