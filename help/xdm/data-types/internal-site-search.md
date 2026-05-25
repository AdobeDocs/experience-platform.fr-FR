---
title: Type de données de recherche interne au site
description: Découvrez le type de données XDM de recherche interne au site.
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
TQID: https://experienceleague.adobe.com/aFl8c91iEEmyqaWll6cyeKwPf02OKx1FrH2URbgKT90
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 372
ht-degree: 1%

---

# Type de données [!UICONTROL Internal Site Search]

[!UICONTROL Internal Site Search] est un type de données XDM standard qui décrit une recherche interne sur le site, y compris tous les détails et comportements de recherche associés.

![](../images/data-types/internal-site-search.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL Boolean] | Indique si un visiteur a utilisé une valeur de recherche suggérée ou saisie automatiquement pour exécuter la recherche. |
| `autoCompleteTypedValue` | [!UICONTROL String] | Pour les scénarios de saisie semi-automatique, les utilisateurs abandonnent parfois leur recherche et sélectionnent un terme spécifique dans la liste déroulante. Cette valeur effectue le suivi de ce que l’utilisateur a commencé à saisir afin de générer l’ensemble spécifique de termes de recherche suggérés. |
| `autoCompleteValue` | [!UICONTROL String] | Pour les scénarios de saisie semi-automatique, les utilisateurs abandonnent parfois leur recherche et sélectionnent un terme spécifique dans le menu déroulant. Cette valeur est utilisée pour effectuer le suivi des termes spécifiques sélectionnés. |
| `instances` | [!UICONTROL Integer] | Nombre de fois où la recherche interne au site a été effectuée. |
| `locationInPage` | [!UICONTROL String] | Lorsqu’il existe plusieurs zones de recherche sur la page, cette valeur doit être utilisée pour identifier l’emplacement spécifique utilisé pour la recherche. |
| `nullInstances` | [!UICONTROL Integer] | Nombre de fois où la recherche interne sur site n’a donné aucun résultat. |
| `numberOfResults` | [!UICONTROL Integer] | Nombre total de résultats de recherche renvoyés. |
| `postalCode` | [!UICONTROL String] | Code postal de la recherche, le cas échéant. |
| `productFindingMethods` | [!UICONTROL String] | Valeur du terme de recherche interne sur site avec liaison de marchandisage. Cette valeur indique le terme qui a été recherché juste avant d’afficher un produit. |
| `radiusDistance` | [!UICONTROL Integer] | Combiné avec `radiusType`, indique la distance sélectionnée du rayon de recherche. |
| `radiusType` | [!UICONTROL Integer] | Type de distance sélectionné de `radiusDistance`, miles ou kilomètres. |
| `refinementInstances` | [!UICONTROL Integer] | Nombre de fois où la recherche interne sur site a été affinée. |
| `refinementType` | Tableau de chaînes | Répertorie les types d’affinement appliqués aux résultats de la recherche. Par exemple, le service, la marque, le prix, en magasin, la note attribuée, la couleur, le matériel, etc. |
| `refinementValue` | [!UICONTROL String] | Valeur sur laquelle la recherche a été affinée. |
| `resultsPageNumber` | [!UICONTROL Integer] | Pour les résultats de recherche paginés, cette valeur effectue le suivi de la page de résultats consultée par le visiteur. |
| `resultsPerPage` | [!UICONTROL Integer] | Pour les résultats de recherche paginés, cette valeur effectue le suivi du nombre de résultats de recherche affichés par page. |
| `searchType` | [!UICONTROL String] | Capture la méthode de recherche en cours d’exécution, le cas échéant. Par exemple, une recherche avec saisie semi-automatique, une recherche avec saisie directe ou tout autre type de fonctionnalité de recherche personnalisée sur un site. |
| `sortOrder` | [!UICONTROL String] | Combiné à `sortType`, indique l’ordre de tri des résultats de recherche, croissant ou décroissant. |
| `term` | [!UICONTROL String] | Terme de recherche interne sur le site saisi par le visiteur. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
