---
keywords: Experience Platform;accueil;rubriques populaires;type de données;types de données;types de données;type de données;types de données;types de données de segmentation;segmentation;segmentation;service de segmentation;types de données du service de segmentation ;
solution: Experience Platform
title: Types de données pris en charge dans Segmentation Service
description: Tous les types de données de modèle de données d’expérience (XDM) sont pris en charge dans Adobe Segmentation Service. Les règles qui constituent une définition de segment sont contextualisées par les types de données suivantes.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 62%

---

# Types de données pris en charge dans Segmentation Service

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
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | En fonction du jour où le segment a été créé. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | En fonction d’une semaine ou d’un mois donné. |

## Événements Experience

En tant que schéma Adobe Experience Platform, [!DNL XDM ExperienceEvents] enregistrer les interactions client explicites et implicites avec ; [!DNL Platform]les applications intégrées, y compris un instantané du système au moment de l’interaction. [!DNL ExperienceEvents] sont des enregistrements factuels. Ainsi, il s’agit d’une source de données disponible lors de la définition de segment.

Comme le montre le tableau ci-dessous, les données d’événement sont générées à l’aide de mots-clés qui aident à affiner le comportement des événements et à spécifier des attributs d’événement.

| Mot-clé | Utilisation |
| ------- | --- |
| Inclure/exclure | Décrit le comportement de l’événement via l’inclusion ou l’exclusion des données. |
| N’importe lequel/Tout | Permet de déterminer le nombre de segments qualifiants. |
| Bouton d’activation/désactivation « Appliquer la règle de temps » | Incorpore des données de date. |
| Est égal à, n’est pas égal à, commence par, ne commence pas par, se termine par, ne se termine pas par, contient, ne contient pas, existe, n’existe pas | Incorpore des données de chaîne. |

### Partage d&#39;audiences

Les audiences externes peuvent également être utilisées comme composants d’une nouvelle définition de segment, en ajoutant leurs règles d’attribut au nouveau segment.

Actuellement, seule Adobe Audience Manager est prise en charge en tant qu’audience externe, avec des sources supplémentaires activées à l’avenir. Pour plus d’informations sur l’utilisation des audiences Adobe Audience Manager avec Platform, reportez-vous à la section [guide de partage d’audience dans la documentation de Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=fr).

### Partage de segments

Les segments créés dans Platform peuvent être utilisés dans d’autres [Services principaux Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html?lang=fr). Pour activer cette fonctionnalité, vous devez contacter votre architecte de solution ou votre consultant.

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
