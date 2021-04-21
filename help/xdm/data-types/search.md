---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; recherche ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données de recherche
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Search Experience Data Model).
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 16%

---

# [!UICONTROL Type ] de données de recherche

[!UICONTROL La ] recherche est un type de données XDM (Experience Data Model) standard qui contient des informations sur l’activité de la recherche Web.

<img src="../images/data-types/search.PNG" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `isPaid` | Booléen | Permet d’indiquer si la recherche est payée ou non. |
| `keywords` | Chaîne | Mots-clés de la recherche. |
| `pageDepth` | Entier | Profondeur de page dans les résultats de la recherche. |
| `position` | Entier | Position ou classement de la liste dans la page des résultats de la recherche. |
| `searchEngine` | Chaîne | Moteur de recherche utilisé pour la recherche. |
| `searchEngineID` | Chaîne | Identificateur spécifique à l&#39;application utilisé pour identifier le moteur de recherche. |
| `slot` | Chaîne | Section nommée de la page sur laquelle le résultat de la recherche est apparu. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues que vous définissez, par exemple `top`, `side` ou `bottom`. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
