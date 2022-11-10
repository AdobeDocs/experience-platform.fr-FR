---
title: Test d’une mise en oeuvre Adobe Target avec Adobe Experience Platform Debugger
description: Découvrez comment utiliser Adobe Experience Platform Debugger pour tester et déboguer un site web activé avec Adobe Target.
source-git-commit: 1ce7ac78936040d76faa3a58b92333a737fbeb66
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 6%

---

# Test d’une mise en oeuvre Adobe Target avec Adobe Experience Platform Debugger

Adobe Experience Platform Debugger fournit une suite d’outils utiles pour tester et déboguer un site web qui a été piloté avec une implémentation Adobe Target. Ce guide couvre certains workflows courants et les bonnes pratiques pour utiliser Platform Debugger sur un site web compatible avec Target.

## Conditions préalables

Pour utiliser Platform Debugger pour Target, le site web doit utiliser la variable [Bibliothèque at.js](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) version 1.x ou ultérieure. Les versions précédentes ne sont pas prises en charge.

## Initialisation de Platform Debugger

Ouvrez le site web que vous souhaitez tester dans un navigateur, puis ouvrez l’extension Platform Debugger.

Sélectionnez **[!DNL Target]** dans le volet de navigation de gauche. Si Platform Debugger détecte qu’une version compatible d’at.js s’exécute sur le site, les détails de mise en oeuvre d’Adobe Target s’affichent.

![La vue Target sélectionnée dans Platform Debugger, indiquant qu’Adobe Target est principale sur la page de navigateur actuellement consultée.](../images/solutions/target/target-initialized.png)

## Informations de configuration globales

Les informations sur la configuration globale de la mise en oeuvre sont affichées en haut de la vue Target dans le débogueur Platform.

![Informations de configuration globales pour Target mises en évidence dans Platform Debugger](../images/solutions/target/global-config.png)

| Nom | Description |
| --- | --- |
| Code client | Identifiant unique qui identifie votre organisation. |
| Version | Version de la bibliothèque Adobe Target actuellement installée sur le site web. |
| Nom global de la demande | Nom de la variable [mbox globale](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) pour l’implémentation de Target, le nom par défaut étant `target-global-mbox`. |
| Événement de chargement de page | Une valeur booléenne indiquant si une [événement de chargement de page](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) a eu lieu. Les événements de chargement de page ne sont pris en charge que pour at.js 2.x. Pour les versions non compatibles, cette valeur est définie par défaut sur `None`. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Network Requests] {#network}

Sélectionner **[!DNL Network Requests]** pour afficher des informations récapitulatives sur chaque requête réseau effectuée sur la page.

![Le [!DNL Network Requests] section pour Target sélectionnée dans Platform Debugger](../images/solutions/target/network-requests.png)

Lorsque vous effectuez des actions sur la page (notamment lors du rechargement de la page), de nouvelles colonnes sont automatiquement ajoutées au tableau, ce qui vous permet de visualiser l’ordre des actions et la manière dont les valeurs sont modifiées entre chaque requête.

![Le [!DNL Network Requests] section pour Target sélectionnée dans Platform Debugger](../images/solutions/target/new-request.png)

Les valeurs suivantes sont capturées :

| Nom | Description |
| --- | --- |
| [!DNL Page Title] | Titre de la page qui a initié cette requête. |
| [!DNL Page URL] | URL de la page qui a initié la requête. |
| [!DNL URL] | URL brute de la requête. |
| [!DNL Method] | Méthode HTTP de la requête. |
| [!DNL Query String] | Chaîne de requête de la requête, extraite de l’URL. |
| [!DNL POST Body] | Corps de la requête (défini uniquement pour les requêtes de POST). |
| [!DNL Pathname] | Chemin d’accès de l’URL de requête. |
| [!DNL Hostname] | Nom d’hôte de l’URL de demande. |
| [!DNL Domain] | Domaine de l’URL de demande. |
| [!DNL Timestamp] | Horodatage du moment où la demande (ou l’événement) a eu lieu, dans le fuseau horaire du navigateur. |
| [!DNL Time Since Page Load] | Temps écoulé depuis le chargement initial de la page au moment de la requête. |
| [!DNL Initiator] | Initiateur de la requête. En d&#39;autres termes, qui a fait la demande ? |
| [!DNL clientCode] | Identifiant du compte de votre organisation, tel qu’il est reconnu par Target. |
| [!DNL requestType] | API utilisée pour la requête. Si vous utilisez at.js 1.x, la valeur est `/json`. Si vous utilisez at.js 2.x, la valeur est `delivery`. |
| [!DNL Audience Manager Blob] | Fournit des informations sur les métadonnées d’Audience Manager chiffrées appelées &quot;blob&quot;. |
| [!DNL Audience Location Hint] | ID de la région de collecte de données. Il s’agit d’un identifiant numérique pour l’emplacement géographique d’un centre de données de service d’ID en particulier. Pour plus d’informations, voir la documentation sur l’Audience Manager sur [Identifiants de zone géographique, emplacements et noms d’hôte du serveur de collecte de données](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=fr) et le guide Experience Cloud Identity Service sur [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | Hauteur du navigateur en pixels. |
| [!DNL Browser Time Offset] | Décalage horaire du navigateur associé à son fuseau horaire. |
| [!DNL Browser Width] | Largeur du navigateur en pixels. |
| [!DNL Color Depth] | Profondeur de couleur de l’écran. |
| [!DNL context] | Objet contenant des informations contextuelles sur le navigateur utilisé pour effectuer la requête, notamment les dimensions d’écran et la plateforme client. |
| [!DNL prefetch] | Les paramètres utilisés dans pendant la `prefetch` traitement. |
| [!DNL execute] | Les paramètres utilisés pendant `execute` traitement. |
| [!DNL Experience Cloud Visitor ID] | Si l’un d’eux est détecté, fournit des informations sur la variable [Identifiant Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) attribué au visiteur du site actuel. |
| [!DNL experienceCloud] | Contient les identifiants Experience Cloud pour cette session d’utilisateur spécifique : A4T [ID de données supplémentaire](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A), et a [identifiant visiteur (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | Le [ID cible](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) pour le visiteur. |
| [!DNL Mbox Host] | Le [hôte](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=fr) à laquelle la requête Target a été envoyée. |
| [!DNL Mbox PC] | Chaîne qui encapsule la variable [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) ID de session et [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) indicateur d’emplacement. Cette valeur est utilisée par at.js pour s’assurer que la session et l’emplacement Edge restent attrayants. |
| [!DNL Mbox Referrer] | Référent URL pour le [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) requête. |
| [!DNL Mbox URL] | L’URL de la variable [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) serveur. |
| [!DNL Mbox Version] | La version de [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) en cours d’utilisation. |
| [!DNL mbox3rdPartyId] | Le [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) affectée au visiteur actif. |
| [!DNL mboxRid] | Le [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) ID de requête. |
| [!DNL requestId] | Identifiant unique de la requête. |
| [!DNL Screen Height] | Hauteur de l’écran en pixels. |
| [!DNL Screen Width] | Largeur de l’écran en pixels. |
| [!DNL Supplemental Data ID] | Identifiant généré par le système utilisé pour faire correspondre les visiteurs aux appels Adobe Target et Adobe Analytics correspondants. Voir [Guide de dépannage d’A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) pour plus d’informations. |
| [!DNL vst] | Le [Configuration de l’API du service d’identité Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | Fournit des informations sur le moteur de rendu WebGL utilisé sur la page, le cas échéant. |

{style=&quot;table-layout:auto&quot;}

Pour afficher les détails d’un paramètre sur un événement réseau particulier, sélectionnez la cellule de tableau en question. Une fenêtre contextuelle s’affiche, fournissant des informations supplémentaires sur le paramètre, y compris une description et sa valeur. Si la valeur est un objet JSON, la boîte de dialogue comprend une vue entièrement navigable de la structure de l’objet.

![Le [!DNL Network Requests] section pour Target sélectionnée dans Platform Debugger](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Sélectionner **[!DNL Configuration]** pour activer ou désactiver une sélection d’outils de débogage supplémentaires pour Target.

![Le [!DNL Configuration Requests] section pour Target sélectionnée dans Platform Debugger](../images/solutions/target/configuration.png)

| Outil de débogage | Description |
| --- | --- |
| [!DNL Target Console Logging] | Lorsque cette option est activée, vous permet d’accéder aux journaux at.js dans l’onglet de la console du navigateur. Cette fonction peut également être activée en ajoutant une `mboxDebug` paramètre de requête (avec toute valeur) à l’URL du navigateur. |
| [!DNL Target Diable] | Lorsque cette option est activée, toutes les fonctionnalités de Target sont désactivées sur la page. Vous pouvez l’utiliser pour déterminer si une offre spécifique à Target est à l’origine du problème sur la page. |
| [!DNL Target Trace] | **Remarque**: Vous devez être connecté pour activer cette fonctionnalité.<br><br>Une fois activés, les jetons de suivi sont envoyés avec chaque requête et un objet trace est renvoyé dans chaque réponse. `at.js` analyse la réponse `window.__targetTraces`. Chaque objet trace contient les mêmes informations que le [[!DNL Network Requests] , avec les ajouts suivants :<ul><li>Un instantané de profil, qui vous permet d’afficher les attributs avant et après les requêtes.</li><li>Correspondance et sans correspondance [activités](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), indiquant pourquoi le profil actuel a été admissible ou non pour des activités spécifiques.<ul><li>Cela peut aider à identifier les audiences auxquelles un profil se qualifie à un moment donné et pourquoi.</li><li>La documentation de Target contient plus d’informations sur les différents types d’activité.</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
