---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;recherche;type de données;type de données;type de données
solution: Experience Platform
title: Type de données de recherche
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Search Experience Data Model).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 25%

---

# [!UICONTROL Rechercher] type de données

[!UICONTROL Rechercher] est un type de données XDM (Experience Data Model) standard qui contient des informations sur l’activité de recherche web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `isPaid` | Booléen | Utilisé pour indiquer si la recherche est payante ou non. |
| `keywords` | Chaîne | Mots-clés de la recherche. |
| `pageDepth` | Nombre entier | Profondeur de page dans les résultats de la recherche. |
| `position` | Nombre entier | Position ou classement de la liste dans la page des résultats de recherche. |
| `searchEngine` | Chaîne | Moteur de recherche utilisé pour la recherche. |
| `searchEngineID` | Chaîne | Identifiant spécifique à l’application utilisé pour identifier le moteur de recherche. |
| `slot` | Chaîne | Section nommée de la page dans laquelle le résultat de la recherche s’est affiché. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues que vous définissez, par exemple : `top`, `side`ou `bottom`. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
