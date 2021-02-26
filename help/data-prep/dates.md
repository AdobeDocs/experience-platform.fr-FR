---
keywords: Experience Platform ; accueil ; rubriques populaires ; mapper csv ; mapper le fichier csv ; mapper le fichier csv à xdm ; mapper csv à xdm ; ui guide ; mapper ; mapper ; date ; fonctions de date ; dates ; fonction de date ; date
solution: Experience Platform
title: Fonctions de date d’aperçu des données
topic: aperçu
description: Ce document introduit la fonction de date utilisée avec l’aperçu des données.
translation-type: tm+mt
source-git-commit: d3531248f8a7116b66f9a7ca00e0eadbc3d9df3d
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 15%

---


# Date, fonction

Data Prep prend en charge les fonctions de date, à la fois sous forme de chaînes et d’objets datetime.

## Format de la fonction Date

La fonction de date convertit les chaînes et les objets datetime en objet ZonedDateTime au format ISO 8601.

**Format**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Paramètre | Description |
| --------- | ----------- |
| `{DATE}` | Obligatoire. Chaîne représentant la date. |
| `{FORMAT}` | Facultatif. Chaîne représentant le format de la date. Pour plus d&#39;informations sur le formatage des chaînes, consultez la section [Chaîne de format de date/heure](#format). |
| `{DEFAULT_DATE}` | Facultatif. Date par défaut à renvoyer si la date fournie est nulle. |

Par exemple, l’expression `date(orderDate, "yyyy-MM-dd")` convertit une valeur `orderDate` de &quot;31 décembre 2020&quot; en une valeur datetime de &quot;2020-12-31&quot;.

## Conversions de la fonction de date

Lorsque les champs de chaîne des données entrantes sont mappés aux champs de date dans les schémas à l’aide du modèle de données d’expérience (XDM), le format de date doit être mentionné explicitement. Si elle n’est pas explicitement mentionnée, l’API tente de convertir les données d’entrée en les faisant correspondre aux formats suivants. Une fois qu’un format correspondant est trouvé, il arrête d’évaluer les formats suivants.

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
> L’outil d’aperçu des données tentera de convertir les chaînes en dates de la meilleure façon possible. Cependant, ces conversions peuvent entraîner des résultats indésirables. Par exemple, la valeur de chaîne &quot;12112020&quot; correspond au modèle &quot;Jour&quot;, mais l’utilisateur a peut-être prévu que la date soit lue avec le modèle &quot;jjMMaaaa&quot;. Par conséquent, les utilisateurs doivent mentionner explicitement le format de date pour les chaînes.

## Chaînes de format de date/heure {#format}

Le tableau suivant indique les lettres de modèle définies pour les chaînes de format. Veuillez noter que les lettres sont sensibles à la casse.

| Symbole | Signification | Présentation | Exemple |
| ------ | ------- | ------------ | ------- |
| G | L&#39;ère | Texte | AD; Anno Domini; A |
| Y | Année, basée sur la semaine ISO | Nombre | 1996 ; 96 |
| y | L&#39;année | Nombre | 2004 ; 04 |
| M/L | Mois de l&#39;année | Nombre/Texte | 7 ; 07 ; Jul ; juillet ; J |
| w | Semaine de l’année | Nombre | 27 |
| W | Semaine du mois | Nombre | 3 |
| D | Jour de l&#39;année | Nombre | 189 |
| d | Jour du mois | Nombre | 10 |
| F | Jour de la semaine dans un mois | Nombre | 2 |
| E | Nom du jour de la semaine | Texte | Mardi ; Tue |
| u | Jour de la semaine, en tant que nombre. 1 représente le lundi, ..., 7 représente le dimanche | Nombre | 1 |
| a | Marqueur AM/PM | Texte | PM |
| H | Heure dans la journée (0-23) | Nombre | 0 |
| k | Heure dans la journée (1-24) | Nombre | 24 |
| K | Heure en AM/PM (0-11) | Nombre | 0 |
| h | Heure en AM/PM (1-12) | Nombre | 12 |
| m | Minute dans l&#39;heure | Nombre | 38 |
| s | Seconde dans la minute | Nombre | 44 |
| S | Milliseconde | Nombre | 245 |
| z | Fuseau horaire | Fuseau horaire général | Pacifique (heure normale du Pacifique); PST ; GMT-08:00 |
| Z | Fuseau horaire | Fuseau horaire RFC 822 | -0800 |
| X | Fuseau horaire | Fuseau horaire ISO 8601 | -08; -0800; -08:00 |
| V | ID fuseau horaire | Texte | Amérique/Los_Angeles |
| O | Décalage du fuseau horaire | Texte | GMT+8 |
| Q/q | Trimestre de l&#39;année | Nombre/Texte | 3 ; 03 ; 3e trimestre ; 3e trimestre |
