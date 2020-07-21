---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Types de données Adobe Experience Platform Segmentation Service
topic: overview
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 82%

---


# Types de données [!DNL Segmentation Service] pris en charge par l&#39;Adobe Experience Platform

All XDM data types are supported within [!DNL Segmentation Service]. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivantes.

## Données de chaîne

Les définitions de segment utilisent des données de chaîne pour définir des contraintes non numériques pour les audiences de segment, telles que « nom du pays » ou « niveau du programme de fidélité ».

Les données de chaîne sont incluses dans les définitions de segment à l’aide d’instructions logiques, inclusives/exclusives et comparatives. Une fois qu’un attribut de chaîne est ajouté à votre définition de segment, vous pouvez utiliser des instructions appropriées à la chaîne pour l’évaluer par rapport à d’autres champs de chaîne.

| Type d’instructions | Exemples |
| -------------- | -------- |
| Logique | `and`, `or`, `not` |
| inclusif/exclusif | `include`, `must` `exist`, `exclude`, `must not exist` |
| Comparaison | `equals`, `does not equal`, `contains`, `starts with` |

## Données de date

Les données de date vous permettent d’attribuer un contexte temporel à vos définitions de segment, soit en utilisant des dates de début/fin spécifiques, soit en utilisant des instructions en fonction de la date, comme le montre le tableau ci-dessous. Une implémentation peut être la création d’une audience de clients qui ont interagi avec votre marque à un moment *cette année* et qui ont également été actifs *au cours des derniers jours*.

| Exemple de champ | Instructions en fonction de la date | Chronologie |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | En fonction du jour où le segment a été créé. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | En fonction d’une semaine ou d’un mois donné. |

## Événements Experience

As an Adobe Experience Platform schema, [!DNL XDM ExperienceEvents] record explicit and implicit customer interactions with [!DNL Platform]-integrated applications, including a snapshot of the system at the time the interaction took place. [!DNL ExperienceEvents] sont des dossiers de faits. Ainsi, il s’agit d’une source de données disponible lors de la définition de segment.

Comme le montre le tableau ci-dessous, les données d’événement sont générées à l’aide de mots-clés qui aident à affiner le comportement des événements et à spécifier des attributs d’événement.

| Mot-clé | Utilisation |
| ------- | --- |
| Inclure/exclure | Décrit le comportement de l’événement via l’inclusion ou l’exclusion des données. |
| N’importe lequel/Tout | Permet de déterminer le nombre de segments qualifiants. |
| Bouton d’activation/désactivation « Appliquer la règle de temps » | Incorpore des données de date. |
| Est égal à, n’est pas égal à, commence par, ne commence pas par, se termine par, ne se termine pas par, contient, ne contient pas, existe, n’existe pas | Incorpore des données de chaîne. |

## Segments

Les définitions de segment existantes peuvent également être utilisées en tant que composants d’une nouvelle définition de segment, en ajoutant leurs attributs et règles basées sur des événements au nouveau segment.

## Audiences

Les audiences externes peuvent également être utilisées comme composants d’une nouvelle définition de segment, en ajoutant leurs règles d’attribut au nouveau segment.

Actuellement, seul Adobe Audience Manager est pris en charge en tant qu’audience. D’autres sources seront activées à l’avenir.

## Autres types de données

Outre les types de données mentionnés ci-dessus, la liste des types de données pris en charge inclut également :

- URI (Uniform Resource Identifier)
- Enum
- Nombre
- Long
- Entier
- Court
- Octet
- Booléen
- Tableau
- Objet
- Map