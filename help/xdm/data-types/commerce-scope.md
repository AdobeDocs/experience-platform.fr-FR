---
title: Type de données d’étendue de commerce
description: Découvrez le type de données XDM (Commerce Scope Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# [!UICONTROL Portée du commerce] type de données

[!UICONTROL Portée du commerce] est un type de données XDM (Experience Data Model) standard qui définit les identifiants pour lesquels un événement s’est produit dans un écosystème de commerce. Il distingue les environnements, les sites web, les magasins et les vues de magasin.

![Schéma du type de données Portée de commerce.](../images/data-types/commerce-scope.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Identifiant d’environnement] | `environmentID` | chaîne | Identifiant de l’environnement. Un ID alphanumérique de 32 chiffres. |
| [!UICONTROL Code du site web] | `websiteCode` | chaîne | Code de site web unique au sein d’un environnement. |
| [!UICONTROL Code de magasin] | `storeCode` | chaîne | Le code de magasin unique au sein d’un site web. |
| [!UICONTROL Code d’affichage du magasin] | `storeViewCode` | chaîne | Code d’affichage de magasin unique dans un magasin. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
