---
solution: Experience Platform
title: Fonctions de date et d’heure PQL
description: Les fonctions de date et d’heure sont utilisées pour effectuer des opérations de date et d’heure sur des valeurs dans Profile Query Language (PQL).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 88%

---

# Fonctions de date et d’heure

Les fonctions de date et d’heure sont utilisées pour effectuer des opérations de date et d’heure sur des valeurs dans [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Current month

La fonction `currentMonth` renvoie le mois en cours sous la forme d’un entier.

**Format**

```sql
currentMonth()
```

**Exemple**

La requête PQL suivante vérifie si le mois de naissance de la personne est le mois en cours.

```sql
person.birthMonth = currentMonth()
```

## Get month

La fonction `getMonth` renvoie le mois, sous la forme d’un entier, en fonction d’un horodatage donné.

**Format**

```sql
{TIMESTAMP}.getMonth()
```

**Exemple**

La requête PQL suivante vérifie si le mois de naissance de la personne est le mois de juin.

```sql
person.birthdate.getMonth() = 6
```

## Current year

La fonction `currentYear` renvoie l’année en cours sous la forme d’un entier.

**Format**

```sql
currentYear()
```

**Exemple**

La requête PQL suivante vérifie si le produit a été vendu lors de l’année en cours.

```sql
product.saleYear = currentYear()
```

## Get year

La fonction `getYear` renvoie l’année, sous la forme d’un entier, en fonction d’un horodatage donné.

**Format**

```sql
{TIMESTAMP}.getYear()
```

**Exemple**

La requête PQL suivante vérifie si l’année de naissance de la personne est 1991, 1992, 1993, 1994 ou 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Current day of month

La fonction `currentDayOfMonth` renvoie le jour du mois en cours sous la forme d’un entier.

**Format**

```sql
currentDayOfMonth()
```

**Exemple**

La requête PQL suivante vérifie si le jour de naissance de la personne est le jour du mois en cours.

```sql
person.birthDay = currentDayOfMonth()
```

## Get day of month

La fonction `getDayOfMonth` renvoie le jour, sous la forme d’un entier, en fonction d’un horodatage donné.

**Format**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Exemple**

La requête PQL suivante vérifie si l’article a été vendu au cours des 15 premiers jours du mois.

```sql
product.sale.getDayOfMonth() <= 15
```

## Occurs

La fonction `occurs` compare la fonction d’horodatage donnée à une période fixe.

**Format**

La fonction `occurs` peut être rédigée dans l’un des formats suivants :

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Description |
| --------- | ----------- |
| `{COMPARISON}` | Opérateur de comparaison. Peut être l’un des opérateurs suivants : `>`, `>=`, `<`, `<=`, `=`, `!=`. Pour plus d’informations sur les fonctions de comparaison, consultez le [document sur les fonctions de comparaison](./comparison-functions.md). |
| `{INTEGER}` | Entier non négatif. |
| `{TIME_UNIT}` | Unité de temps. Peut être l’un des mots suivants : `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | Préposition décrivant à quel moment comparer la date. Peut être l’un des mots suivants : `before`, `after`, `from`. |
| `{TIME}` | Il peut s’agir d’un littéral d’horodatage (`today`, `now`, `yesterday`, `tomorrow`), d’une unité de temps relative (`this`, `last` ou `next` suivi d’une unité de temps) ou d’un attribut d’horodatage. |

>[!NOTE]
>
>L’utilisation du mot `on` est facultative. Il sert à améliorer la lisibilité de certaines combinaisons, comme `timestamp occurs on date(2019,12,31)`.

**Exemple**

La requête PQL suivante vérifie si l’article a été vendu la semaine précédente.

```sql
product.saleDate occurs last week
```

La requête PQL suivante vérifie si l’article a été vendu entre le 8 janvier 2015 et le 1er juillet 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Now

`now` est un mot réservé qui représente l’horodatage de l’exécution PQL.

**Exemple**

La requête PQL suivante vérifie si un article a été vendu il y a exactement trois heures.

```sql
product.saleDate occurs = 3 hours before now
```

## Today

`today` est un mot réservé qui représente l’horodatage du début du jour de l’exécution PQL.

**Exemple**

La requête PQL suivante vérifie si l’anniversaire d’une personne était il y a trois jours.

```sql
person.birthday occurs = 3 days before today
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de date et d’heure, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
