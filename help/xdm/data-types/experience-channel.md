---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;champs;schémas;schémas;détails de page web;type de données;type de données;page web
solution: Experience Platform
title: Type de données du canal d’expérience
description: Découvrez le type de données Experience Channel Data Model (XDM).
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 24%

---

# Type de données [!UICONTROL Experience channel]

[!UICONTROL Experience channel] est un type de données XDM (Experience Data Model) standard qui décrit un canal d’expérience. Un canal d’expérience représente une méthode ou un chemin d’accès pour la manière dont les expériences numériques sont utilisées.

Il existe plusieurs canaux d’expérience, chacun avec des contraintes différentes sur la manière dont le contenu est diffusé, sur la manière dont l’interaction client peut être observée et sur la manière dont les données sont collectées. Dans un canal, les expériences peuvent être diffusées à des emplacements spécifiques. Les emplacements et les types d’emplacements existant dans un canal diffèrent d’un canal à l’autre.

![](../images/data-types/experience-channel.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | Chaîne | Identifiant qui identifie de manière unique le canal. Chaque canal d’expérience spécifique définit une constante `@id`. |
| `_type` | Chaîne | Fournit un libellé de classification approximatif pour les canaux ayant des propriétés similaires. |
| `contentTypes` | Tableau de chaînes | Types de contenu que ce canal peut diffuser. |
| `locationTypes` | Tableau de chaînes | Types d’emplacements (emplacements virtuels) correspondant à ce canal et vers lesquels il peut diffuser du contenu. |
| `mediaAction` | Chaîne | Décrit une action multimédia d’événement d’expérience, le cas échéant. |
| `mediaType` | Chaîne | Décrit le type de média : exposition médiatique achetée, exposition médiatique détenue ou exposition médiatique gagnée. |
| `metricTypes` | Tableau de chaînes | Mesures pouvant être collectées dans ce canal. |
| `mode` | Chaîne | Façon dont les expériences sont diffusées dans ce canal. |
| `typeAtSource` | Chaîne | Nom personnalisé pour le canal. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
