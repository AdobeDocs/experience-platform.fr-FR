---
title: Notes de mise à jour du SDK web d’Adobe Experience Platform
description: Notes de mise à jour les plus récentes pour le SDK web d’Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Experience Platform Web SDK;Web SDK;notes de mise à jour;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 466938163cc4f453c40da3709f556a53be334728
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 64%

---


# Notes de mise à jour de Web SDK

Ce document présente les notes de mise à jour du SDK web d’Adobe Experience Platform.
Pour obtenir les dernières notes de mise à jour sur l’extension de balise du SDK web, reportez-vous à la section [Notes de mise à jour de l’extension de balise du SDK web](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Version 2.30.0 - jeudi 24 septembre 2025

**Nouvelles fonctionnalités**

- Ajout de la prise en charge de l’affichage des notifications push.

## Version 2.29.0 - vendredi 4 septembre 2025

**Nouvelles fonctionnalités**

- Ajout de la prise en charge de la collecte de données Adobe Advertisement pour Adobe Parcours Analytics
- Ajout de la prise en charge de l’enregistrement des détails d’abonnement push dans les profils des utilisateurs.

**Correctifs et améliorations**

- Correction d’un problème où les sections de remplacement de configuration étaient fusionnées au lieu d’être remplacées.
- Correction d’un cas où la collection de liens envoyait l’intégralité du contenu du document en tant que nom du lien.
- Correction d’un problème en raison duquel certaines propositions ne pouvaient pas être rendues de nouveau.

## Version 2.28.1 - vendredi 31 juillet 2025

**Correctifs et améliorations**

- Correction d’un problème qui empêchait l’exécution des versions personnalisées.

## Version 2.28.0 - vendredi 24 juillet 2025

**Nouvelles fonctionnalités**

- Ajout de la prise en charge des règles de disqualification de Adobe Journey Optimizer.

**Correctifs et améliorations**

- Correction d’une erreur dans le [dispositif de suivi Media Analytics](commands/getmediaanalyticstracker.md) en raison de laquelle la propriété `length` de l’objet média acceptait incorrectement des types de données non valides.
- Amélioration de la [gestion des identités](identity/overview.md) de la gestion des erreurs pour traiter correctement les rejets de promesses en cas d’échec de la recherche d’identité.
- Correction d’un problème où le rendu du [contenu de personnalisation](personalization/rendering-personalization-content.md) avec des éléments de contenu HTML échouait avec une erreur liée à un `renderStatusHandler` manquant.
- Correction d’une Activity Map [collection d’URL](commands/configure/clickcollectionenabled.md) pour gérer correctement les URL non HTTP.

**Problèmes connus**

- Le processus [build personnalisée](/help/web-sdk/install/create-custom-build.md) utilisant `npx @adobe/alloy` ne fonctionne actuellement pas comme prévu dans la version 2.28.0. Tous les composants sont inclus dans la version générée, quels que soient les modules sélectionnés. Ce problème n’affecte pas le fichier JavaScript standard disponible sur le réseau CDN. Correction en cours.

## Version 2.27.0 - mercredi 20 mai 2025

**Correctifs et améliorations**

- Correction d’un problème lié aux messages in-app en raison duquel le style personnalisé n’était pas correctement appliqué.
- Modification du format de l’historique des événements. Cela entraîne la réaffichage des messages in-app et des cartes de contenu lorsque les anciennes données d’historique sont supprimées.
- Correction d’un problème où les propositions étaient réappliquées dans les cas d’utilisation de SPA.
- Correction d’un problème lié au suivi des clics sur les éléments DOM fantômes.

## Version 2.26.0 - jeudi 5 mars 2025

**Nouvelles fonctionnalités**

- Vous pouvez désormais utiliser le package NPM Web SDK pour créer des versions SDK Web personnalisées et sélectionner uniquement les composants de bibliothèque dont vous avez besoin. Cela permet de réduire la taille de la bibliothèque et d’optimiser les temps de chargement. Consultez la documentation sur la [création d’une version de Web SDK personnalisée à l’aide du package NPM](install/create-custom-build.md).
- La commande [`getIdentity`](commands/getidentity.md) lit désormais automatiquement l’ECID directement à partir du cookie d’identité `kndctr`. Si vous appelez `getIdentity` avec l’espace de noms `ECID` et qu’il existe déjà un cookie d’identité, Web SDK n’effectue plus de requête à Edge Network pour obtenir l’identité. Il lit désormais l’identité à partir du cookie.

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les commandes `getIdentity` ne renvoyaient pas l’identité après l’envoi d’un appel `collect`.
- Correction d’un problème en raison duquel les redirections de personnalisation provoquaient le scintillement du contenu avant la redirection.

## Version 2.25.0 - vendredi 23 janvier 2025

**Correction et améliorations**

- Ajout de la validation des options à la commande `setDebug`.
- Ajout d’un avertissement lors de la configuration d’une fonction `onBeforeLinkClickSend` ou d’un qualificateur de lien de téléchargement lorsque la collecte de clics est désactivée.
- Correction d’un problème où les propositions rendues n’étaient pas incluses dans les notifications d’affichage.

**Nouvelles fonctionnalités**

- Mise en œuvre d’un système de secours pour le domaine Edge configuré lorsque les cookies tiers sont activés et que les requêtes vers adobedc.demdex.net sont bloquées.

## Version 2.24.1 - samedi 6 décembre 2024

**Correction et améliorations**

- Correction d’un problème de dépendance lié au moteur de règles [Adobe Experience Platform](https://github.com/adobe/aepsdk-rulesengine-typescript/), qui provoquait des erreurs dans certaines intégrations client. Web SDK nécessite désormais [Adobe Experience Platform Rules Engine](https://github.com/adobe/aepsdk-rulesengine-typescript/) version 2.0.3 ou ultérieure.

## Version 2.24.0 - vendredi 31 octobre 2024

**Nouvelles fonctionnalités**

- Les [remplacements de flux de données](../datastreams/overrides.md) sont désormais pris en charge au démarrage des sessions multimédia.

- Ajout de la prise en charge des jetons de réponse Adobe Target dans le hook de surveillance [`onContentRendering`](monitoring-hooks.md#onContentRendering).

**Correctifs et améliorations**

- Lorsque plusieurs messages in-app sont renvoyés, seul celui dont la priorité est la plus élevée s’affiche. Les autres sont enregistrés comme supprimés.
- Les remplacements de trains de données vides ne sont plus envoyés à Edge Network, ce qui réduit les conflits potentiels avec les configurations de routage côté serveur.
- Les noms des composants de messages de journalisation suivants ont été renommés pour s’aligner sur les autres SDK Adobe :
   - `DecisioningEngine` a été renommé `RulesEngine`
   - `LegacyMediaAnalytics` a été renommé `MediaAnalyticsBridge`
   - `Privacy` a été renommé `Consent`
- Correction d’une erreur qui se produisait lorsque les éléments de contenu par défaut étaient rendus via [`applyPropositions`](../web-sdk/commands/applypropositions.md).
- Correction d’une erreur CSS dans les actions de déplacement et de redimensionnement d’Adobe Target.
- Suppression de la clé `machineLearning` des réponses [`sendEvent`](../web-sdk/commands/sendevent/overview.md).

## Version 2.23.0 - vendredi 19 septembre 2024

**Nouvelles fonctionnalités**

- Ajout de la prise en charge de la demande de l’[CORE ID](identity/overview.md#tracking-coreid-web-sdk) dans la commande [getIdentity](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library).

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les cookies n’étaient pas correctement écrits lors de l’exécution locale du SDK web.

## Version 2.22.0 - vendredi 22 août 2024

**Nouvelles fonctionnalités**

- Ajout de la prise en charge des points d’extension de surveillance de la personnalisation.

**Correctifs et améliorations**

- Suppression de la prise en charge d’Internet Explorer, réduisant la taille d’espace mémoire de la bibliothèque de 9 %.
- Correction d’un problème où les détails des liens d’Activity Map n’étaient pas initialisés lorsque le hook de moniteur `onInstanceConfigured` était appelé.
- Correction d’un problème en raison duquel les destinations de cookies n’étaient pas définies sur le bon chemin d’accès.
- Correction d’un problème client lié à l’appel à .
- Correction d’un problème en raison duquel un codage d’URL non valide dans le paramètre `adobe_mc` entraînait l’échec des appels [sendEvent](commands/sendevent/overview.md).

## Version 2.21.1 - vendredi 18 juillet 2024

**Correctifs et améliorations**

- Correction d’une erreur de build lors de l’utilisation de la bibliothèque NPM.

## Version 2.21.0 - mercredi 16 juillet 2024

**Nouvelles fonctionnalités**

- Ajout de la prise en charge du suivi automatique des interactions de propositions.
- Ajout d’un script de build personnalisé qui fournit un fichier alloy.js.
- Amélioration de la collecte de clics avec la prise en charge d’Activity Map et du regroupement d’événements.

## Version 2.20.0 - mercredi 21 mai 2024

**Nouvelles fonctionnalités**

- Ajout de la prise en charge de [Streaming Media Collection](../web-sdk/commands/configure/streamingmedia.md).

**Correctifs et améliorations**

- Correction d’un bug en raison duquel le contenu par défaut était masqué par le fragment de code de masquage préalable lorsque le consentement était refusé.

## Version 2.19.2 - 10 janvier 2024

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les erreurs d’identité masquaient d’autres erreurs et transformaient les erreurs d’identité en avertissements.
- Correction d’un problème en raison duquel les appels du bas de la page n’étaient jamais envoyés lorsqu’il existait un appel du haut de la page avec `renderDecisions` défini sur `false`.
- Correction d’un problème en raison duquel Web SDK ne pouvait pas lire les identités interdomaines lorsqu’il existait plusieurs paramètres de chaîne de requête `adobe_mc`.

## Version 2.19.1 - 10 novembre 2023

**Correctifs et améliorations**

- Correction d’un problème en raison duquel le tableau de propositions renvoyé depuis les appels `sendEvent` était toujours vide.

## Version 2.19.0 - 1 novembre 2023

**Nouvelles fonctionnalités**

- Ajout de la prise en charge du rendu des messages in-app d’Adobe Journey Optimizer.
- Ajout de la prise en charge des [événements haut et bas de page](use-cases/top-bottom-page-events.md).
- Ajout de [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) option à la commande `sendEvent` pour contrôler la demande de portée dans toute la page et de surface par défaut.

**Correctifs et améliorations**

- Combinaison d’événements d’affichage de personnalisation lors du rendu de plusieurs types de personnalisation.
- Correction d’un problème où les noms des vues d’application d’une seule page étaient sensibles à la casse.
- Correction d’un problème lié aux sélecteurs d’offres personnalisés DOM fantômes.

## Version 2.18.0 - 31 juillet 2023

**Nouvelles fonctionnalités**

- Ajout de la prise en charge des [remplacements par commande de l’identifiant de train de données](../datastreams/overrides.md).

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les liens de sortie ne remplissaient pas les critères du fait que le domaine faisait partie de la requête.
- `edgeConfigId` est devenu obsolète et est remplacé par `datastreamId` dans la configuration du SDK Web.

## Version 2.17.0 - 17 mai 2023

**Correctifs et améliorations**

- Le SDK Web code désormais les valeurs de destination des cookies d’Audience Manager, à l’instar de [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=fr).

## Version 2.16.0 - 25 avril 2023

**Nouvelles fonctionnalités**

- Ajout de la prise en charge des [remplacements de la configuration du train de données](../datastreams/overrides.md).

## Version 2.15.0 - 30 mars 2023

**Nouvelles fonctionnalités**

- Ajout de la prise en charge du rappel de clic sur les liens [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).
- Ajout de la prise en charge du suivi des clics par Adobe Journey Optimizer.

**Correctifs et améliorations**

- La collecte de liens recueille désormais le nom du lien et le pays du visiteur.
- Suppression de l’erreur de console pour les destinations d’URL ayant échoué.

## Version 2.14.0 - 25 janvier 2023

- (Beta) Ajout de la prise en charge des surfaces et propositions d’Adobe Journey Optimizer.

**Correctifs et améliorations**

- Correction d’un problème lié aux actions de code personnalisé du VEC d’Adobe Target en raison duquel le code était injecté dans un autre emplacement qu’avec [!DNL at.js].
- Correction d’un problème en raison duquel l’en-tête « référent » n’était pas correctement défini sur les requêtes envoyées au réseau Edge.
- Correction d’un problème en raison duquel les propriétés de l’[indicateur client de l’agent utilisateur](/help/web-sdk/use-cases/client-hints.md) pouvaient être définies sur un type incorrect.
- Correction d’un problème en raison duquel `placeContext.localTime` ne correspondait pas au schéma.

## Version 2.13.1 - 13 octobre 2022

- Correction d’un problème en raison duquel la migration des visiteurs et visiteuses ne fonctionnait pas si « window.Visitor » était défini après la configuration. Ce problème se pose en particulier lors de l’utilisation des balises Adobe.
- Correction d’un problème en raison duquel `device.screenWidth` et `device.screenHeight` étaient renseignées comme des chaînes dans certains environnements.

## Version 2.13.0 - 28 septembre 2022

**Nouvelles fonctionnalités**

- Ajout de la prise en charge de la [Migration complète page par page](home.md#migrating-to-web-sdk). Le profil Adobe Target est désormais conservé lorsqu’un visiteur ou un visiteuse passe d’une page at.js à une page SDK web.
- Ajout de la prise en charge configurable des [Indicateurs clients d’agent utilisateur à forte entropie](/help/web-sdk/use-cases/client-hints.md).
- Ajout de la prise en charge de la commande [`applyResponse`](/help/web-sdk/commands/applyresponse.md) . Cela permet une personnalisation hybride via l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/).
- Les liens du mode QA fonctionnent désormais sur plusieurs pages.

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les mesures de suivi des clics de personnalisation n’étaient pas mises à jour lorsque le suivi des liens était désactivé.
- Mise à jour des commandes afin de générer une erreur de validation lorsque des options inconnues sont spécifiées.
- La propriété `_experience.decisioning.propositionEventType` est désormais renseignée lors de l’envoi automatique d’événements de personnalisation d’affichage et d’interaction.
- Ajout de la validation des espaces de noms dupliqués pour la commande `getIdentity`.
- Ajout de la validation de la portée de décision dupliquée pour la commande `sendEvent`.

## Version 2.12.0 - 29 juin 2022

- Modification des requêtes sur le réseau Edge afin d’utiliser l’indicateur d’emplacement du cookie `cluster` dans le champ de l’URL. Cela permet de s’assurer que les utilisateurs et utilisatrices qui changent leur position (par exemple, via un VPN ou qui conduisent avec des appareils mobiles, etc.) en milieu de session atteignent le même niveau Edge et disposent du même profil de personnalisation.
- Fonctions configurées avec Stringify dans la réponse de commande getLibraryInfo.

## Version 2.11.0 - 13 juin 2022

**Nouvelles fonctionnalités**

- Vous pouvez désormais diffuser des expériences personnalisées plus précisément, en partageant les identifiants de visiteurs et visiteuses entre les applications mobiles et le contenu web mobile, ainsi qu’entre les domaines. Consultez la [documentation dédiée](identity/id-sharing.md) pour en savoir plus.
- Vous pouvez désormais rendre ou exécuter un tableau de propositions à partir de [!DNL Adobe Target] dans des applications monopages, sans incrémenter les mesures d’analyse. Cela réduit les erreurs de création de rapports et augmente la précision des analyses. Consultez la [documentation dédiée](personalization/rendering-personalization-content.md#applypropositions) pour en savoir plus.
- Ajout d’informations supplémentaires à la commande `getLibraryInfo`, y compris les commandes disponibles et la configuration finale de l’instance.

**Correctifs et améliorations**

- Mise à jour des paramètres des cookies pour utiliser `sameSite="none"` et l’indicateur `secure` sur les pages [!DNL HTTPS].
- Correction d’un problème où le contenu personnalisé n’était pas correctement appliqué lors de l’utilisation du pseudo sélecteur `eq`.
- Correction d’un problème où `localTimezoneOffset` pouvait échouer lors de la validation d’Experience Platform.

## Version 2.10.1 - 3 mai 2022

- Correction d’un problème où plusieurs éléments iframes persistants étaient créée pour les synchronisations des identifiants et les destinations de segment.

## Version 2.10.0 - 22 avril 2022

- Utilisez un élément iframe persistant pour toutes les synchronisations des identifiants et destinations de segment.
- Correction d’un problème où les propositions de mesures fusionnées étaient dupliquées dans le résultat `sendEvent`.

## Version 2.9.0 - 10 mars 2022

- Ajout de la prise en charge du suivi des expériences Adobe Target [!DNL control (default)].
- Optimisation des événements de modification de la vue pour les applications monopages. La notification d’affichage est désormais incluse avec l’événement de modification de la vue lors du rendu d’expériences personnalisées.
- Suppression de l’avertissement de la console en cas d’absence de `eventType`.
- Correction d’un problème où la propriété `propositions` n’était renvoyée que par une commande `sendEvent` lorsque des expériences étaient demandées ou récupérées à partir du cache. La propriété `propositions` sera désormais toujours définie comme un tableau.
- Correction d’un problème en raison duquel les conteneurs masqués n’étaient pas affichés lorsqu’une erreur était renvoyée depuis Edge Network.
- Correction d’un problème où les événements d’interaction n’étaient pas comptabilisés dans Adobe Target. Ce problème a été corrigé en ajoutant le nom de la vue au fichier XDM sur web.webPageDetails.viewName.
- Correction des liens rompus de la documentation dans les messages de la console.

## Version 2.8.0, - 19 janvier 2022

- Prise en charge des sélecteurs DOM fantômes pour la personnalisation.
- Types d’événements de personnalisation renommés. (`display` et `click` deviennent `decisioning.propositionDisplay` et `decisioning.propositionInteract`.)
- Correction d’un problème où les offres HTML avec des balises de script intégrées ajoutaient deux fois les balises de script à la page même si le script n’était exécuté qu’une seule fois.

## Version 2.7.0 - 26 octobre 2021

- Exposition d’informations supplémentaires d’Edge Network dans la valeur renvoyée de `sendEvent`, y compris `inferences` et `destinations`. Le format de ces propriétés peut changer, car ces fonctionnalités sont actuellement déployées dans le cadre d’une version Beta.

## Version 2.6.4 - 7 septembre 2021

- Correction d’un problème où les actions HTML définies d’Adobe Target appliquées à l’élément `head` remplaçaient l’intégralité du contenu `head`. Les actions HTML définies appliquées à l’élément `head` sont désormais modifiées pour ajouter un HTML.

## Version 2.6.3 - 16 août 2021

- Correction d’un problème où les objets non destinés à un usage public étaient exposés via la promesse résolue de la commande `configure`.

## Version 2.6.2 - 4 août 2021

- Correction d’un problème où un avertissement d’obsolescence de `result.decisions` (fourni par la commande `sendEvent`) était consigné dans la console même lorsque la propriété `result.decisions` n’était pas utilisée. Aucun avertissement ne sera consigné lors de l’accès à la propriété `result.decisions`, mais la propriété est toujours obsolète.

## Version 2.6.1 - 29 juillet 2021

- Correction d’un problème où le rendu de la personnalisation pour une vue d’application monopage sans contenu de personnalisation générait une erreur et provoquait le rejet de la promesse renvoyée par la commande `sendEvent`.

## Version 2.6.0 - 27 juillet 2021

- Fournit davantage de contenu de personnalisation dans la promesse résolue `sendEvent`, y compris les jetons de réponse Adobe Target. Lorsque la commande `sendEvent` est exécutée, une promesse est renvoyée, qui est finalement résolue avec un objet `result` contenant les informations reçues du serveur. Auparavant, cet objet de résultat incluait une propriété nommée `decisions`. Cette propriété `decisions` a été rendue obsolète. Une nouvelle propriété, `propositions`, a été ajoutée. Cette nouvelle propriété permet aux clientes et clients d’accéder à davantage de contenu de personnalisation, notamment des [jetons de réponse](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Version 2.5.0 - Juin 2021

- Ajout de la prise en charge des offres de personnalisation de redirection.
- Les largeurs et hauteurs de fenêtre d’affichage collectées automatiquement et qui sont des valeurs négatives ne seront plus envoyées au serveur.
- Lorsqu’un événement est annulé en renvoyant `false` d’un rappel `onBeforeEventSend`, un message est désormais consigné.
- Correction d’un problème où des éléments spécifiques de données XDM destinés à un seul événement étaient inclus dans plusieurs événements.

## Version 2.4.0 - Mars 2021

- Le SDK peut désormais être installé en tant que package [NPM](/help/web-sdk/install/npm.md).
- Ajout de la prise en charge d’une option `out` lors de la [configuration du consentement par défaut](/help/web-sdk/commands/configure/defaultconsent.md), qui ignore tous les événements jusqu’à ce que le consentement soit reçu (l’option `pending` existante met les événements en file d’attente et les envoie une fois le consentement reçu).
- Le rappel [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) peut désormais être utilisé pour empêcher l’envoi d’un événement.
- Utilise désormais un groupe de champs de schéma XDM au lieu de `meta.personalization` lors de l’envoi d’événements au sujet du contenu personnalisé rendu ou sur lequel l’utilisateur ou l’utilisatrice a cliqué.
- La commande [`getIdentity`](/help/web-sdk/commands/getidentity.md) renvoie désormais l’identifiant de zone géographique Edge ainsi que l’identité.
- Amélioration et gestion plus efficace des avertissements et des erreurs reçus du serveur.
- Ajout de la prise en charge de la norme de consentement 2.0 d’Adobe pour la commande [`setConsent`](/help/web-sdk/commands/setconsent.md).
- Une fois reçues, les préférences de consentement sont hachées et stockées dans un espace de stockage local afin d’optimiser l’intégration entre les CMP, Experience Platform Web SDK et Experience Platform Edge Network. Si vous collectez des préférences de consentement, nous vous recommandons d’appeler `setConsent` à chaque chargement de page.
- Ajout des deux [hooks de surveillance](https://github.com/adobe/alloy/wiki/Monitoring-Hooks) suivants : `onCommandResolved` et `onCommandRejected`.
- Correction de bug : les événements de notification d’interaction de personnalisation contenaient des informations en double sur la même activité lorsqu’un utilisateur ou une utilisatrice accédait à une nouvelle vue d’application monopage, revenait à la vue d’origine, puis cliquait sur un élément éligible à la conversion.
- Correction de bug : si le paramètre `documentUnloading` du premier événement envoyé par le SDK était défini sur `true`, l’utilisation de [`sendBeacon`](https://developer.mozilla.org/fr-FR/docs/Web/API/Navigator/sendBeacon) pour envoyer l’événement entraînait une erreur, car l’identité n’était pas connue.

## Version 2.3.0 - Novembre 2020

- Ajout de la prise en charge de la valeur à usage unique afin de permettre des stratégies de sécurité du contenu plus strictes.
- Ajout de la prise en charge de la personnalisation pour les applications monopages.
- Amélioration de la compatibilité avec d’autres codes JavaScript sur la page qui peuvent remplacer les API `window.console`.
- Correction de bug : `sendBeacon` n’était pas utilisé lorsque `documentUnloading` était défini sur `true` ou lorsque les clics sur les liens étaient automatiquement suivis.
- Correction de bug : le lien n’était pas automatiquement suivi si l’élément d’ancrage contenait du contenu HTML.
- Correction de bug : certaines erreurs de navigateur contenant une propriété `message` en lecture seule n’étaient pas traitées de manière appropriée, ce qui entraînait l’affichage d’une erreur différente au client ou à la cliente.
- Correction de bug : l’exécution du SDK dans un élément iframe entraînait une erreur si la page HTML de l’élément iframe provenait d’un sous-domaine différent de celui de la page HTML de la fenêtre parente.

## Version 2.2.0 - Octobre 2020

- Correction de bug : l’objet Opt-in empêchait Web SDK d’effectuer des appels lorsque `idMigrationEnabled` était `true`.
- Correction de bug : sensibilisation de Web SDK aux requêtes qui doivent renvoyer des offres de personnalisation afin d’éviter tout problème de scintillement.

## Version 2.1.0 - Août 2020

- Suppression de la commande `syncIdentity` et prise en charge de la transmission de ces identifiants dans la commande `sendEvent`.
- Prise en charge de la norme de consentement IAB 2.0.
- Prise en charge de la transmission d’identifiants supplémentaires dans la commande `setConsent`.
- Prise en charge du remplacement de l’`datasetId` dans la commande `sendEvent`.
- Prise en charge des hooks de surveillance ([En savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- Transmission de `environment: browser` dans les données contextuelles des détails d’implémentation.
