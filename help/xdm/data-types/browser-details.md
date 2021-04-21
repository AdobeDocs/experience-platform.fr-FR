---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; navigateur ; détails du navigateur ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données Détails du navigateur
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM des détails du navigateur.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 19%

---

# [!UICONTROL Type de données ] détaillé du navigateur

[!UICONTROL Le navigateur ] détaille un type de données XDM standard qui décrit les détails relatifs à un navigateur ou une application.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `acceptLanguage` | Chaîne | Balise de langue IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
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
