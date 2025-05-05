---
title: Tester une mise en œuvre Adobe Target avec Adobe Experience Platform Debugger
description: Découvrez comment utiliser Adobe Experience Platform Debugger pour tester et déboguer un site web activé avec Adobe Target.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 84%

---

# Tester une mise en œuvre Adobe Target avec Adobe Experience Platform Debugger

Adobe Experience Platform Debugger fournit une suite d’outils utiles pour tester et déboguer un site web qui a été piloté avec une mise en œuvre Adobe Target. Ce guide couvre certains workflows et bonnes pratiques courants pour utiliser Experience Platform Debugger sur un site web activé avec Target.

## Conditions préalables

Pour utiliser Experience Platform Debugger pour Target, le site web doit utiliser la version 1.x ou ultérieure de la bibliothèque [at.js](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/). Les versions précédentes ne sont pas prises en charge.

## Initialisation d’Experience Platform Debugger

Ouvrez le site web que vous souhaitez tester dans un navigateur, puis ouvrez l’extension Experience Platform Debugger.

Sélectionnez **[!DNL Target]** dans le volet de navigation de gauche. Si Experience Platform Debugger détecte qu’une version compatible d’at.js s’exécute sur le site, les détails de mise en œuvre d’Adobe Target s’affichent.

![Vue Target sélectionnée dans Experience Platform Debugger, indiquant qu’Adobe Target est actif sur la page de navigateur actuellement consultée](../images/solutions/target/target-initialized.png)

## Informations sur la configuration globale

Les informations sur la configuration globale de la mise en œuvre sont affichées en haut de la vue Target dans Experience Platform Debugger.

![Informations sur la configuration globale pour Target mises en évidence dans Experience Platform Debugger](../images/solutions/target/global-config.png)

| Nom | Description |
| --- | --- |
| Code client | Identifiant unique qui identifie votre organisation. |
| Version | Version de la bibliothèque Adobe Target actuellement installée sur le site web. |
| Nom global de la demande | Nom de la [mbox globale](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) pour la mise en œuvre de Target, le nom par défaut étant `target-global-mbox`. |
| Événement de chargement de page | Valeur booléenne indiquant si un [événement de chargement de page](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) a eu lieu. Les événements de chargement de page ne sont pris en charge que pour at.js 2.x. Pour les versions non compatibles, cette valeur est définie par défaut sur `None`. |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

Sélectionnez **[!DNL Network Requests]** pour afficher un résumé des informations sur chaque requête réseau effectuée sur la page.

![Section [!DNL Network Requests] pour Target sélectionnée dans Experience Platform Debugger](../images/solutions/target/network-requests.png)

Lorsque vous effectuez des actions sur la page (notamment lors du rechargement de la page), de nouvelles colonnes sont automatiquement ajoutées au tableau, ce qui vous permet de visualiser l’ordre des actions et la manière dont les valeurs sont modifiées entre chaque requête.

![Section [!DNL Network Requests] pour Target sélectionnée dans Experience Platform Debugger](../images/solutions/target/new-request.png)

Les valeurs suivantes sont capturées :

| Nom | Description |
| --- | --- |
| [!DNL Page Title] | Titre de la page qui a initié cette requête. |
| [!DNL Page URL] | URL de la page qui a initié la requête. |
| [!DNL URL] | URL brute de la requête. |
| [!DNL Method] | Méthode HTTP de la requête. |
| [!DNL Query String] | Chaîne de requête de la requête, extraite de l’URL. |
| [!DNL POST Body] | Corps de la requête (défini uniquement pour les requêtes POST). |
| [!DNL Pathname] | Chemin d’accès de l’URL de la requête. |
| [!DNL Hostname] | Nom d’hôte de l’URL de la requête. |
| [!DNL Domain] | Domaine de l’URL de la requête. |
| [!DNL Timestamp] | Date et heure du moment où la demande (ou l’événement) a eu lieu, dans le fuseau horaire du navigateur. |
| [!DNL Time Since Page Load] | Temps écoulé depuis le chargement initial de la page au moment de la requête. |
| [!DNL Initiator] | Initiateur de la requête. En d’autres termes, qui a effectué la requête ? |
| [!DNL clientCode] | Identifiant du compte de votre organisation, tel qu’il est reconnu par Target. |
| [!DNL requestType] | API utilisée pour la requête. Si vous utilisez at.js 1.x, la valeur est `/json`. Si vous utilisez at.js 2.x, la valeur est `delivery`. |
| [!DNL Audience Manager Blob] | Fournit des informations sur les métadonnées chiffrées d’Audience Manager appelées « blob ». |
| [!DNL Audience Location Hint] | ID de la région de collecte de données. Il s’agit d’un identifiant numérique pour l’emplacement géographique d’un centre de données de service d’ID spécifique. Pour plus d’informations, voir la documentation sur Audience Manager dans [Identifiants de zone géographique, emplacements et noms d’hôte du serveur de collecte de données](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=fr) et le guide Service d’identités d’Experience Cloud sur [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=fr#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | Hauteur du navigateur en pixels. |
| [!DNL Browser Time Offset] | Décalage horaire du navigateur associé à son fuseau horaire. |
| [!DNL Browser Width] | Largeur du navigateur en pixels. |
| [!DNL Color Depth] | Intensité de couleur de l’écran. |
| [!DNL context] | Objet contenant des informations contextuelles sur le navigateur utilisé pour effectuer la requête, notamment les dimensions d’écran et la plateforme client. |
| [!DNL prefetch] | Paramètres utilisés pendant le traitement `prefetch`. |
| [!DNL execute] | Paramètres utilisés pendant le traitement `execute`. |
| [!DNL Experience Cloud Visitor ID] | Si l’un d’eux est détecté, fournit des informations sur la variable [Identifiant Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr) attribué au visiteur actuel du site. |
| [!DNL experienceCloud] | Contient les identifiants Experience Cloud pour cette session d’utilisateur spécifique : un [identifiant de données supplémentaires](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?lang=fr?#section_2C1F745A2B7D41FE9E30915539226E3A) A4T, et un [identifiant visiteur (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=fr). |
| [!DNL id] | L’[identifiant cible](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) pour le visiteur. |
| [!DNL Mbox Host] | L’[hôte](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=fr) auquel la requête Target a été envoyée. |
| [!DNL Mbox PC] | Chaîne qui encapsule l’identifiant de session [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) et l’indicateur d’emplacement [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=fr#concept_0AE2ED8E9DE64288A8B30FCBF1040934). Cette valeur est utilisée par at.js pour s’assurer que la session et l’emplacement Edge restent visibles. |
| [!DNL Mbox Referrer] | Référent URL pour la requête spécifique [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/). |
| [!DNL Mbox URL] | URL du serveur [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/). |
| [!DNL Mbox Version] | Version de [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) en cours d’utilisation. |
| [!DNL mbox3rdPartyId] | L’[`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=fr) affecté au visiteur actuel. |
| [!DNL mboxRid] | L’identifiant de requête [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/). |
| [!DNL requestId] | Identifiant unique pour la requête. |
| [!DNL Screen Height] | Hauteur de l’écran en pixels. |
| [!DNL Screen Width] | Largeur de l’écran en pixels. |
| [!DNL Supplemental Data ID] | Identifiant généré par le système utilisé pour faire correspondre les visiteurs aux appels Adobe Target et Adobe Analytics correspondants. Voir le [guide de dépannage A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?lang=fr?#section_75002584FA63456D8D9086172925DD8D) pour plus d’informations. |
| [!DNL vst] | La [configuration de l’API Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html?lang=fr). |
| [!DNL webGLRenderer] | Fournit des informations sur le moteur de rendu WebGL utilisé sur la page, le cas échéant. |

{style="table-layout:auto"}

Pour afficher les détails d’un paramètre sur un événement réseau particulier, sélectionnez la cellule de tableau en question. Une fenêtre contextuelle s’affiche, fournissant des informations supplémentaires sur le paramètre, y compris une description et sa valeur. Si la valeur est un objet JSON, la boîte de dialogue comprend une vue entièrement navigable de la structure de l’objet.

![Section [!DNL Network Requests] pour Target sélectionnée dans Experience Platform Debugger](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Sélectionnez **[!DNL Configuration]** pour activer ou désactiver une sélection d’outils de débogage supplémentaires pour Target.

![Section [!DNL Configuration Requests] pour Target sélectionnée dans Experience Platform Debugger](../images/solutions/target/configuration.png)

| Outil de débogage | Description |
| --- | --- |
| [!DNL Target Console Logging] | Lorsque cette option est activée, elle vous permet d’accéder aux journaux at.js dans l’onglet de la console du navigateur. Cette fonction peut également être activée en ajoutant un paramètre de requête `mboxDebug` (avec n’importe quelle valeur) à l’URL du navigateur. |
| [!DNL Target Disable] | Lorsque cette option est activée, toutes les fonctionnalités de Target sont désactivées sur la page. Vous pouvez l’utiliser pour déterminer si une offre spécifique à Target est à l’origine du problème sur la page. |
| [!DNL Target Trace] | **Remarque** : vous devez être connecté(e) pour activer cette fonctionnalité.<br><br>Une fois activés, les jetons de suivi sont envoyés avec chaque requête et un objet de suivi est renvoyé dans chaque réponse. `at.js` analyse la réponse `window.__targetTraces`. Chaque objet de suivi contient les mêmes informations que l’[onglet [!DNL Network Requests]], avec les ajouts suivants :<ul><li>Un instantané de profil, qui vous permet d’afficher les attributs avant et après les requêtes.</li><li>[Activités](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=fr) avec ou sans correspondance, indiquant pourquoi le profil actuel se qualifiait ou non pour des activités spécifiques.<ul><li>Cela peut aider à identifier les audiences pour lesquelles un profil se qualifie à un moment donné et pourquoi.</li><li>La documentation de Target contient plus d’informations sur les différents types d’activité.</li></ul></li></ul> |

{style="table-layout:auto"}
