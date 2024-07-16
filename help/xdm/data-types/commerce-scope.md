---
title: Type de données d’étendue Commerce
description: Découvrez le type de données XDM (Commerce Scope Experience Data Model).
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# Type de données [!UICONTROL Commerce Scope]

[!UICONTROL Portée de Commerce] est un type de données XDM (Experience Data Model) standard qui définit les identifiants pour lesquels un événement s’est produit dans un écosystème de commerce. Il distingue les environnements, les sites web, les magasins et les vues de magasin.

![Schéma du type de données Portée Commerce.](../images/data-types/commerce-scope.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID d’environnement] | `environmentID` | Chaîne | Identifiant de l’environnement. Un ID alphanumérique de 32 chiffres. |
| [!UICONTROL Code de site Web] | `websiteCode` | Chaîne | Code de site web unique au sein d’un environnement. |
| [!UICONTROL Code magasin] | `storeCode` | Chaîne | Le code de magasin unique au sein d’un site web. |
| [!UICONTROL Code de vue de magasin] | `storeViewCode` | Chaîne | Code d’affichage de magasin unique dans un magasin. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
