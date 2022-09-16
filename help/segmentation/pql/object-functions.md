---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;pql;PQL;langage de requête de profil;fonctions d’objet;objet;
solution: Experience Platform
title: Fonctions d’objet PQL
topic-legacy: developer guide
description: Le langage de requête de profil (PQL) offre des fonctions pour faciliter l’interaction avec les objets.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 70%

---

# Fonctions d’objet

[!DNL Profile Query Language] (PQL) offre des fonctions pour faciliter l’interaction avec les objets. Vous trouverez plus d’informations sur les autres fonctions PQL dans la section [[!DNL Profile Query Language] aperçu](./overview.md).

## Est nul

La fonction `isNull` détermine si une référence d&#39;objet n&#39;existe pas.

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

La fonction `isNotNull` détermine si une référence d&#39;objet existe.

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
