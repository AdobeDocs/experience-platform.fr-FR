---
solution: Experience Platform
title: Types de données pris en charge dans Segmentation Service
description: Tous les types de données des modèles de données d’expérience (XDM) sont pris en charge dans Adobe Segmentation Service. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivantes.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 52%

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

## Événements Experience

En tant que schéma Adobe Experience Platform, [!DNL XDM ExperienceEvents] enregistrer les interactions client explicites et implicites avec les applications intégrées à Experience Platform, y compris un instantané du système au moment où l’interaction a eu lieu. [!DNL ExperienceEvents] sont des enregistrements de faits. Ainsi, il s’agit d’une source de données disponible lors de la définition de segment.

Comme le montre le tableau ci-dessous, les données d’événement sont générées à l’aide de mots-clés qui aident à affiner le comportement des événements et à spécifier des attributs d’événement.

| Mot-clé | Utilisation |
| ------- | --- |
| Inclure/exclure | Décrit le comportement de l’événement via l’inclusion ou l’exclusion des données. |
| N’importe lequel/Tout | Permet de déterminer le nombre de définitions de segment admissibles. |
| Bouton d’activation/désactivation « Appliquer la règle de temps » | Incorpore des données de date. |
| Est égal à, n’est pas égal à, commence par, ne commence pas par, se termine par, ne se termine pas par, contient, ne contient pas, existe, n’existe pas | Incorpore des données de chaîne. |

### Partage d&#39;audiences

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
