---
title: Type de données d’étendue Commerce
description: Découvrez le type de données du modèle de données d’expérience (XDM) de la portée Commerce.
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
TQID: https://experienceleague.adobe.com/PDBCsaYP6y57O9XzKCrAnDFG58lRZpR2qNkqNQ8p-0U
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 144
ht-degree: 6%

---

# Type de données [!UICONTROL Commerce Scope]

[!UICONTROL Portée de ] est un type de données standard du modèle de données d’expérience (XDM) qui définit les identifiants de l’endroit où un événement s’est produit dans un écosystème de commerce. Il distingue les environnements, les sites web, les boutiques et les affichages de boutique.

![Diagramme du type de données Commerce Scope.](../images/data-types/commerce-scope.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Identifiant d’environnement] | `environmentID` | chaîne | Identifiant d’environnement. Identifiant alphanumérique à 32 chiffres. |
| [!UICONTROL Code du site web] | `websiteCode` | chaîne | Code de site web unique dans un environnement. |
| [!UICONTROL Code de magasin] | `storeCode` | chaîne | Code de magasin unique au sein d’un site web. |
| [!UICONTROL Code d’affichage de la boutique] | `storeViewCode` | chaîne | Code d’affichage de magasin unique dans un magasin. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
