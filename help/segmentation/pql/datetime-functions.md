---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de date et d’heure
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Fonctions de date et d’heure

Les fonctions de date et d’heure sont utilisées pour effectuer des opérations de date et d’heure sur des valeurs dans le langage  de (PQL). Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans la présentation [du de la langue  du](./overview.md).

## Mois en cours

La `currentMonth` fonction renvoie le mois en cours sous la forme d’un entier.

**Format**

```sql
currentMonth()
```

**Exemple**

Le PQL suivant vérifie si le mois de naissance de la personne est le mois en cours.

```sql
person.birthMonth = currentMonth()
```

## Obtenir le mois

La `getMonth` fonction renvoie le mois, sous la forme d’un entier, en fonction d’un horodatage donné.

**Format**

```sql
{TIMESTAMP}.getMonth()
```

**Exemple**

Le PQL suivant vérifie si le mois de naissance de la personne est en juin.

```sql
person.birthdate.getMonth() = 6
```

## Année en cours

La `currentYear` fonction renvoie l’année en cours sous la forme d’un entier.

**Format**

```sql
currentYear()
```

**Exemple**

Le PQL suivant vérifie si le produit a été vendu au cours de l’année en cours.

```sql
product.saleYear = currentYear()
```

## Obtenir l&#39;année

La `getYear` fonction renvoie l’année, sous la forme d’un entier, en fonction d’un horodatage donné.

**Format**

```sql
{TIMESTAMP}.getYear()
```

**Exemple**

Le suivant de la LPQ  vérifier si l&#39;année de naissance de la personne tombe en 1991, 1992, 1993, 1994 ou 1995.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Jour actuel du mois

La `currentDayOfMonth` fonction renvoie le jour du mois en cours sous la forme d’un entier.

**Format**

```sql
currentDayOfMonth()
```

**Exemple**

Le PQL suivant vérifie si le jour de naissance de la personne correspond au jour du mois en cours.

```sql
person.birthDay = currentDayOfMonth()
```

## Obtenir le jour du mois

La `getDayOfMonth` fonction renvoie le jour, sous la forme d’un entier, en fonction d’un horodatage donné.

**Format**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Exemple**

Le PQL suivant vérifie si l’article a été vendu au cours des 15 premiers jours du mois.

```sql
product.sale.getDayOfMonth() <= 15
```

## Se produit

La `occurs` fonction compare la fonction d’horodatage donnée à une période fixe.

**Format**

La `occurs` fonction peut être écrite dans l’un des formats suivants :

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Description |
| --------- | ----------- |
| `{COMPARISON}` | Opérateur de comparaison. Peut être l’un des opérateurs suivants : `>`, `>=`, `<`, `<=`, `=`, `!=`. Vous trouverez plus d&#39;informations sur les fonctions de comparaison dans le des fonctions de [comparaison](./comparison-functions.md). |
| `{INTEGER}` | Entier non négatif. |
| `{TIME_UNIT}` | Une unité de temps. Peut être l’un des mots suivants : `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, , , , ,,.`year(s)``decade(s)``century``centuries``millennium``millennia` |
| `{DIRECTION}` | Une préposition décrivant à quel moment comparer la date. Peut être l’un des mots suivants : `before`, `after`, `from`. |
| `{TIME}` | Il peut s’agir d’un littéral d’horodatage (`today`, `now`, `yesterday`, `tomorrow`), d’une unité de temps relative (l’une des unités `this`, `last``next` ou suivie d’une unité de temps) ou d’un attribut d’horodatage. |

>[!NOTE] L’utilisation du mot `on` est facultative. Il est là pour améliorer la lisibilité de certaines combinaisons, comme `timestamp occurs on date(2019,12,31)`.

**Exemple**

Le PQL suivant vérifie si l’article a été vendu la semaine dernière.

```sql
product.saleDate occurs last week
```

Le PQL suivant vérifie si un article a été vendu entre le 8 janvier 2015 et le 1er juillet 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Maintenant

`now` est un mot réservé qui représente l’horodatage de l’exécution PQL.

**Exemple**

Le PQL suivant vérifie si un article a été vendu exactement trois heures auparavant.

```sql
product.saleDate occurs = 3 hours before now
```

## Aujourd&#39;hui

`today` est un mot réservé qui représente l’horodatage du  du jour de l’exécution PQL.

**Exemple**

Le PQL suivant vérifie si l&#39;anniversaire d&#39;une personne était il y a trois jours.

```sql
person.birthday occurs = 3 days before today
```

## Étapes suivantes

Maintenant que vous avez appris les fonctions de date et d’heure, vous pouvez les utiliser dans votre  PQL. Pour plus d&#39;informations sur les autres fonctions de PQL, veuillez lire la présentation [de la langue du](./overview.md).
