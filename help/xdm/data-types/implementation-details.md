---
title: Type de données Détails de mise en oeuvre
description: Découvrez le type de données du modèle de données d’expérience (XDM) relatif aux détails de mise en oeuvre.
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 7%

---

# Type de données [!UICONTROL Détails de mise en oeuvre]

[!UICONTROL Détails de mise en oeuvre] est un type de données XDM (Experience Data Model) standard qui décrit une mise en oeuvre technologique, telle qu’une API ou un SDK.

![Structure de type de données](../images/data-types/implementation-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `environment` | Chaîne | Environnement de l’implémentation. |
| `name` | Chaîne | Identifiant du SDK ou du point de terminaison. Tous les SDK ou points de terminaison sont identifiés via un URI, y compris les extensions. |
| `version` | Chaîne | Version de l’API ou du SDK. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
