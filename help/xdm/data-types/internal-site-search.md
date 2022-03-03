---
title: Type de données de recherche de site interne
description: Ce document présente le type de données XDM de recherche de site interne.
source-git-commit: eaea904ddda6b7ffee6f52cd4af897c2a8885714
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 6%

---

# [!UICONTROL Recherche de site interne] type de données

[!UICONTROL Recherche de site interne] est un type de données XDM standard qui décrit une recherche de site interne, y compris tous les comportements et détails de recherche associés.

![](../images/data-types/internal-site-search.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Booléen] | Indique si un visiteur a utilisé une valeur de recherche suggérée ou saisie semi-automatique pour exécuter la recherche. |
| `autoCompleteTypedValue` | [!UICONTROL Chaîne] | Pour les scénarios de saisie semi-automatique, les utilisateurs abandonnent parfois leur recherche et sélectionnent un terme spécifique dans la liste déroulante. Cette valeur effectue le suivi de ce que l’utilisateur a commencé à saisir afin de générer l’ensemble spécifique de termes de recherche suggérés. |
| `autoCompleteValue` | [!UICONTROL Chaîne] | Pour les scénarios de saisie semi-automatique, les utilisateurs abandonnent parfois leur recherche et sélectionnent un terme spécifique dans le menu déroulant. Cette valeur est utilisée pour effectuer le suivi des termes spécifiques sélectionnés. |
| `instances` | [!UICONTROL Nombre entier] | Nombre de fois où la recherche interne sur le site a eu lieu. |
| `locationInPage` | [!UICONTROL Chaîne] | S’il existe plusieurs zones de recherche sur la page, cette valeur doit être utilisée pour identifier l’emplacement spécifique sur lequel l’utilisateur a effectué la recherche. |
| `nullInstances` | [!UICONTROL Nombre entier] | Nombre de fois où la recherche interne sur le site a eu lieu et n’a fourni aucun résultat. |
| `numberOfResults` | [!UICONTROL Nombre entier] | Nombre total de résultats de recherche renvoyés. |
| `postalCode` | [!UICONTROL Chaîne] | Le code postal utilisé pour la recherche, le cas échéant. |
| `productFindingMethods` | [!UICONTROL Chaîne] | Valeur du terme de recherche interne sur le site avec liaison de marchandisage. Cette valeur indique le terme recherché immédiatement avant l’affichage d’un produit. |
| `radiusDistance` | [!UICONTROL Nombre entier] | Combiné avec `radiusType`, indique la distance sélectionnée du rayon de recherche. |
| `radiusType` | [!UICONTROL Nombre entier] | Type de distance sélectionné de `radiusDistance`, soit des kilomètres. |
| `refinementInstances` | [!UICONTROL Nombre entier] | Nombre de fois où la recherche interne sur le site a été affinée. |
| `refinementType` | Tableau de chaînes | Répertorie les types d’amélioration appliqués aux résultats de la recherche. Par exemple, département, marque, prix, en magasin, évaluation des révisions, couleur, matériau, etc. |
| `refinementValue` | [!UICONTROL Chaîne] | Valeur à laquelle la recherche a été affinée. |
| `resultsPageNumber` | [!UICONTROL Nombre entier] | Pour les résultats de recherche paginés, cette valeur effectue le suivi de la page des résultats que le visiteur consulte. |
| `resultsPerPage` | [!UICONTROL Nombre entier] | Pour les résultats de recherche paginés, cette valeur effectue le suivi du nombre de résultats de recherche affichés par page. |
| `searchType` | [!UICONTROL Chaîne] | Capture la méthode de recherche en cours d’exécution, le cas échéant. Par exemple, une recherche par type anticipé, une recherche saisie directement ou tout autre type de fonctionnalité de recherche personnalisée d’un site. |
| `sortOrder` | [!UICONTROL Chaîne] | Combiné avec `sortType`, indique l’ordre de tri des résultats de la recherche, croissant ou décroissant. |
| `term` | [!UICONTROL Chaîne] | Terme de recherche interne du site saisi par le visiteur. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
