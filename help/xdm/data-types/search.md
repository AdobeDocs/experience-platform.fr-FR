---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;recherche;type de données;type de données;type de données;
solution: Experience Platform
title: Rechercher type de données
description: Découvrez le type de données Modèle de données d’expérience de recherche (XDM).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
TQID: https://experienceleague.adobe.com/8hPqVpN96g0k5bDAiVgZHTAcxYKiH-qWIQTHF-NTkWg
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 182
ht-degree: 16%

---

# Type de données [!UICONTROL Search]

[!UICONTROL Recherche] est un type de données standard du modèle de données d’expérience (XDM) qui contient des informations sur l’activité de recherche sur le web.

![rechercher une image](../images/data-types/search.PNG){width=500}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `isPaid` | Booléen | Utilisé pour indiquer si la recherche est payante ou non. |
| `keywords` | Chaîne | Mots-clés de la recherche. |
| `pageDepth` | Entier | Profondeur de page dans les résultats de la recherche. |
| `position` | Entier | Position ou classement de la liste dans la page des résultats de recherche. |
| `searchEngine` | Chaîne | Moteur de recherche utilisé pour la recherche. |
| `searchEngineID` | Chaîne | Identifiant spécifique à l’application utilisé pour identifier le moteur de recherche. |
| `slot` | Chaîne | Section nommée de la page dans laquelle s’est affiché le résultat de la recherche. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues que vous définissez, telles que `top`, `side` ou `bottom`. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
