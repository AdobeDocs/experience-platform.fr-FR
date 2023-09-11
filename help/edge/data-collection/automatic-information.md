---
title: Informations collectées automatiquement
description: Une vue d’ensemble des données que le SDK Web de Adobe Experience Platform collecte automatiquement.
source-git-commit: 89b981104e3cbe597d1556484f4365866bf2a11d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 32%

---

# Informations collectées automatiquement

Le SDK Web de Adobe Experience Platform collecte automatiquement certaines informations prêtes à l’emploi. Si votre entreprise ne souhaite pas collecter automatiquement ces données, vous pouvez utiliser la variable `context` dans le [`configure` command](../fundamentals/configuring-the-sdk.md).

Mots-clés exclus de la variable `context` ne sont pas inclus dans la collecte de données. Si la variable `context` n’existe pas dans le tableau `configure` , toutes les données du tableau ci-dessous sont automatiquement collectées.

| Nom | Description | `context` mot-clé de tableau | Chemin XDM | Exemple de valeur |
| --- | --- | --- | --- | --- |
| Hauteur d’écran | Hauteur de l’écran en pixels. | `device` | `events[].xdm.device.screenHeight` | `900` |
| Largeur d’écran | Largeur de l’écran en pixels. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| Orientation de l’écran | Orientation de l’écran. | `device` | `events[].xdm.device.screenOrientation` | `landscape` ou `portrait`. |
| Type d’environnement | Type d’environnement par lequel l’expérience est apparue. Le SDK Web de Adobe Experience Platform définit toujours ce champ sur `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| Hauteur de la fenêtre d’affichage | Hauteur de la zone de contenu du navigateur en pixels. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| Largeur de la fenêtre d’affichage | Largeur de la zone de contenu du navigateur en pixels. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| Nom du SDK | Identifiant du SDK. Ce champ utilise un URI pour améliorer l’unicité entre les identifiants fournis par différentes bibliothèques de logiciels. Lorsque la bibliothèque autonome est utilisée, la valeur est `https://ns.adobe.com/experience/alloy`. Lorsque la bibliothèque est utilisée dans le cadre de l’extension de balise, la valeur est `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| Version du SDK | Lorsque la bibliothèque autonome est utilisée, la valeur est la version de la bibliothèque. Lorsque la bibliothèque est utilisée dans le cadre de l’extension de balise, la valeur est une concaténation de la version de la bibliothèque et de la version de l’extension de balise. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| Environnement | Environnement dans lequel les données ont été collectées. Le SDK Web de Adobe Experience Platform définit toujours ce champ sur `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| Heure locale | Horodatage local pour l’utilisateur final au format ISO étendu simplifié [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Décalage du fuseau horaire local | Nombre de minutes pendant lesquelles l’utilisateur est décalé par rapport à GMT. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| Date et heure | Horodatage UTC pour l’utilisateur final au format ISO étendu simplifié [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | Toujours inclus | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| URL de la page actuelle | URL de la page active. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| URL du référent | URL de la page précédemment visitée. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
