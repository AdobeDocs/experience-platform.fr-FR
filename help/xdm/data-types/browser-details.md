---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;navigateur;détails du navigateur;type de données;type de données;type de données
solution: Experience Platform
title: Type de données Détails du navigateur
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM Détails du navigateur.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 20%

---

# [!UICONTROL Type de données ] Détails du navigateur

[!UICONTROL Les ] détails du navigateur correspondent à un type de données XDM standard qui décrit les détails relatifs à un navigateur ou à une application.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `acceptLanguage` | Chaîne | Balise de langue IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booléen | Indique si les paramètres de l’utilisateur permettent l’écriture de cookies. |
| `javaEnabled` | Booléen | Indique si Java a été activé sur l’appareil à partir duquel l’observation a été effectuée. |
| `javaScriptEnabled` | Booléen | Indique si JavaScript a été activé sur le périphérique à partir duquel l’observation a été effectuée. |
| `javaScriptVersion` | Chaîne | Version de JavaScript prise en charge lors de l’observation. |
| `javaVersion` | Chaîne | Version de Java prise en charge lors de l’observation. |
| `name` | Chaîne | Nom de l’application ou du navigateur. |
| `quicktimeVersion` | Chaîne | Version d’Apple Quicktime prise en charge lors de l’observation. |
| `thirdPartyCookiesEnabled` | Booléen | Indique si les cookies tiers ont été activés dans l’appareil à partir duquel l’observation a été effectuée. |
| `userAgent` | Chaîne | Chaîne de l’agent utilisateur HTTP issue de la demande du client. |
| `vendor` | Chaîne | Fournisseur de l’application ou du navigateur. |
| `version` | Chaîne | Version de l’application ou du navigateur. |
| `viewportHeight` | Entier | Taille verticale en pixels de la fenêtre dans laquelle l’événement a été affiché. Pour un événement d’affichage Web, il s’agit de la hauteur de la fenêtre d’affichage du navigateur. |
| `viewportWidth` | Entier | Taille horizontale en pixels de la fenêtre dans laquelle l’événement a été affiché. Pour un événement d’affichage Web, il s’agit de la largeur de la fenêtre d’affichage du navigateur. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
