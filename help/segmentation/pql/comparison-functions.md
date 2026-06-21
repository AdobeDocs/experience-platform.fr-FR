---
solution: Experience Platform
title: Fonctions de comparaison de PQL
description: Les fonctions de comparaison sont utilisées pour comparer les différentes expressions et valeurs, renvoyant « true » ou « false » en conséquence.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
TQID: https://experienceleague.adobe.com/tlSxTCl0xpwnAHz-O1PaJl8wowkiBg5WNuZClccB4W4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 309
ht-degree: 89%

---

# Fonctions de comparaison

Les fonctions de comparaison sont utilisées pour comparer les différentes expressions et valeurs, renvoyant `true` ou `false` en conséquence. Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Égal à

La fonction `=` (égal à) vérifie si une valeur ou expression est égale à une autre valeur ou expression.

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Exemple**

La requête PQL suivante vérifie si le pays de l’adresse du domicile est le Canada.

```sql
homeAddress.countryISO = "CA"
```

## Différent de

La fonction `!=` (différent de) vérifie si une valeur ou expression est **différente** d&#39;une autre valeur ou expression.

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**Exemple**

La requête PQL suivante vérifie si le pays de l’adresse du domicile n’est pas le Canada.

```sql
homeAddress.countryISO != "CA"
```

## Supérieur à

La fonction `>` (supérieur à) permet de vérifier si la première valeur est supérieure à la seconde.

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire ne tombe ni en janvier ni en février.

```sql
person.birthMonth > 2
```

## Supérieur ou égal à

La fonction `>=` (supérieur ou égal à) permet de vérifier si la première valeur est supérieure ou égale à la seconde.

**Format**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire ne tombe ni en janvier ni en février.

```sql
person.birthMonth >= 3
```

## Inférieur à

La fonction `<` (inférieur à) permet de vérifier si la première valeur est inférieure à la seconde.

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire tombe en janvier.

```sql
person.birthMonth < 2
```

## Inférieur ou égal à

La fonction `<=` (inférieur ou égal à) permet de vérifier si la première valeur est inférieure ou égale à la seconde.

**Format**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Exemple**

La requête PQL suivante définit les personnes dont l’anniversaire tombe en janvier ou en février.

```sql
person.birthMonth <= 2
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de comparaison, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
