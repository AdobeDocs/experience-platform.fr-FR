---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;date;date functions;dates;
solution: Experience Platform
title: Fonctions de date
topic: overview
description: Ce document présente les fonctions de date utilisées avec l’aperçu des données.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 17%

---


# Fonctions de date

Data Prep prend en charge les fonctions de date, à la fois sous forme de chaînes et d’objets datetime.

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

## Chaînes de format de date/heure

Le tableau suivant indique les lettres de modèle définies pour les chaînes de format. Veuillez noter que les lettres sont sensibles à la casse.

| Symbole | Signification | Présentation | Exemple |
| ------ | ------- | ------------ | ------- |
| G | L&#39;ère | Texte | AD; Anno Domini; A |
| Y | Année, basée sur la semaine ISO | Nombre | 1996; 96 |
| y | L&#39;année | Nombre | 2004; 04 |
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
| Q/q | Trimestre de l&#39;année | Nombre/Texte | 3 ; 03 ; T3 ; 3e trimestre |

**Exemple**

L’expression `date(orderDate, 'yyyy-MM-dd')` convertit la date de commande, si sa valeur est &quot;31 décembre 2020&quot;, en une heure de date avec la valeur &quot;2020-12-31&quot;.