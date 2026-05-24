---
solution: Experience Platform
title: Fonctions d’objet PQL
description: Profile Query Language (PQL) offre des fonctions permettant de simplifier l’interaction avec les objets .
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
TQID: https://experienceleague.adobe.com/IMiDHJ3jbAsE2vSuIYYdqYYZkBpMk1GeToS0oqi3Qw4
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 127
ht-degree: 52%

---

# Fonctions d’objet

[!DNL Profile Query Language] (PQL) offre des fonctions permettant de simplifier l’interaction avec les objets . Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Est nul

La fonction `isNull` détermine si une référence d&#39;objet n&#39;existe pas sous forme booléenne.

**Format**

```sql
{OBJECT}.isNull()
```

**Exemple**

La requête PQL suivante vérifie si l’adresse de la personne n’existe pas.

```sql
person.homeAddress.isNull()
```

## N’est pas nul

La fonction `isNotNull` détermine si une référence d&#39;objet existe sous forme booléenne.

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
