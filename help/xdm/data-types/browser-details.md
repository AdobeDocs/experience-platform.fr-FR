---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;browser;browser details;datatype;data-type;data type;
solution: Experience Platform
title: Type de données des détails du navigateur
topic: overview
description: Ce document présente un aperçu du type de données XDM des détails du navigateur.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 21%

---


# [!UICONTROL Type de données des détails] du navigateur

[!UICONTROL Les détails] du navigateur sont un type de données XDM standard qui décrit les détails relatifs à un navigateur ou une application.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `acceptLanguage` | Chaîne | An IETF language tag ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booléen | Indique si les paramètres de l’utilisateur autorisent l’écriture de cookies. |
| `javaEnabled` | Booléen | Indique si Java a été activé sur le périphérique à partir duquel l’observation a été effectuée. |
| `javaScriptEnabled` | Booléen | Indique si JavaScript a été activé sur le périphérique à partir duquel l’observation a été effectuée. |
| `javaScriptVersion` | Chaîne | Version de JavaScript prise en charge lors de l’observation. |
| `javaVersion` | Chaîne | Version de Java prise en charge lors de l’observation. |
| `name` | Chaîne | Nom de l’application ou du navigateur. |
| `quicktimeVersion` | Chaîne | Version d’Apple Quicktime prise en charge lors de l’observation. |
| `thirdPartyCookiesEnabled` | Booléen | Indique si les cookies tiers ont été activés sur le périphérique à partir duquel l’observation a été effectuée. |
| `userAgent` | Chaîne | Chaîne HTTP user-agent issue de la demande du client. |
| `vendor` | Chaîne | Fournisseur de l’application ou du navigateur. |
| `version` | Chaîne | Version de l’application ou du navigateur. |
| `viewportHeight` | Entier | Taille verticale en pixels de la fenêtre dans laquelle le événement s’affichait. Pour un événement de vue Web, il s’agit de la hauteur de fenêtre d’affichage du navigateur. |
| `viewportWidth` | Entier | Taille horizontale en pixels de la fenêtre dans laquelle le événement s’affichait. Pour un événement de vue Web, il s’agit de la largeur de fenêtre d’affichage du navigateur. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)