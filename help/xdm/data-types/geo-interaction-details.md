---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;balise;détails de l’interaction;type de données;type de données;type de données;
solution: Experience Platform
title: Type De Données Des Détails De L’Interaction Géographique
description: Découvrez le type de données XDM des détails de l’interaction géographique.
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
TQID: https://experienceleague.adobe.com/eZFOzS1giUeQzb-33mLYEVIwd-9qmDsDdvwiZ3AgGSQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 158
ht-degree: 3%

---

# [!UICONTROL Détails de l’interaction géographique] type de données

[!UICONTROL Détails de l’interaction géographique] est un type de données XDM standard qui décrit l’état actuel d’inclusion dans une zone définie géographiquement.

![](../images/data-types/geo-interaction-details.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL Forme géographique]](./geo-shape.md) | Décrit la forme géographique de la zone avec laquelle il y a interaction. Ce champ peut décrire une boîte, un cercle ou un polygone. |
| `deviceGeoAccuracy` | Double | Précision du mécanisme ou du dispositif de mesure géographique, exprimée en mètres. |
| `distanceToCenter` | Double | Distance par rapport au centre de la zone dans le cas d’un cercle géographique, mesurée en mètres. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
