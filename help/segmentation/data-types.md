---
solution: Experience Platform
title: Types de données pris en charge dans Segmentation Service
description: Tous les types de données des modèles de données d’expérience (XDM) sont pris en charge dans Adobe Segmentation Service. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivantes.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
TQID: https://experienceleague.adobe.com/5LfyxR4YImiPa4XwBBGtIuo-VV2GzzsvNDoq-yOk8ac
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2: id: b784da9a-7978-4766-bf1f-5ab2b23d894aid: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 510
ht-degree: 54%

---

# Types de données pris en charge dans Segmentation Service

Tous les types de données des modèles de données d’expérience (XDM) sont pris en charge dans Adobe Experience Platform Segmentation Service. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivantes.

## Données de chaîne

Les définitions de segment utilisent des données de chaîne pour définir des contraintes non numériques pour les audiences, telles que « nom du pays » ou « niveau du programme de fidélité ».

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
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Pertinent pour le jour où la définition de segment a été créée. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | En fonction d’une semaine ou d’un mois donné. |

## Événements d’expérience

En tant que schéma Adobe Experience Platform, [!DNL XDM ExperienceEvents] enregistrer les interactions client explicites et implicites avec les applications intégrées à Experience Platform, y compris un instantané du système au moment où l’interaction a eu lieu. [!DNL ExperienceEvents] sont des enregistrements de faits. Ainsi, il s’agit d’une source de données disponible lors de la définition de segment.

Comme le montre le tableau ci-dessous, les données d’événement sont générées à l’aide de mots-clés qui aident à affiner le comportement des événements et à spécifier des attributs d’événement.

| Mot-clé | Utilisation |
| ------- | --- |
| Inclure/exclure | Décrit le comportement de l’événement via l’inclusion ou l’exclusion des données. |
| N’importe lequel/Tout | Permet de déterminer le nombre de définitions de segment admissibles. |
| Bouton d’activation/désactivation « Appliquer la règle de temps » | Incorpore des données de date. |
| Est égal à, n’est pas égal à, commence par, ne commence pas par, se termine par, ne se termine pas par, contient, ne contient pas, existe, n’existe pas | Incorpore des données de chaîne. |

### Partage d’audiences

Les audiences externes peuvent également être utilisées comme composants d’une nouvelle définition de segment, en ajoutant leurs règles d’attribut aux nouvelles définitions de segment.

Actuellement, seul Adobe Audience Manager est pris en charge en tant qu’audience externe, des sources supplémentaires étant activées à l’avenir. Vous trouverez plus d’informations sur l’utilisation des audiences Adobe Audience Manager avec Experience Platform dans le guide [partage d’audiences](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr) de la documentation de Adobe Audience Manager.

### Partage de la définition de segment

Les définitions de segment créées dans Experience Platform peuvent être utilisées dans d’autres [services principaux de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=fr). Pour activer cette fonctionnalité, vous devez contacter votre architecte de solution ou votre consultant.

## Autres types de données

Outre les types de données mentionnés ci-dessus, la liste des types de données pris en charge comprend également :

- Identifiant de ressource uniforme (URI)
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
