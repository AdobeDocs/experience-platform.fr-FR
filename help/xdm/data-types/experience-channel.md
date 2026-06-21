---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;Détails de la page web;type de données;type de données;page web
solution: Experience Platform
title: Type de données du canal d’expérience
description: Découvrez le type de données du modèle de données d’expérience (XDM) du canal d’expérience.
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
TQID: https://experienceleague.adobe.com/ztkh-QGjpud4jQ-6rTpePhUf5ITdyVcpc43qlTz855Q
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 266
ht-degree: 18%

---

# Type de données [!UICONTROL canal Experience]

[!UICONTROL Canal d’expérience] est un type de données standard du modèle de données d’expérience (XDM) qui décrit un canal d’expérience. Un canal d’expérience représente une méthode ou un chemin d’accès pour la manière dont les expériences numériques sont utilisées.

Il existe plusieurs canaux d’expérience, chacun ayant des contraintes différentes sur la manière dont le contenu est diffusé, dont l’interaction client peut être observée et dont les données sont collectées. Au sein d’un canal, les expériences peuvent être diffusées à des emplacements spécifiques. Les emplacements et les types d’emplacements qui existent dans un canal varient d’un canal à l’autre.

![](../images/data-types/experience-channel.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_id` | Chaîne | Identifiant qui identifie le canal de manière unique. Chaque canal d’expérience spécifique définit un `@id` constant. |
| `_type` | Chaîne | Fournit une étiquette de classification approximative pour les canaux avec des propriétés similaires. |
| `contentTypes` | Tableau de chaînes | Types de contenu que ce canal peut diffuser. |
| `locationTypes` | Tableau de chaînes | Types d’emplacements (emplacements virtuels) correspondant à ce canal et vers lesquels il peut diffuser du contenu. |
| `mediaAction` | Chaîne | Décrit une action de média d’événement d’expérience, le cas échéant. |
| `mediaType` | Chaîne | Décrit le type de média : exposition médiatique achetée, exposition médiatique détenue ou exposition médiatique gagnée. |
| `metricTypes` | Tableau de chaînes | Mesures pouvant être collectées dans ce canal. |
| `mode` | Chaîne | Façon dont les expériences sont diffusées dans ce canal. |
| `typeAtSource` | Chaîne | Nom personnalisé du canal. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
