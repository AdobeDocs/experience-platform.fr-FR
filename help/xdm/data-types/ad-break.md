---
title: Type de données de coupure publicitaire
description: Découvrez le type de données Modèle de données d’expérience (XDM) de coupure publicitaire .
exl-id: dfe0c386-8459-440d-95b5-b2139fac0fc3
TQID: https://experienceleague.adobe.com/ezXIQ1w0eEFef2OZgMEzzhZNAkT51yIGzNFdvA6mfUU
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 5%

---

# Type de données [!UICONTROL Ad break]

[!UICONTROL Ad break] est un type de données standard du modèle de données d’expérience (XDM) qui décrit comment une annonce publicitaire horodatée est insérée dans un média horodaté.

![Structure du type de données](../images/data-types/ad-break.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_dc.title` | Chaîne | Nom convivial de la coupure publicitaire. |
| `_id` | Chaîne | Identifiant unique de la coupure publicitaire. |
| `offset` | Entier | Décalage, en secondes, de la coupure publicitaire par rapport au début du contenu principal. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/advertising-break.schema.json)
