---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;navigateur;détails du navigateur;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données des détails du navigateur
description: Découvrez le type de données XDM des détails du navigateur.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 27%

---

# [!UICONTROL Informations sur le navigateur] type de données

[!UICONTROL Détails du navigateur] est un type de données XDM standard qui décrit les détails relatifs à un navigateur ou à une application.

![](../images/data-types/browser-details.png){width=450}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `acceptLanguage` | Chaîne | Balise de langue IETF ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Booléen | Indique si les paramètres de l’utilisateur ou de l’utilisatrice permettent l’écriture de cookies. |
| `javaEnabled` | Booléen | Indique si Java a été activé sur l’appareil à partir duquel l’observation a été effectuée. |
| `javaScriptEnabled` | Booléen | Indique si JavaScript a été activé sur l’appareil à partir duquel l’observation a été effectuée. |
| `javaScriptVersion` | Chaîne | Version de JavaScript prise en charge lors de l’observation. |
| `javaVersion` | Chaîne | Version de Java prise en charge lors de l’observation. |
| `name` | Chaîne | Nom de l’application ou du navigateur. |
| `quicktimeVersion` | Chaîne | Version d’Apple Quicktime prise en charge lors de l’observation. |
| `thirdPartyCookiesEnabled` | Booléen | Indique si les cookies tiers ont été activés dans l’appareil à partir duquel l’observation a été effectuée. |
| `userAgent` | Chaîne | Chaîne user-agent HTTP de la demande du client. |
| `vendor` | Chaîne | Fournisseur de l’application ou du navigateur. |
| `version` | Chaîne | La version de l’application ou du navigateur. |
| `viewportHeight` | Nombre entier | Taille verticale en pixels de la fenêtre à l’intérieur de laquelle l’événement était affiché. Pour un événement d’affichage web, il s’agit de la hauteur de la fenêtre d’affichage du navigateur. |
| `viewportWidth` | Nombre entier | Taille horizontale en pixels de la fenêtre à l’intérieur de laquelle l’événement était affiché. Pour un événement d’affichage web, il s’agit de la largeur de la fenêtre d’affichage du navigateur. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
