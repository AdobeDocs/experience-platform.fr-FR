---
title: Notes de mise à jour du SDK web Adobe Experience Platform
description: Notes de mise à jour les plus récentes pour le SDK Web Adobe Experience Platform.
keywords: SDK Web Adobe Experience Platform;SDK Web Platform;SDK Web;notes de mise à jour;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 777a1749670f36abc09e4bacd190b1be17a9a237
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 2%

---


# Notes de mise à jour

Ce document couvre les notes de mise à jour du SDK Web de Adobe Experience Platform.
Pour obtenir les dernières notes de mise à jour sur l’extension de balise du SDK Web, reportez-vous à la section [Notes de mise à jour de l’extension de balise SDK Web](extension/web-sdk-ext-release-notes.md).

## Version 2.13.0 - 28 septembre 2022

**Nouvelles fonctionnalités**

* Ajout de la prise en charge de la migration complète page par page. Le profil Adobe Target est désormais conservé lorsqu’un visiteur passe d’une page at.js à une page SDK Web.
* Ajout de la prise en charge configurable de [Conseils client User-Agent à forte entropie](fundamentals/user-agent-client-hints.md#high-entropy).
* Ajout de la prise en charge de la nouvelle `applyResponse` . Cela permet une personnalisation hybride via le [API du serveur réseau Edge](../server-api/overview.md).
* Les liens du mode AQ fonctionnent désormais sur plusieurs pages.

**Correctifs et améliorations**

* Correction d’un problème en raison duquel les mesures de suivi des clics de personnalisation n’étaient pas mises à jour lorsque le suivi des liens était désactivé.
* Mise à jour des commandes pour générer une erreur de validation lorsque des options inconnues sont spécifiées.
* Le `_experience.decisioning.propositionEventType` est maintenant renseignée lors de l’envoi automatique d’événements d’affichage et de personnalisation d’interaction.
* Ajout de la validation d’espace de noms dupliquée pour le `getIdentity` .
* Ajout de la validation de l’étendue de décision dupliquée pour la variable `sendEvent` .

## Version 2.12.0 - 29 juin 2022

* Modifiez les requêtes sur le réseau Edge pour utiliser la variable `cluster` indicateur d’emplacement du cookie dans le cadre de l’URL. Cela permet de s’assurer que les utilisateurs qui changent de position (par exemple, via un VPN ou qui conduisent avec des périphériques mobiles, etc.) en milieu de session atteignent le même niveau et disposent du même profil de personnalisation.
* Restreindre les fonctions configurées dans la réponse de commande getLibraryInfo .

## Version 2.11.0 - 13 juin 2022

**Nouvelles fonctionnalités**

* Vous pouvez désormais diffuser des expériences personnalisées plus précisément, en partageant les identifiants visiteur entre les applications mobiles et le contenu web mobile, ainsi qu’entre les domaines. Voir [documentation dédiée](identity/id-sharing.md) pour en savoir plus.
* Vous pouvez désormais générer ou exécuter un tableau de propositions à partir de [!DNL Adobe Target] dans des applications d’une seule page, sans incrémenter les mesures d’analyse. Cela réduit les erreurs de création de rapports et augmente la précision des analyses. Voir [documentation dédiée](personalization/rendering-personalization-content.md#applypropositions) pour en savoir plus.
* Ajout d’informations supplémentaires au `getLibraryInfo` , y compris les commandes disponibles et la configuration finale de l&#39;instance.

**Correctifs et améliorations**

* Mise à jour des paramètres de cookie pour utiliser `sameSite="none"` et `secure` indicateur sur [!DNL HTTPS] pages.
* Correction d’un problème en raison duquel le contenu personnalisé n’était pas correctement appliqué lors de l’utilisation de la variable `eq` pseudo-sélecteur.
* Correction d’un problème en raison duquel `localTimezoneOffset` peut échouer lors de la validation de l’Experience Platform.

## Version 2.10.1 - 3 mai 2022

* Correction d’un problème en raison duquel plusieurs iframes persistantes étaient créées pour les synchronisations des identifiants et les destinations de segment.

## Version 2.10.0 - 22 avril 2022

* Utilisez un iframe persistant pour toutes les synchronisations des identifiants et destinations de segment.
* Correction d’un problème en raison duquel les propositions de mesures fusionnées étaient dupliquées dans la variable `sendEvent` result.

## Version 2.9.0 - 10 mars 2022

* Ajout de la prise en charge du suivi [!DNL control (default)] Expériences Adobe Target.
* Optimisation des événements view-change pour les applications d’une seule page. La notification d’affichage est désormais incluse avec l’événement view-change lors de la génération d’expériences personnalisées.
* Suppression de l’avertissement de la console lorsqu’il n’y en avait pas `eventType` est présente.
* Correction d’un problème en raison duquel la variable `propositions` n’est renvoyée que par une `sendEvent` lorsque des expériences ont été demandées ou extraites du cache. Le `propositions` sera désormais toujours définie comme un tableau.
* Correction d’un problème en raison duquel les conteneurs masqués n’étaient pas affichés lorsqu’une erreur était renvoyée depuis Adobe Experience Edge.
* Correction d’un problème en raison duquel les événements d’interaction n’étaient pas comptabilisés dans Adobe Target. Ce problème a été corrigé en ajoutant le nom de la vue au fichier XDM sur web.webPageDetails.viewName.
* Correction des liens rompus de la documentation dans les messages de la console.

## Version 2.8.0 - 19 janvier 2022

* Prise en charge des sélecteurs DOM fantômes pour la personnalisation.
* Types d’événements de personnalisation renommés. (`display` et `click` devenir `decisioning.propositionDisplay` et `decisioning.propositionInteract`)
* Correction d’un problème en raison duquel les offres de HTML avec des balises de script intégrées ajoutaient deux fois les balises de script à la page même si le script n’était exécuté qu’une seule fois.

## Version 2.7.0 - 26 octobre 2021

* Exposer des informations supplémentaires d’Experience Edge dans la valeur renvoyée de `sendEvent`, y compris `inferences` et `destinations`. Le format de ces propriétés peut changer, car ces fonctionnalités sont actuellement déployées dans le cadre d’une version bêta. Pour plus d’informations, voir [Suivi des événements.](fundamentals/tracking-events.md)

## Version 2.6.4 - 7 septembre 2021

* Correction d’un problème en raison duquel les actions Adobe Target de HTML étaient appliquées à la variable `head` remplacaient l’intégralité de l’élément `head` contenu. Définissez maintenant les actions de HTML appliquées à la variable `head` sont modifiés pour ajouter un HTML.

## Version 2.6.3 - 16 août 2021

* Correction d’un problème en raison duquel les objets non destinés à un usage public étaient exposés via la promesse résolue de la fonction `configure` .

## Version 2.6.2 - 4 août 2021

* Correction d’un problème en raison duquel un avertissement d’obsolescence de la variable `result.decisions` (fourni par la variable `sendEvent` ) sont consignés dans la console même lorsque la variable `result.decisions` n’était pas accessible. Aucun avertissement ne sera consigné lors de l’accès à la variable `result.decisions` , mais la propriété est toujours obsolète.

## Version 2.6.1 - 29 juillet 2021

* Correction d’un problème en raison duquel le rendu de la personnalisation pour une vue d’application d’une seule page sans contenu de personnalisation générait une erreur et provoquait la promesse renvoyée par la variable `sendEvent` à rejeter.

## Version 2.6.0 - 27 juillet 2021

* Fournit davantage de contenu de personnalisation dans le `sendEvent` promesse résolue, y compris les jetons de réponse Adobe Target. Lorsque la variable `sendEvent` est exécutée, une promesse est renvoyée, qui est finalement résolue avec une `result` contenant les informations reçues du serveur. Auparavant, cet objet de résultat incluait une propriété nommée `decisions`. Ceci `decisions` a été abandonnée. Une nouvelle propriété, `propositions`, a été ajouté. Cette nouvelle propriété permet aux clients d’accéder à davantage de contenu de personnalisation, notamment [jetons de réponse](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Version 2.5.0 - Juin 2021

* Ajout de la prise en charge des offres de personnalisation de redirection.
* Les largeurs et hauteurs de fenêtre d’affichage collectées automatiquement et qui sont des valeurs négatives ne seront plus envoyées au serveur.
* Lorsqu’un événement est annulé en revenant `false` de `onBeforeEventSend` , un message est maintenant consigné.
* Correction d’un problème en raison duquel des éléments spécifiques de données XDM destinés à un seul événement étaient inclus dans plusieurs événements.

## Version 2.4.0 - Mars 2021

* Le SDK peut désormais être [installé en tant que package npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=fr).
* Ajout de la prise en charge d’une `out` lorsque [configuration du consentement par défaut](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), qui supprime tous les événements jusqu’à ce que le consentement soit reçu (le `pending` option met les événements en file d’attente et les envoie une fois le consentement reçu).
* Le [Rappel onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) peut désormais être utilisé pour empêcher l’envoi d’un événement.
* Utilise désormais un groupe de champs de schéma XDM au lieu de `meta.personalization` lors de l’envoi d’événements au sujet du contenu personnalisé rendu ou sur lequel l’utilisateur a cliqué.
* Le [getIdentity, commande](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) renvoie désormais l’identifiant de région de périphérie à côté de l’identité.
* Les avertissements et erreurs reçus du serveur ont été améliorés et sont gérés de manière plus appropriée.
* Ajout de la prise en charge de [Adobe Consentement envoyé 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Une fois reçues, les préférences de consentement sont hachées et stockées dans un espace de stockage local afin d’optimiser l’intégration entre les CMP, le SDK web Platform et le réseau Platform Edge. Si vous collectez des préférences de consentement, nous vous encourageons maintenant à appeler `setConsent` à chaque chargement de page.
* Deux [hooks de surveillance](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` et `onCommandRejected`, ont été ajoutés.
* Bug Fix : Les événements de notification d’interaction de personnalisation contiendraient des informations en double sur la même activité lorsqu’un utilisateur accédait à une nouvelle vue d’application d’une seule page, revenait à la vue d’origine et cliquait sur un élément admissible à la conversion.
* Bug Fix : Si le premier événement envoyé par le SDK avait `documentUnloading` défini sur `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) est utilisé pour envoyer l’événement, ce qui entraîne une erreur concernant l’absence d’identification.

## Version 2.3.0 - Novembre 2020

* Ajout de la prise en charge de la valeur à usage unique pour permettre des stratégies de sécurité du contenu plus strictes.
* Ajout de la prise en charge de la personnalisation pour les applications d’une seule page.
* Amélioration de la compatibilité avec d’autres codes JavaScript sur la page qui peuvent être remplacés `window.console` API.
* Bug Fix : `sendBeacon` n’était pas utilisé lorsque `documentUnloading` a été défini sur `true` ou lorsque les clics sur les liens ont été automatiquement suivis.
* Bug Fix : Un lien ne serait pas automatiquement suivi si l’élément d’ancrage contenait du contenu HTML.
* Bug Fix : Certaines erreurs de navigateur contenant une `message` n’ont pas été gérées correctement, ce qui a entraîné une erreur différente lors de l’exposition du client.
* Bug Fix : L’exécution du SDK dans un iframe entraîne une erreur si la page de HTML de l’iframe provient d’un sous-domaine différent de celui de la page de HTML de la fenêtre parente.

## Version 2.2.0 - Octobre 2020

* Bug Fix : L’objet Opt-in empêchait Alloy d’effectuer des appels lors de la `idMigrationEnabled` is `true`.
* Bug Fix : Rendre à Alloy conscient des demandes qui doivent renvoyer des offres de personnalisation pour éviter un problème de scintillement.

## Version 2.1.0 - Août 2020

* Supprimez le `syncIdentity` la commande et la prise en charge de la transmission de ces identifiants dans la variable `sendEvent` .
* Prise en charge de la norme de consentement IAB 2.0.
* Prise en charge de la transmission d’identifiants supplémentaires dans la variable `setConsent` .
* Prise en charge du remplacement de la variable `datasetId` dans le `sendEvent` .
* Moniteurs d’affectation de prise en charge ([En savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pass `environment: browser` dans les données contextuelles des détails de mise en oeuvre.
