---
solution: Experience Platform
title: Fonctions d’objet PQL
description: Profile Query Language (PQL) offre des fonctions pour faciliter l’interaction avec les objets.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 70%

---

# Fonctions d’objet

[!DNL Profile Query Language] (PQL) offre des fonctions pour faciliter l’interaction avec les objets. Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

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
