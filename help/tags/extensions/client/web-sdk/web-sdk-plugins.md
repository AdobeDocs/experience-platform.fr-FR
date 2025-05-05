---
title: Présentation de l’extension de modules externes SDK Web courants
description: Découvrez l’extension de balise des modules externes SDK Web courants dans Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# Présentation de l’extension de modules externes SDK Web courants

>[!IMPORTANT]
>
>L’extension est destinée à être utilisée avec l’extension SDK Web de Adobe Experience Platform. Pour obtenir des informations sur la version qui doit être utilisée avec AppMeasurement, reportez-vous à la présentation de l’ [ extension de modules externes courants Analytics](../plugins/overview.md).

Ce document explique comment configurer l’extension de balise des modules externes du SDK Web et l’utiliser pour augmenter l’ [extension du SDK Web Adobe Experience Platform](../web-sdk/overview.md).

## Configuration de l’extension de modules externes SDK Web courants

Cette section fournit une référence pour les options disponibles lors de la configuration de l’extension des modules externes SDK Web.

>[!IMPORTANT]
>
>L’extension de modules externes SDK Web courants est destinée à augmenter l’extension du SDK Web Adobe Experience Platform. Toutefois, il n’est pas nécessaire de l’installer pour que l’extension fonctionne comme prévu.

## Ajout de modules externes à l’extension SDK Web Adobe Experience Platform

Aucune configuration n’est nécessaire pour initialiser ou ajouter un module externe à votre bibliothèque en dehors de l’utilisation des éléments de données natifs suivants fournis par l’extension de modules externes SDK Web courants :

* [`getAndPersistValue`](#getAndPersistValue)
* [`getGeoCoordinates`](#getGeoCoordinates)
* [`getNewRepeat`](#getNewRepeat)
* [`getPageName`](#getPagename)
* [`getPreviousValue`](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [`getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [&grave;getValOnce](#getValOnce)
* [`getVisitDuration`](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [`pFo`](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies et permet de stocker les valeurs générées par l’utilisateur dans les cookies. Pour plus d’informations, reportez-vous à la documentation spécifique au plug-in .

Permet de configurer le [`getAndPersistValue` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). L’élément de données `getAndPersistValue` stocke une valeur dans un cookie qui peut être récupérée ultérieurement au cours d’une visite.

L’élément de données `getAndPersistValue` fournit les arguments suivants :

* `vtp` (obligatoire) : valeur à conserver d’une page à l’autre.
* `cn` (facultatif) : nom du cookie permettant de stocker la valeur. Si cet argument n’est pas défini, le cookie est nommé `"s_gapv"`
* `ex` (facultatif) : nombre de jours avant l’expiration du cookie. Si cet argument est défini sur `0` ou n’est pas défini, le cookie expire à la fin de la visite (30 minutes d’inactivité).

Si la variable de l’argument `vtp` est définie, l’élément de données définit le cookie, puis renvoie la valeur du cookie. Si la variable de l’argument `vtp` n’est pas définie, l’élément de données renvoie uniquement la valeur du cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Ce plug-in nécessite un accès à l’emplacement sur le client, mais ne renvoie pas d’exception s’il ne l’obtient pas.

Permet de configurer le [`getGeoCoordinates` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). L’élément de données `getGeoCoordinates` capture la latitude et la longitude des appareils des visiteurs.

L’élément de données `getGeoCoordinates` n’utilise aucun argument. Elle renvoie l’une des valeurs suivantes :

* `"geo coordinates not available"` : pour les appareils qui ne disposent pas de données de géolocalisation au moment de l’exécution du module externe. Cette valeur est courante lors du premier accès de la visite, en particulier lorsque les visiteurs doivent d’abord donner leur consentement pour effectuer le suivi de leur emplacement.
* `"error retrieving geo coordinates"` : lorsque le module externe rencontre des erreurs lors de la tentative de récupération de l’emplacement de l’appareil
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"` : où [LATITUDE]/[LONGITUDE] sont respectivement la latitude et la longitude

### `getNewRepeat`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Pour plus d’informations, reportez-vous à la documentation spécifique au plug-in .

Permet de configurer le [`getNewRepeat` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). L’élément de données `getNewRepeat` détermine si un visiteur sur le site est un nouveau visiteur ou un visiteur régulier pendant le nombre de jours souhaité.

L’élément de données `getNewRepeat` utilise les arguments suivants :

* `d` (entier, facultatif) : nombre minimum de jours requis entre les visites qui réinitialise le statut des visiteurs à `"New"`. Si cet argument n’est pas défini, il prend par défaut 30 jours.

Cet élément de données renvoie la valeur de `"New"` si le cookie défini par l’élément de données n’existe pas ou a expiré. Elle renvoie la valeur de `"Repeat"` si le cookie défini par l’élément de données existe et que le temps écoulé depuis l’accès actif et celui défini dans le cookie sont supérieurs à 30 minutes. Cette méthode renvoie la même valeur pour une visite entière.

### `getPageName`

Permet de configurer le [`getPageName` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). L’élément de données `getPageName` crée une version formatée facile à lire et conviviale de l’URL actuelle.

L’élément de données `getPageName` utilise les arguments suivants :

* `si` (facultatif, chaîne) : identifiant inséré au début de la chaîne représentant l’identifiant du site. Cette valeur peut être un identifiant numérique ou un nom convivial. Lorsqu’elle n’est pas définie, le domaine actif est défini par défaut.
* `qv` (facultatif, chaîne) : liste délimitée par des virgules de paramètres de chaîne de requête qui, s’ils figurent dans l’URL, sont ajoutés à la chaîne.
* `hv` (facultatif, chaîne) : liste délimitée par des virgules de paramètres trouvés dans le hachage de l’URL qui, s’ils figurent dans l’URL, sont ajoutés à la chaîne.
* `de` (facultatif, chaîne) : délimiteur permettant de séparer les différentes parties de la chaîne. La valeur par défaut est une barre verticale (`|`).

L’élément de données renvoie une chaîne contenant une version formatée de l’URL. Cette chaîne est généralement attribuée à la variable `pageName`, mais peut également être utilisée dans d’autres variables.

### `getPreviousValue`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies et permet de stocker les valeurs générées par l’utilisateur dans les cookies. Pour plus d’informations, reportez-vous à la documentation spécifique au plug-in .

Permet de configurer le [`getPreviousValue` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). L’élément de données `getPreviousValue` définit une variable sur une valeur définie lors d’un précédent accès.

L’élément de données `getPreviousValue` utilise les arguments suivants :

* `v` (chaîne, obligatoire) : variable dont la valeur doit être transmise à la demande d’image suivante. Une variable courante utilisée est `s.pageName` pour récupérer la valeur de la page précédente.
* `c` (chaîne, facultatif) : nom du cookie qui stocke la valeur.  Si cet argument n’est pas défini, il est défini par défaut sur `"s_gpv"`.

Lorsque vous appelez cet élément de données, il renvoie la valeur de chaîne contenue dans le cookie. Le plug-in réinitialise ensuite l’expiration du cookie et lui affecte la valeur de variable de l’argument `v`. Le cookie expire après 30 minutes d’inactivité.

### `getQueryParam`

Permet de configurer le [`getQueryParam` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). L’élément de données `getQueryParam` extrait la valeur de tout paramètre de chaîne de requête contenu dans une URL. Elle est utile pour extraire les codes de campagne, internes et externes, des URL de page d’entrée. Elle est également utile lors de l’extraction de termes de recherche ou d’autres paramètres de chaîne de requête. Cet élément de données fournit des fonctionnalités puissantes pour l’analyse d’URL complexes, y compris les hachages et les URL contenant plusieurs paramètres de chaîne de requête.

L’élément de données `getQueryParam` utilise les arguments suivants :

* `qsp` (obligatoire) : liste, délimitée par des virgules, de paramètres de chaîne de requête à rechercher dans l’URL. Il n’est pas sensible à la casse.
* `de` (facultatif) : délimiteur à utiliser si plusieurs paramètres de chaîne de requête correspondent. La valeur par défaut est une chaîne vide.
* `url` (facultatif) : URL, chaîne ou variable personnalisée à partir de laquelle extraire les valeurs des paramètres de chaîne de requête. La valeur par défaut est `window.location`.

L’appel de cet élément de données renvoie une valeur en fonction des arguments ci-dessus et de l’URL :

* Si aucun paramètre de chaîne de requête correspondant n’est trouvé, la méthode renvoie une chaîne vide.
* Si un paramètre de chaîne de requête correspondant est trouvé, la méthode renvoie la valeur du paramètre de chaîne de requête.
* Si un paramètre de chaîne de requête correspondant est trouvé mais que la valeur est vide, la méthode renvoie `true`.
* Si plusieurs paramètres de chaîne de requête correspondants sont trouvés, la méthode renvoie une chaîne dont chaque valeur de paramètre est délimitée par la chaîne dans l’argument `de`.

### `getTimeParting`

Permet de configurer le [`getTimeParting` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). L’élément de données `getTimeParting` capture les détails du moment où une activité mesurable a lieu sur votre site. Cet élément de données est utile lorsque vous souhaitez ventiler les mesures selon une division répétable du temps sur une période donnée. Vous pouvez par exemple comparer des taux de conversion entre deux jours différents de la semaine, par exemple tous les dimanches et tous les jeudis. Vous pouvez également comparer les périodes de la journée, par exemple tous les matins et tous les soirs.

L’élément de données `getTimeParting` utilise l’argument suivant :

`t` (chaîne facultative mais recommandée) : nom du fuseau horaire auquel convertir l’heure locale du visiteur.  La valeur par défaut est UTC/GMT. Reportez-vous à la [Liste des fuseaux horaires de la base de données TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) sur Wikipédia pour obtenir une liste complète des valeurs valides.

Les valeurs valides courantes sont les suivantes :

* `"America/New_York"` pour l’heure de l’Est
* `"America/Chicago"` pour l’heure normale du Centre
* `"America/Denver"` pour l’heure de montagne
* `"America/Los_Angeles"` pour l’heure Pacifique

L’appel de cet élément de données renvoie une chaîne contenant les éléments suivants délimités par une barre verticale (`|`) :

* L’année en cours
* Le mois en cours
* Jour du mois
* Jour de la semaine
* Heure actuelle (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Pour plus d’informations, reportez-vous à la documentation spécifique au plug-in .

Permet de configurer le [`getTimeSinceLastVisit` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). L’élément de données `getTimeSinceLastVisit` effectue le suivi du temps nécessaire à un visiteur pour revenir sur votre site après sa dernière visite.

L’élément de données `getTimeSinceLastVisit` n’utilise aucun argument. Elle renvoie le temps écoulé depuis la dernière visite du visiteur sur le site, regroupé au format suivant :

* La durée comprise entre 30 minutes et une heure depuis la dernière visite est définie sur la référence d’une demi-minute la plus proche. Par exemple, `"30.5 minutes"`, `"53 minutes"`
* Le temps entre une heure et un jour est arrondi à la référence d’un quart d’heure la plus proche. Par exemple, `"2.25 hours"`, `"7.5 hours"`
* Le temps supérieur à un jour est arrondi à la référence de jour la plus proche. Par exemple, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Si un visiteur ne s’est pas rendu sur le site avant ou si le temps écoulé est supérieur à deux ans, la valeur est définie sur `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies et permet de stocker les valeurs générées par l’utilisateur dans les cookies. Pour plus d’informations, reportez-vous à la documentation spécifique au plug-in .

Permet de configurer le [`getValOnce` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). L’élément de données `getValOnce` empêche qu’une variable soit définie plusieurs fois sur la même valeur.

L’élément de données `getValOnce` utilise les arguments suivants :

* `vtc` (obligatoire, chaîne) : variable à vérifier et à vérifier si elle vient d’être définie sur une valeur identique.
* `cn` (facultatif, chaîne) : nom du cookie qui contient la valeur à vérifier. Par défaut : `"s_gvo"`
* `et` (facultatif, entier) : expiration du cookie en jours (ou en minutes, selon l’argument `ep`). La valeur par défaut est `0`, qui expire à la fin de la session du navigateur.
* `ep` (facultatif, chaîne) : définissez cet argument uniquement si l’argument `et` est également défini. Définissez cet argument sur `"m"` si vous souhaitez que l’argument `et` expire en minutes plutôt qu’en jours. La valeur par défaut est `"d"`, ce qui définit l’argument `et` en jours.

Si l’argument `vtc` et la valeur du cookie correspondent, cette méthode renvoie une chaîne vide. Si l’argument `vtc` et la valeur du cookie ne correspondent pas, la méthode renvoie l’argument `vtc` sous la forme d’une chaîne.

### `getVisitDuration`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Pour plus d’informations, reportez-vous à la documentation spécifique au plug-in .

Permet de configurer le [`getVisitDuration` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). L’élément de données `getVisitDuration` effectue le suivi en minutes de la durée de la visite du visiteur sur le site jusqu’à ce moment-là.

L’élément de données `getVisitDuration` n’utilise aucun argument. Elle renvoie l’une des valeurs suivantes :

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (où `[x]` est le nombre de minutes écoulées depuis l’arrivée du visiteur sur le site)

### `getVisitNum`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Pour plus d’informations, reportez-vous à la documentation spécifique au plug-in .

Permet de configurer le [`getVisitNum` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). L’élément de données `getVisitNum` renvoie le nombre de visites pour tous les visiteurs qui se rendent sur le site au cours du nombre de jours souhaité.

L’élément de données `getVisitNum` utilise les arguments suivants :

* `rp` (facultatif, entier OU chaîne) : nombre de jours avant la réinitialisation du compteur de visites.  La valeur par défaut est `365` lorsqu’elle n’est pas définie.
   * Lorsque cet argument est `"w"`, le compteur se réinitialise à la fin de la semaine (ce samedi à 23 h 59).
   * Lorsque cet argument est `"m"`, le compteur se réinitialise à la fin du mois (le dernier jour de ce mois).
   * Lorsque cet argument est de `"y"`, le compteur se réinitialise à la fin de l’année (le 31 décembre).
* `erp` (facultatif, booléen) : lorsque l’argument `rp` est un nombre, cet argument détermine si l’expiration du nombre de visites doit être étendue. S’il est défini sur `true`, les accès ultérieurs à votre site réinitialisent le compteur de visites. S’il est défini sur `false`, les accès ultérieurs à votre site ne s’étendent pas lorsque le compteur de visites est réinitialisé. La valeur par défaut est `true`. Cet argument n’est pas valide lorsque l’argument `rp` est une chaîne.

Le nombre de visites augmente chaque fois que le visiteur revient sur votre site après 30 minutes d’inactivité. L’appel de cette méthode renvoie un entier représentant le nombre de visites actuel du visiteur.

### `p_fo` (Page First Only)

Permet de configurer le [`p_fo` module externe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). L’élément de données `p_fo` est un utilitaire qui vérifie l’existence d’un objet JavaScript spécifique. Si l’objet n’existe pas, le plug-in crée l’objet et renvoie `true`. Si l’objet JavaScript existe déjà sur la page, il renvoie `false`. Cet élément de données est utile pour exécuter le code une seule fois sur une page.

L’élément de données `p_fo` utilise les arguments suivants :

* `on` (obligatoire, chaîne) : nom de l’objet JavaScript créé par l’élément de données si l’objet n’existe pas encore sur la page.

Si l’objet n’existe pas encore, cette méthode renvoie `true` et crée l’objet. Si l’objet existe déjà, cette méthode renvoie `false`.
