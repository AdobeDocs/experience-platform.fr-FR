---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;recherche;type de données;type de données;type de données;
solution: Experience Platform
title: Rechercher type de données
description: Découvrez le type de données Modèle de données d’expérience de recherche (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 18%

---

# Type de données [!UICONTROL Search]

[!UICONTROL Recherche] est un type de données standard du modèle de données d’expérience (XDM) qui contient des informations sur l’activité de recherche sur le web.

![rechercher une image](../images/data-types/search.PNG){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `isPaid` | Booléen | Utilisé pour indiquer si la recherche est payante ou non. |
| `keywords` | Chaîne | Mots-clés de la recherche. |
| `pageDepth` | Nombre entier | Profondeur de page dans les résultats de la recherche. |
| `position` | Nombre entier | Position ou classement de la liste dans la page des résultats de recherche. |
| `searchEngine` | Chaîne | Moteur de recherche utilisé pour la recherche. |
| `searchEngineID` | Chaîne | Identifiant spécifique à l’application utilisé pour identifier le moteur de recherche. |
| `slot` | Chaîne | Section nommée de la page dans laquelle s’est affiché le résultat de la recherche. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues que vous définissez, telles que `top`, `side` ou `bottom`. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
