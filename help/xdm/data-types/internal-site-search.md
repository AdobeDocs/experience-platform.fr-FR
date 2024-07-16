---
title: Type de données de recherche de site interne
description: Découvrez le type de données XDM de recherche de site interne.
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Type de données [!UICONTROL Recherche de site interne]

[!UICONTROL Recherche de site interne] est un type de données XDM standard qui décrit une recherche de site interne, y compris tous les comportements et détails de recherche associés.

![](../images/data-types/internal-site-search.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Booléen] | Indique si un visiteur a utilisé une valeur de recherche suggérée ou saisie semi-automatique pour exécuter la recherche. |
| `autoCompleteTypedValue` | [!UICONTROL Chaîne] | Dans le cas de scénarios de saisie semi-automatique, les utilisateurs abandonnent parfois leur recherche et sélectionnent un terme spécifique dans la liste déroulante. Cette valeur effectue le suivi de ce que l’utilisateur a commencé à saisir afin de générer l’ensemble spécifique de termes de recherche suggérés. |
| `autoCompleteValue` | [!UICONTROL Chaîne] | Pour les scénarios de saisie semi-automatique, les utilisateurs abandonnent parfois leur recherche et sélectionnent un terme spécifique dans le menu déroulant. Cette valeur est utilisée pour effectuer le suivi des termes spécifiques sélectionnés. |
| `instances` | [!UICONTROL Entier] | Nombre de fois où la recherche interne sur le site a eu lieu. |
| `locationInPage` | [!UICONTROL Chaîne] | S’il existe plusieurs zones de recherche sur la page, cette valeur doit être utilisée pour identifier l’emplacement spécifique sur lequel l’utilisateur a effectué la recherche. |
| `nullInstances` | [!UICONTROL Entier] | Nombre de fois où la recherche interne sur le site a eu lieu et n’a fourni aucun résultat. |
| `numberOfResults` | [!UICONTROL Entier] | Nombre total de résultats de recherche renvoyés. |
| `postalCode` | [!UICONTROL Chaîne] | Le code postal utilisé pour la recherche, le cas échéant. |
| `productFindingMethods` | [!UICONTROL Chaîne] | Valeur du terme de recherche interne sur le site avec liaison de marchandisage. Cette valeur indique le terme recherché immédiatement avant l’affichage d’un produit. |
| `radiusDistance` | [!UICONTROL Entier] | Associé à `radiusType`, indique la distance sélectionnée du rayon de recherche. |
| `radiusType` | [!UICONTROL Entier] | Type de distance sélectionné `radiusDistance`, soit des kilomètres, soit des kilomètres. |
| `refinementInstances` | [!UICONTROL Entier] | Nombre de fois où la recherche interne sur le site a été affinée. |
| `refinementType` | Tableau de chaînes | Répertorie les types d’amélioration appliqués aux résultats de la recherche. Par exemple, département, marque, prix, en magasin, évaluation des révisions, couleur, matériau, etc. |
| `refinementValue` | [!UICONTROL Chaîne] | Valeur à laquelle la recherche a été affinée. |
| `resultsPageNumber` | [!UICONTROL Entier] | Pour les résultats de recherche paginés, cette valeur effectue le suivi de la page des résultats que le visiteur consulte. |
| `resultsPerPage` | [!UICONTROL Entier] | Pour les résultats de recherche paginés, cette valeur effectue le suivi du nombre de résultats de recherche affichés par page. |
| `searchType` | [!UICONTROL Chaîne] | Capture la méthode de recherche en cours d’exécution, le cas échéant. Par exemple, une recherche par type anticipé, une recherche saisie directement ou tout autre type de fonctionnalité de recherche personnalisée d’un site. |
| `sortOrder` | [!UICONTROL Chaîne] | Combiné avec `sortType`, indique l’ordre de tri des résultats de recherche, ascendant ou descendant. |
| `term` | [!UICONTROL Chaîne] | Terme de recherche interne du site saisi par le visiteur. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
