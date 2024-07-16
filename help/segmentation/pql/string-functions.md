---
solution: Experience Platform
title: Fonctions de chaîne PQL
description: Profile Query Language (PQL) offre des fonctions pour faciliter l’interaction avec les chaînes.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 88%

---

# Fonctions de chaîne

[!DNL Profile Query Language] (PQL) offre des fonctions pour faciliter l’interaction avec les chaînes. Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Comme

La fonction `like` permet de déterminer si une chaîne correspond à un modèle donné.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Description |
| --------- | ----------- |
| `{STRING_1}` | La chaîne à vérifier. |
| `{STRING_2}` | L&#39;expression à laquelle comparer la première chaîne. Les deux caractères spéciaux pris en charge pour créer une expression sont `%` et `_`. <ul><li>`%` est utilisé pour représenter aucun ou plusieurs caractères.</li><li>`_` est utilisé pour représenter exactement un caractère.</li></ul> |

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

La requête PQL suivante détermine si l’adresse e-mail de la personne se termine par « .com » en respectant la casse.

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

La requête PQL suivante détermine si l’adresse e-mail de la personne ne se termine pas par « .com » en respectant la casse.

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

La requête PQL suivante détermine si l’adresse e-mail de la personne contient la chaîne « 2010@gm » en respectant la casse.

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

La requête PQL suivante détermine si l’adresse e-mail de la personne ne contient pas la chaîne « 2010@gm » en respectant la casse.

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

La fonction `notEqualTo` permet de déterminer si une chaîne est différente d&#39;une chaîne donnée.

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

La fonction `matches` permet de déterminer si une chaîne correspond à une expression régulière donnée. Reportez-vous à [ce document](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) pour plus d&#39;informations concernant les modèles correspondants dans les expressions régulières.

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Exemple**

La requête PQL suivante détermine si le nom de la personne commence par « John » sans tenir compte de la casse.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Si vous utilisez des fonctions d’expression régulière telles que `\w`, vous **devez** pour échapper la barre oblique inverse. Ainsi, au lieu d&#39;écrire uniquement `\w`, vous devez inclure une barre oblique inverse supplémentaire et écrire `\\w`.

## Groupe d’expressions régulières

La fonction `regexGroup` est utilisée pour extraire des informations spécifiques en fonction de l&#39;expression régulière fournie.

**Format**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Exemple**

La requête PQL suivante est utilisée pour extraire le nom de domaine d’une adresse e-mail.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Si vous utilisez des fonctions d’expression régulière telles que `\w`, vous **devez** pour échapper la barre oblique inverse. Ainsi, au lieu d&#39;écrire uniquement `\w`, vous devez inclure une barre oblique inverse supplémentaire et écrire `\\w`.

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de chaîne, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
