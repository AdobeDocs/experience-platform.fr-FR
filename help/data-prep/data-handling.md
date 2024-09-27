---
keywords: Experience Platform;accueil;rubriques populaires;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de lʼui;mappeur;mappage;data prep;préparation des données;préparer des données;
solution: Experience Platform
title: Gestion des formats de données avec la préparation des données
description: Ce document donne un aperçu de la manière dont différents types de données sont traités dans la préparation des données.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: a49140853124f4f7beee87a739c8e670838947f4
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 95%

---

# Gestion des formats de données avec la préparation des données

La préparation des données peut gérer de manière robuste différents formats de données ingérés dans Adobe Experience Platform. Ce document décrit comment différents formats de données sont traités avec la préparation de données.

## Booléens {#booleans}

Si le type source est une chaîne et que le type cible est une valeur booléenne, la préparation de données peut automatiquement analyser la valeur et convertir la valeur source en valeur booléenne.

Les valeurs `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true` et `TRUE` sont automatiquement analysées pour être `true`.

Les valeurs `n`, `N`, `no`, `NO`, `off`, `OFF`, `false` et `FALSE` sont automatiquement analysées pour être `false`.

## Dates {#dates}

La préparation de données prend en charge les fonctions de date, à la fois sous forme de chaînes et d’objets datetime.

### Format de la fonction Date

La fonction de date convertit les chaînes et les objets datetime en objet ZonedDateTime au format ISO 8601.

**Format**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATE}` | Obligatoire. Chaîne représentant la date. |
| `{FORMAT}` | Facultatif. Chaîne représentant le format de la date source. Vous trouverez plus d’informations sur le formatage des chaînes dans la [section Chaîne de format date/heure](#format). |
| `{DEFAULT_DATE}` | Facultatif. Date par défaut à renvoyer si la date fournie est nulle. |

Par exemple, l’expression `date(orderDate, "yyyy-MM-dd")` convertira une valeur `orderDate` de « 31 décembre 2020 » en une valeur datetime de « 2020-12-31 ».

### Conversions des fonctions de date

Lorsque les champs de chaîne des données entrantes sont mappés aux champs de date dans les schémas à l’aide du modèle de données d’expérience (XDM), le format de date doit être mentionné explicitement. Si celui-ci n’est pas mentionné explicitement, la préparation de données tente de convertir les données d’entrée en les faisant correspondre aux formats suivants. Une fois qu’un format correspondant est trouvé, il arrête l’évaluation des formats suivants.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> La préparation de données tentera de convertir les chaînes en dates autant que possible. Cependant, ces conversions peuvent entraîner des résultats indésirables. Par exemple, la valeur de chaîne « 12112020 » correspond au modèle « MMjjaaaa », mais l’utilisateur peut avoir prévu que la date soit lue avec le modèle « jjMMaaaa ». Par conséquent, les utilisateurs doivent mentionner explicitement le format de date pour les chaînes.

### Chaînes de format de date/heure {#format}

>[!TIP]
>
>Actuellement, la fonction de date dans l’ingestion par lots supprime les millisecondes si les valeurs de date sont dans ce format : `2024-05-05 20:39:00.005` PST. Pour conserver les millisecondes, utilisez ce format : `2024-05-05 20:39:00.005-0800`

Le tableau suivant indique les lettres de modèle définies pour les chaînes de format. Veuillez noter que les lettres sont sensibles à la casse.

| Symbole | Signification | Présentation | Exemple |
| ------ | ------- | ------------ | ------- |
| G | L’ère | Texte | AD; Anno Domini; A |
| Y | Année, selon la semaine ISO | Nombre | 1996; 96 |
| y | L’année | Nombre | 2004; 04 |
| M/L | Mois de l’année | Nombre/Texte | 7; 07; Juil; Juillet; J |
| w | Semaine de l’année | Nombre | 27 |
| W | Semaine du mois | Nombre | 3 |
| D | Jour de l’année | Nombre | 189 |
| d | Jour du mois | Nombre | 10 |
| F | Jour de la semaine dans un mois | Nombre | 2 |
| E | Nom du jour de la semaine | Texte | Mardi; Mard |
| u | Jour de la semaine, sous la forme d’un nombre. 1 représente le lundi, ..., 7 représente le dimanche | Nombre | 1 |
| a | Marqueur matin/après-midi | Texte | PM |
| H | Heure dans la journée (0-23) | Nombre | 0 |
| k | Heure dans la journée (1-24) | Nombre | 24 |
| K | Heure en AM/PM (0-11) | Nombre | 0 |
| h | Heure en AM/PM (1-12) | Nombre | 12 |
| m | Minute dans l’heure | Nombre | 38 |
| s | Seconde dans la minute | Nombre | 44 |
| S | Milliseconde | Nombre | 245 |
| z | Fuseau horaire | Fuseau horaire général | Pacifique (heure normale du Pacifique); PST; GMT-08:00 |
| Z | Fuseau horaire | Fuseau horaire RFC 822 | -0800 |
| X | Fuseau horaire | Fuseau horaire ISO 8601 | -08; -0800; -08:00 |
| V | Identifiant de fuseau horaire | Texte | Amérique/Los_Angeles |
| O | Décalage du fuseau horaire | Texte | GMT+8 |
| Q/q | Trimestre de l’année | Nombre/Texte | 3; 03; T3; 3e trimestre |

## Mappages {#maps}

Les cartes ne sont actuellement pas prises en charge dans [!DNL Data Prep].
