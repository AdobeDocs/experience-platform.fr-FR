---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;object functions;object;
solution: Experience Platform
title: Fonctions d’objet
topic: developer guide
description: Le langage de requête de profil (PQL) offre des fonctions pour faciliter l’interaction avec les objets.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 82%

---


# Fonctions d’objet

[!DNL Profile Query Language] (PQL) offre des fonctions pour simplifier l’interaction avec les objets. More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

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