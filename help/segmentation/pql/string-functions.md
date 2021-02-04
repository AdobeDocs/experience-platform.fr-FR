---
keywords: Experience Platform;accueil;rubriques populaires;segmentation;Segmentation;Segmentation Service;pql;PQL;Profil Requête Language;string fonctions;string;
solution: Experience Platform
title: Fonctions de chaîne
topic: developer guide
description: Le langage de requête de profil (PQL) offre des fonctions pour faciliter l’interaction avec les chaînes.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 95%

---


# Fonctions de chaîne

[!DNL Profile Query Language] (PQL) offre les fonctions pour rendre l&#39;interaction avec les chaînes plus simple. Vous trouverez plus d&#39;informations sur les autres fonctions PQL dans le [[!DNL Profile Query Language] overview](./overview.md).

## Like

La fonction `like` permet de déterminer si une chaîne correspond à un modèle donné.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | L’expression à laquelle comparer la première chaîne. Les deux caractères spéciaux pris en charge pour créer une expression sont `%` et `_`. <ul><li>`%` est utilisé pour représenter aucun ou plusieurs caractères.</li><li>`_` est utilisé pour représenter exactement un caractère.</li></ul> |

**Exemple**

La requête PQL suivante récupère toutes les villes contenant le modèle « es ».

```sql
city like "%es%"
```

## Starts with

La fonction `startsWith` permet de déterminer si une chaîne commence par une sous-chaîne donnée.

**Format**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Un paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur vraie. |

**Exemple**

La requête PQL suivante détermine si le nom de la personne commence par « Joe » en respectant la casse.

```sql
person.name.startsWith("Joe")
```

## Does not start with

La fonction `doesNotStartWith` permet de déterminer si une chaîne ne commence pas par une sous-chaîne donnée.

**Format**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Un paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur vraie. |

**Exemple**

La requête PQL suivante détermine si le nom de la personne ne commence pas par « Joe » en respectant la casse.

```sql
person.name.doesNotStartWith("Joe")
```

## Ends with

La fonction `endsWith` permet de déterminer si une chaîne se termine par une sous-chaîne donnée.

**Format**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Un paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur vraie. |

**Exemple**

La requête PQL suivante détermine si l’adresse électronique de la personne se termine par « .com » en respectant la casse.

```sql
person.emailAddress.endsWith(".com")
```

## Does not end with

La fonction `doesNotEndWith` permet de déterminer si une chaîne ne se termine pas par une sous-chaîne donnée.

**Format**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Un paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur vraie. |

**Exemple**

La requête PQL suivante détermine si l’adresse électronique de la personne ne se termine pas par « .com » en respectant la casse.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

La fonction `contains` permet de déterminer si une chaîne contient une sous-chaîne donnée.

**Format**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Un paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur vraie. |

**Exemple**

La requête PQL suivante détermine si l’adresse électronique de la personne contient la chaîne « 2010@gm » en respectant la casse.

```sql
person.emailAddress.contains("2010@gm")
```

## Does not contain

La fonction `doesNotContain` permet de déterminer si une chaîne ne contient pas une sous-chaîne donnée.

**Format**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Un paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur vraie. |

**Exemple**

La requête PQL suivante détermine si l’adresse électronique de la personne ne contient pas la chaîne « 2010@gm » en respectant la casse.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Equals

La fonction `equals` permet de déterminer si une chaîne est égale à une sous-chaîne donnée.

**Format**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à comparer à la première chaîne. |

**Exemple**

La requête PQL suivante détermine si le nom de la personne est « John » en respectant la casse.

```sql
person.name.equals("John")
```

## Not equal to

La fonction `notEqualTo` permet de déterminer si une chaîne est différente d’une chaîne donnée.

**Format**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | La chaîne à comparer à la première chaîne. |

**Exemple**

La requête PQL suivante détermine si le nom de la personne n’est pas « John » en respectant la casse.

```sql
person.name.notEqualTo("John")
```

## Matches

La fonction `matches` permet de déterminer si une chaîne correspond à une expression régulière donnée. Reportez-vous à [ce document](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) pour plus d’informations concernant les modèles correspondants dans les expressions régulières.

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Exemple**

La requête PQL suivante détermine si le nom de la personne commence par « John » sans tenir compte de la casse.

```sql
person.name.matches("(?i)^John")
```

## Regular expression group

La fonction `regexGroup` est utilisée pour extraire des informations spécifiques en fonction de l’expression régulière fournie.

**Format**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Exemple**

La requête PQL suivante est utilisée pour extraire le nom de domaine d’une adresse électronique.

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de chaîne, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).

