---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;pql;PQL;langage de requête de profil;fonctions de comparaison;comparaison;
solution: Experience Platform
title: Fonctions de comparaison PQL
description: Les fonctions de comparaison sont utilisées pour comparer différentes expressions et valeurs, renvoyant "true" ou "false" en conséquence.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 85%

---

# Fonctions de comparaison

Les fonctions de comparaison sont utilisées pour comparer les différentes expressions et valeurs, renvoyant `true` ou `false` en conséquence. Vous trouverez plus d’informations sur les autres fonctions PQL dans la section [[!DNL Profile Query Language] aperçu](./overview.md).

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
