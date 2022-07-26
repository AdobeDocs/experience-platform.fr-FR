---
title: Type de données Détails de mise en oeuvre
description: Ce document fournit un aperçu du type de données du modèle de données d’expérience (XDM) relatif aux détails de mise en oeuvre.
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 18%

---

# [!UICONTROL Détails de mise en oeuvre] type de données

[!UICONTROL Détails de mise en oeuvre] est un type de données XDM (Experience Data Model) standard qui décrit une mise en oeuvre technologique, telle qu’une API ou un SDK.

![Structure du type de données](../images/data-types/implementation-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `environment` | Chaîne | Environnement de l’implémentation. |
| `name` | Chaîne | Identifiant du SDK ou du point de terminaison. Tous les SDK ou points de terminaison sont identifiés via un URI, y compris les extensions. |
| `version` | Chaîne | Version de l’API ou du SDK. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
