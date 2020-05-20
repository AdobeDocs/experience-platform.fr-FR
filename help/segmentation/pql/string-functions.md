---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions de chaîne
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 8%

---


# Fonctions de chaîne

Les offres PQL (Profil Requête Language) simplifient l’interaction avec les chaînes. Pour plus d&#39;informations sur les autres fonctions PQL, consultez la présentation [du langage](./overview.md)Profil Requête.

## J’aime

La `like` fonction est utilisée pour déterminer si une chaîne correspond à un modèle spécifié.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | expression à comparer à la première chaîne. Deux caractères spéciaux sont pris en charge pour créer une expression : `%` et `_`. <ul><li>`%` est utilisée pour représenter zéro ou plusieurs caractères.</li><li>`_` est utilisé pour représenter exactement un caractère.</li></ul> |

**Exemple**

La requête PQL suivante récupère toutes les villes contenant le modèle &quot;es&quot;.

```sql
city like "%es%"
```

## Commence par

La `startsWith` fonction est utilisée pour déterminer si une chaîne est début avec une sous-chaîne spécifiée.

**Format**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur true. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si le nom de la personne est début avec &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Ne commence pas par

La `doesNotStartWith` fonction est utilisée pour déterminer si une chaîne ne se début pas avec une sous-chaîne spécifiée.

**Format**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur true. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si le nom de la personne ne correspond pas à &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Se termine par

La `endsWith` fonction est utilisée pour déterminer si une chaîne se termine par une sous-chaîne spécifiée.

**Format**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur true. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si l’adresse électronique de la personne se termine par &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Ne se termine pas par

La `doesNotEndWith` fonction permet de déterminer si une chaîne ne se termine pas par une sous-chaîne spécifiée.

**Format**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur true. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si l’adresse électronique de la personne ne se termine pas par &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains (Contient)

La `contains` fonction est utilisée pour déterminer si une chaîne contient une sous-chaîne spécifiée.

**Format**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur true. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si l’adresse électronique de la personne contient la chaîne &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## Ne contient pas

La `doesNotContain` fonction permet de déterminer si une chaîne ne contient pas de sous-chaîne spécifiée.

**Format**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à rechercher dans la première chaîne. |
| `{BOOLEAN}` | Paramètre facultatif permettant de déterminer si la vérification est sensible à la casse. Par défaut, cette valeur est définie sur true. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si l’adresse électronique de la personne ne contient pas la chaîne &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Est égal

La `equals` fonction est utilisée pour déterminer si une chaîne est égale à la chaîne spécifiée.

**Format**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à comparer à la première chaîne. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si le nom de la personne est &quot;John&quot;.

```sql
person.name.equals("John")
```

## Différent de

La `notEqualTo` fonction permet de déterminer si une chaîne n’est pas égale à la chaîne spécifiée.

**Format**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | Chaîne sur laquelle effectuer la vérification. |
| `{STRING_2}` | Chaîne à comparer à la première chaîne. |

**Exemple**

La requête PQL suivante détermine, avec respect de la casse, si le nom de la personne n’est pas &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Correspond à

La `matches` fonction permet de déterminer si une chaîne correspond à une expression régulière spécifique. Veuillez consulter [ce document](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) pour plus d&#39;informations sur les modèles correspondants dans les expressions régulières.

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Exemple**

La requête PQL suivante détermine, sans tenir compte de la casse, si le nom de la personne début avec &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

## Groupe d&#39;expressions régulières

La `regexGroup` fonction est utilisée pour extraire des informations spécifiques, sur la base de l&#39;expression régulière fournie.

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

Maintenant que vous avez pris connaissance des fonctions de chaîne, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d&#39;informations sur d&#39;autres fonctions PQL, veuillez lire la présentation [de la langue de la Requête de](./overview.md)Profil.

