---
solution: Experience Platform
title: Fonctions de chaîne PQL
description: Profile Query Language (PQL) offre des fonctions permettant de simplifier l’interaction avec les chaînes.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
TQID: https://experienceleague.adobe.com/J4AulkVwMq7YKXs6L1A-seVd9PZXxbhMsd8FKQ5Mso4
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 859
ht-degree: 66%

---

# Fonctions de chaîne

[!DNL Profile Query Language] (PQL) offre des fonctions permettant de simplifier l’interaction avec les chaînes. Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Comme

La fonction `like` permet de déterminer si une chaîne correspond à un modèle donné sous la forme d’une valeur booléenne.

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

## Commence par

La fonction `startsWith` permet de déterminer si une chaîne commence par une sous-chaîne donnée sous la forme d’une valeur booléenne.

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

## Ne commence pas par

La fonction `doesNotStartWith` permet de déterminer si une chaîne ne commence pas par une sous-chaîne donnée sous la forme d’une valeur booléenne.

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

## Se termine par

La fonction `endsWith` permet de déterminer si une chaîne se termine par une sous-chaîne donnée sous la forme d’une valeur booléenne.

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

## Ne se termine pas par

La fonction `doesNotEndWith` permet de déterminer si une chaîne ne se termine pas par une sous-chaîne donnée sous la forme d’une valeur booléenne.

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

## Contient

La fonction `contains` permet de déterminer si une chaîne contient une sous-chaîne donnée sous la forme d’une valeur booléenne.

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

## Ne contient pas

La fonction `doesNotContain` permet de déterminer si une chaîne ne contient pas une sous-chaîne donnée en tant que valeur booléenne.

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

## Égal à

La fonction `equals` est utilisée pour déterminer si une chaîne est égale à la chaîne spécifiée sous la forme d’une valeur booléenne.

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

## Différent de

La fonction `notEqualTo` permet de déterminer si une chaîne est différente d&#39;une chaîne booléenne donnée.

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

## Correspond à

La fonction `matches` permet de déterminer si une chaîne correspond à une expression régulière donnée. Reportez-vous à [ce document](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) pour plus d’informations sur les modèles correspondants dans les expressions régulières en tant que valeur booléenne.

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
>Si vous utilisez des fonctions d’expression régulière telles que `\w`, vous **devez** échapper le caractère barre oblique inverse. Ainsi, au lieu d’écrire uniquement `\w`, vous devez inclure une barre oblique inverse supplémentaire et `\\w` écrire.

## Groupe d’expressions régulières

La fonction `regexGroup` est utilisée pour extraire des informations spécifiques en fonction de l&#39;expression régulière fournie sous la forme d&#39;une chaîne.

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
>Si vous utilisez des fonctions d’expression régulière telles que `\w`, vous **devez** échapper le caractère barre oblique inverse. Ainsi, au lieu d’écrire uniquement `\w`, vous devez inclure une barre oblique inverse supplémentaire et `\\w` écrire.

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de chaîne, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
