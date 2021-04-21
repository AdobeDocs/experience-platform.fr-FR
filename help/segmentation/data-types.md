---
keywords: Experience Platform ; accueil ; rubriques populaires ; type de données ; types de données ; types de données ; type de données ; type de données ; type de données de segmentation ; segmentation ; segmentation ; service de segmentation ; types de données du service de segmentation ;
solution: Experience Platform
title: Types de données pris en charge dans le service de segmentation
topic-legacy: overview
description: Tous les types de données de modèle de données d’expérience (XDM) sont pris en charge dans Adobe Segmentation Service. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivantes.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 61%

---

# Types de données pris en charge dans le service de segmentation

Tous les types de données de modèle de données d’expérience (XDM) sont pris en charge dans Adobe Experience Platform Segmentation Service. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivantes.

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
| person.firstPurchase | `today`,  `yesterday`,  `this month`,  `this year` | En fonction du jour où le segment a été créé. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | En fonction d’une semaine ou d’un mois donné. |

## Événements Experience

En tant que schéma Adobe Experience Platform, [!DNL XDM ExperienceEvents] enregistre les interactions client explicites et implicites avec les applications intégrées [!DNL Platform], y compris un instantané du système au moment de l&#39;interaction. [!DNL ExperienceEvents] sont des dossiers de faits. Ainsi, il s’agit d’une source de données disponible lors de la définition de segment.

Comme le montre le tableau ci-dessous, les données d’événement sont générées à l’aide de mots-clés qui aident à affiner le comportement des événements et à spécifier des attributs d’événement.

| Mot-clé | Utilisation |
| ------- | --- |
| Inclure/exclure | Décrit le comportement de l’événement via l’inclusion ou l’exclusion des données. |
| N’importe lequel/Tout | Permet de déterminer le nombre de segments qualifiants. |
| Bouton d’activation/désactivation « Appliquer la règle de temps » | Incorpore des données de date. |
| Est égal à, n’est pas égal à, commence par, ne commence pas par, se termine par, ne se termine pas par, contient, ne contient pas, existe, n’existe pas | Incorpore des données de chaîne. |

### Partage d&#39;audiences

Les audiences externes peuvent également être utilisées comme composants d’une nouvelle définition de segment, en ajoutant leurs règles d’attribut au nouveau segment.

Actuellement, seule Adobe Audience Manager est prise en charge en tant qu’audience externe, les sources supplémentaires étant activées à l’avenir. Pour plus d&#39;informations sur l&#39;utilisation des audiences Adobe Audience Manager avec la plate-forme, consultez le [guide de partage d&#39;audiences dans la documentation Adobe Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Partage de segments

Les segments créés dans Platform peuvent être utilisés dans d’autres [services principaux de Adobe Experience Cloud](https://docs.adobe.com/content/help/fr-FR/core-services/interface/experience-cloud.html). Pour activer cette fonctionnalité, vous devez contacter votre architecte de solution ou votre consultant.

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
