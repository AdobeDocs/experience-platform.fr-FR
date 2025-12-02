---
title: Présentation De L’Extension De Modules Externes Web SDK Courants
description: Découvrez l’extension de balise des modules externes courants de SDK Web dans Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 0%

---

# Présentation de l’extension de modules externes courants Web SDK

>[!IMPORTANT]
>
>L’extension est destinée à être utilisée avec l’extension Adobe Experience Platform Web SDK. Pour obtenir des informations sur la version destinée à être utilisée avec AppMeasurement, reportez-vous à la présentation de l’extension [Plug-ins Analytics courants](../plugins/overview.md).

Ce document explique comment configurer l’extension de balise Plugins de Web SDK et l’utiliser pour étendre l’extension de SDK Web [Adobe Experience Platform](../web-sdk/overview.md).

## Configuration de l’extension de modules externes courants de Web SDK

Cette section fournit des informations relatives aux options disponibles lors de la configuration de l’extension de modules externes Web SDK.

>[!IMPORTANT]
>
>L’extension de modules externes courants Web SDK est destinée à compléter l’extension Adobe Experience Platform Web SDK. Toutefois, vous n’avez pas besoin de l’installer pour que l’extension fonctionne comme prévu.

## Ajout de modules externes à l’extension Adobe Experience Platform Web SDK

Aucune configuration n’est nécessaire pour initialiser ou ajouter un module externe à votre bibliothèque en dehors de l’utilisation des éléments de données natifs suivants fournis par l’extension de modules externes de SDK Web communs :

* [`getAndPersistValue`](web-sdk-plugins.md#getandpersistvalue)
* [`getGeoCoordinates`](#getgeocoordinates)
* [`getNewRepeat`](#getnewrepeat)
* [`getPageName`](#getpagename)
* [`getPreviousValue`](#getpreviousvalue)
* [`getQueryParam`](#getqueryparam)
* [`getTimeParting`](#gettimeparting)
* [`getTimeSinceLastVisit`](#gettimesincelastvisit)
* [`getValOnce`](#getvalonce)
* [`getVisitDuration`](#getvisitduration)
* [`getVisitNum`](#getvisitnum)
* [`p_fo`](#p_fo-page-first-only)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies et permet de stocker les valeurs générées par l’utilisateur dans les cookies. Reportez-vous à la documentation spécifique au plug-in pour plus d’informations.

Permet d’installer et de configurer le plug-in [`getAndPersistValue` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html?lang=fr). L’élément de données `getAndPersistValue` stocke une valeur dans un cookie qui peut être récupérée ultérieurement au cours d’une visite.

L’élément de données `getAndPersistValue` fournit les arguments suivants :

* `vtp` (obligatoire) : valeur à conserver d’une page à l’autre
* `cn` (facultatif) : nom du cookie dans lequel stocker la valeur. Si cet argument n’est pas défini, le cookie est nommé `"s_gapv"`
* `ex` (facultatif) : nombre de jours avant l’expiration du cookie. Si cet argument est `0` ou n’est pas défini, le cookie expire à la fin de la visite (30 minutes d’inactivité).

Si la variable dans l’argument `vtp` est définie, l’élément de données définit le cookie puis renvoie la valeur du cookie. Si la variable dans l’argument `vtp` n’est pas définie, l’élément de données renvoie uniquement la valeur du cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Ce plug-in nécessite un accès à l’emplacement sur le client, mais ne renvoie pas d’exception s’il ne l’obtient pas.

Permet d’installer et de configurer le plug-in [`getGeoCoordinates` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html?lang=fr). L’élément de données `getGeoCoordinates` capture la latitude et la longitude des appareils des visiteurs.

L’élément de données `getGeoCoordinates` n’utilise aucun argument. Elle renvoie l’une des valeurs suivantes :

* `"geo coordinates not available"` : pour les appareils qui ne disposent pas de données de géolocalisation au moment de l’exécution du module. Cette valeur est courante lors du premier accès de la visite, en particulier lorsque les visiteurs doivent d’abord donner leur consentement pour le suivi de leur emplacement.
* `"error retrieving geo coordinates"` : lorsque le plug-in rencontre des erreurs lors de la tentative de récupération de l’emplacement de l’appareil
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"` : où `[LATITUDE]/[LONGITUDE]` sont la latitude et la longitude, respectivement

### `getNewRepeat`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Reportez-vous à la documentation spécifique au plug-in pour plus d’informations.

Permet d’installer et de configurer le plug-in [`getNewRepeat` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html?lang=fr). L’élément de données `getNewRepeat` détermine si un visiteur ou une visiteuse sur le site est un nouveau visiteur ou un visiteur récurrent au cours du nombre de jours souhaité.

L’élément de données `getNewRepeat` utilise les arguments suivants :

* `d` (entier, facultatif) : nombre minimum de jours requis entre les visites qui réinitialise les visiteurs et visiteuses sur `"New"`. Si cet argument n’est pas défini, la valeur par défaut est de 30 jours.

Cet élément de données renvoie la valeur de `"New"` si le cookie défini par l’élément de données n’existe pas ou a expiré. Elle renvoie la valeur de `"Repeat"` si le cookie défini par l’élément de données existe et si le temps écoulé depuis l’accès actif et celui défini dans le cookie sont supérieurs à 30 minutes. Cette méthode renvoie la même valeur pour une visite complète.

### `getPageName`

Permet d’installer et de configurer le plug-in [`getPageName` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html?lang=fr). L’élément de données `getPageName` crée une version formatée conviviale et facile à lire de l’URL actuelle.

L’élément de données `getPageName` utilise les arguments suivants :

* `si` (facultatif, chaîne) : identifiant inséré au début de la chaîne représentant l’identifiant du site. Cette valeur peut être un identifiant numérique ou un nom convivial. Lorsqu’il n’est pas défini, il correspond par défaut au domaine actif.
* `qv` (facultatif, chaîne) : liste délimitée par des virgules de paramètres de chaîne de requête qui, s’ils se trouvent dans l’URL, sont ajoutés à la chaîne
* `hv` (facultatif, chaîne) : liste délimitée par des virgules de paramètres trouvés dans le hachage de l’URL qui, s’ils se trouvent dans l’URL, sont ajoutés à la chaîne
* `de` (facultatif, chaîne) : délimiteur permettant de fractionner des parties individuelles de la chaîne. La valeur par défaut est une barre verticale (`|`).

L’élément de données renvoie une chaîne contenant une version formatée conviviale de l’URL. Cette chaîne est généralement attribuée à la variable `pageName`, mais peut également être utilisée dans d’autres variables.

### `getPreviousValue`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies et permet de stocker les valeurs générées par l’utilisateur dans les cookies. Reportez-vous à la documentation spécifique au plug-in pour plus d’informations.

Permet d’installer et de configurer le plug-in [`getPreviousValue` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html?lang=fr). L’élément de données `getPreviousValue` définit une variable sur une valeur définie sur un accès précédent.

L’élément de données `getPreviousValue` utilise les arguments suivants :

* `v` (chaîne, obligatoire) : variable contenant la valeur que vous souhaitez transmettre à la demande d’image suivante. Une variable couramment utilisée est `s.pageName` pour récupérer la valeur de la page précédente.
* `c` (chaîne, facultatif) : nom du cookie qui stocke la valeur.  Si cet argument n’est pas défini, la valeur par défaut est `"s_gpv"`.

Lorsque vous appelez cet élément de données, il renvoie la valeur de chaîne contenue dans le cookie. Le plug-in réinitialise ensuite l’expiration du cookie et lui affecte la valeur de variable à partir de l’argument `v`. Le cookie expire après 30 minutes d’inactivité.

### `getQueryParam`

Permet d’installer et de configurer le plug-in [`getQueryParam` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html?lang=fr). L’élément de données `getQueryParam` extrait la valeur de tout paramètre de chaîne de requête contenu dans une URL. Elle est utile pour extraire des codes de campagne, internes et externes, à partir des URL de page de destination. Il est également utile lors de l’extraction de termes de recherche ou d’autres paramètres de chaîne de requête. Cet élément de données fournit des fonctionnalités fiables pour l’analyse d’URL complexes, y compris des hachages et des URL contenant plusieurs paramètres de chaîne de requête.

L’élément de données `getQueryParam` utilise les arguments suivants :

* `qsp` (obligatoire) : liste délimitée par des virgules de paramètres de chaîne de requête à rechercher dans l’URL. Elle n’est pas sensible à la casse.
* `de` (facultatif) : délimiteur à utiliser si plusieurs paramètres de chaîne de requête correspondent. La valeur par défaut est une chaîne vide.
* `url` (facultatif) : URL, chaîne ou variable personnalisée à partir de laquelle extraire les valeurs de paramètre de chaîne de requête. La valeur par défaut est `window.location`.

L’appel de cet élément de données renvoie une valeur en fonction des arguments ci-dessus et de l’URL :

* Si un paramètre de chaîne de requête correspondant est introuvable, la méthode renvoie une chaîne vide.
* Si un paramètre de chaîne de requête correspondant est trouvé, la méthode renvoie la valeur de ce paramètre.
* Si un paramètre de chaîne de requête correspondant est trouvé mais que la valeur est vide, la méthode renvoie `true`.
* Si plusieurs paramètres de chaîne de requête correspondants sont trouvés, la méthode renvoie une chaîne avec chaque valeur de paramètre délimitée par la chaîne dans l’argument `de`.

### `getTimeParting`

Permet d’installer et de configurer le plug-in [`getTimeParting` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html?lang=fr). L’élément de données `getTimeParting` capture les détails du moment où une activité mesurable a lieu sur votre site. Cet élément de données est utile lorsque vous souhaitez ventiler les mesures selon une division du temps répétable sur une période donnée. Par exemple, vous pouvez comparer les taux de conversion entre deux jours différents de la semaine, comme tous les dimanches par rapport à tous les jeudis. Vous pouvez également comparer les périodes de la journée, par exemple tous les matins par rapport à tous les soirs.

L’élément de données `getTimeParting` utilise l’argument suivant :

`t` (chaîne facultative mais recommandée) : nom du fuseau horaire dans lequel convertir l’heure locale du visiteur.  La valeur par défaut est l’heure UTC/GMT. Reportez-vous à la [Liste des fuseaux horaires de la base de données TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) sur Wikipédia pour une liste complète des valeurs valides.

Les valeurs valides courantes sont les suivantes :

* `"America/New_York"` pour l&#39;heure de l&#39;Est
* `"America/Chicago"` pour Central Time
* `"America/Denver"` pour l&#39;heure des montagnes
* `"America/Los_Angeles"` pour heure du Pacifique

L’appel de cet élément de données renvoie une chaîne contenant les éléments suivants délimités par une barre verticale (`|`) :

* L’année en cours
* Le mois en cours
* Le jour du mois
* Jour de la semaine
* L’heure actuelle (matin/après-midi)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Reportez-vous à la documentation spécifique au plug-in pour plus d’informations.

Permet d’installer et de configurer le plug-in [`getTimeSinceLastVisit` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html?lang=fr). L’élément de données `getTimeSinceLastVisit` effectue le suivi du temps pris par un visiteur pour revenir sur votre site après sa dernière visite.

L’élément de données `getTimeSinceLastVisit` n’utilise aucun argument. Elle renvoie la durée écoulée depuis la dernière visite du visiteur sur le site, regroupée au format suivant :

* Le temps écoulé entre 30 minutes et une heure depuis la dernière visite correspond à la valeur repère de la demi-minute la plus proche. Par exemple, `"30.5 minutes"`, `"53 minutes"`
* Le temps entre une heure et une journée est arrondi au quart d&#39;heure de référence le plus proche. Par exemple, `"2.25 hours"`, `"7.5 hours"`
* La durée supérieure à un jour est arrondie au jour de référence le plus proche. Par exemple, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Si un visiteur n’a jamais effectué de visite auparavant ou si le temps écoulé est supérieur à deux ans, la valeur est définie sur `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies et permet de stocker les valeurs générées par l’utilisateur dans les cookies. Reportez-vous à la documentation spécifique au plug-in pour plus d’informations.

Permet d’installer et de configurer le plug-in [`getValOnce` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html?lang=fr). L’élément de données `getValOnce` empêche qu’une variable soit définie sur la même valeur plusieurs fois.

L’élément de données `getValOnce` utilise les arguments suivants :

* `vtc` (obligatoire, chaîne) : variable à vérifier et voir si elle vient d’être définie sur une valeur identique
* `cn` (facultatif, chaîne) : nom du cookie qui contient la valeur à vérifier. La valeur par défaut est `"s_gvo"`
* `et` (facultatif, entier) : expiration du cookie en jours (ou minutes, selon l’argument `ep`). La valeur par défaut est `0`, qui expire à la fin de la session du navigateur
* `ep` (facultatif, chaîne) : définissez cet argument uniquement si l’argument `et` est également défini. Définissez cet argument sur `"m"` si vous souhaitez que l’argument `et` expire en minutes au lieu de jours. La valeur par défaut est `"d"`, ce qui définit l’argument `et` en jours.

Si l’argument `vtc` et la valeur du cookie correspondent, cette méthode renvoie une chaîne vide. Si l’argument `vtc` et la valeur du cookie ne correspondent pas, la méthode renvoie l’argument `vtc` sous la forme d’une chaîne.

### `getVisitDuration`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Reportez-vous à la documentation spécifique au plug-in pour plus d’informations.

Permet d’installer et de configurer le plug-in [`getVisitDuration` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html?lang=fr). L’élément de données `getVisitDuration` effectue le suivi de la durée, en minutes, pendant laquelle le visiteur a séjourné sur le site jusqu’à ce point.

L’élément de données `getVisitDuration` n’utilise aucun argument. Elle renvoie l’une des valeurs suivantes :

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (où `[x]` est le nombre de minutes écoulées depuis que le visiteur a atterri sur le site)

### `getVisitNum`

>[!IMPORTANT]
>
>Cet élément de données définit les cookies. Reportez-vous à la documentation spécifique au plug-in pour plus d’informations.

Permet d’installer et de configurer le plug-in [`getVisitNum` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html?lang=fr). L’élément de données `getVisitNum` renvoie le nombre de visites pour tous les visiteurs qui se rendent sur le site au cours du nombre de jours souhaité.

L’élément de données `getVisitNum` utilise les arguments suivants :

* `rp` (facultatif, entier OU chaîne) : nombre de jours avant la réinitialisation du compteur de nombre de visites.  La valeur par défaut est `365` lorsqu’elle n’est pas définie.
   * Lorsque cet argument est `"w"`, le compteur se réinitialise à la fin de la semaine (ce samedi à 23:59)
   * Lorsque cet argument est `"m"`, le compteur se réinitialise à la fin du mois (le dernier jour de ce mois)
   * Lorsque cet argument est `"y"`, le compteur se réinitialise à la fin de l’année (31 décembre)
* `erp` (facultatif, booléen) : lorsque l’argument `rp` est un nombre, cet argument détermine si l’expiration du nombre de visites doit être étendue. Si cette valeur est définie sur `true`, les accès suivants à votre site réinitialisent le compteur de nombre de visites. Si ce paramètre est défini sur `false`, les accès suivants à votre site ne sont pas étendus lorsque le compteur du nombre de visites se réinitialise. La valeur par défaut est `true`. Cet argument n’est pas valide lorsque l’argument `rp` est une chaîne.

Incrément du nombre de visites chaque fois que le visiteur revient sur votre site après 30 minutes d’inactivité. L’appel de cette méthode renvoie un entier qui représente le numéro de visite actuel du visiteur.

### `p_fo` (Page First Uniquement)

Permet d’installer et de configurer le plug-in [`p_fo` Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html?lang=fr). L’élément de données `p_fo` est un utilitaire qui vérifie l’existence d’un objet JavaScript spécifique. Si l’objet n’existe pas, le plug-in crée l’objet et renvoie `true`. Si l’objet JavaScript existe déjà sur la page, il renvoie `false`. Cet élément de données est utile pour exécuter le code exactement une fois sur une page.

L’élément de données `p_fo` utilise les arguments suivants :

* `on` (obligatoire, chaîne) : nom de l’objet JavaScript créé par l’élément de données si l’objet n’existe pas encore sur la page.

Si l’objet n’existe pas encore, cette méthode renvoie `true` et crée l’objet . Si l’objet existe déjà, cette méthode renvoie la valeur `false`.
