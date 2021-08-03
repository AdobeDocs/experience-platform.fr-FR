---
title: Notes de mise à jour du SDK web Adobe Experience Platform
description: Notes de mise à jour les plus récentes pour le SDK Web Adobe Experience Platform.
keywords: SDK Web Adobe Experience Platform;SDK Web Platform;SDK Web;notes de mise à jour;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 165c9bce5dabce9704202ebab6b97a4a30e4ca00
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 3%

---

# Notes de mise à jour

## Version 2.6.2 - 4 août 2021

* Correction d’un problème en raison duquel un avertissement d’obsolescence de `result.decisions` (fourni par la commande `sendEvent`) était consigné dans la console même lorsque la propriété `result.decisions` n’était pas accessible. Aucun avertissement ne sera consigné lors de l’accès à la propriété `result.decisions`, mais la propriété est toujours obsolète.

## Version 2.6.1 - 29 juillet 2021

* Correction d’un problème en raison duquel le rendu de la personnalisation pour une vue d’application d’une seule page sans contenu de personnalisation générait une erreur et provoquait le rejet de la promesse renvoyée par la commande `sendEvent`.

## Version 2.6.0 - 27 juillet 2021

* Fournit davantage de contenu de personnalisation dans la promesse résolue `sendEvent`, y compris les jetons de réponse Adobe Target. Lorsque la commande `sendEvent` est exécutée, une promesse est renvoyée, qui est finalement résolue avec un objet `result` contenant les informations reçues du serveur. Cet objet result comprend une propriété nommée `decisions`. Cette propriété `decisions` est obsolète. Une nouvelle propriété, `propositions`, a été ajoutée. Cette nouvelle propriété permet aux clients d’accéder à davantage de contenu de personnalisation, y compris des jetons de réponse. D’autres documents seront bientôt disponibles.

## Version 2.5.0 - Juin 2021

* Ajout de la prise en charge des offres de personnalisation de redirection.
* Les largeurs et hauteurs de fenêtre d’affichage collectées automatiquement et qui sont des valeurs négatives ne seront plus envoyées au serveur.
* Lorsqu’un événement est annulé en renvoyant `false` d’un rappel `onBeforeEventSend`, un message est maintenant consigné.
* Correction d’un problème en raison duquel des éléments spécifiques de données XDM destinés à un seul événement étaient inclus dans plusieurs événements.

## Version 2.4.0 - Mars 2021

* Le SDK peut désormais être [installé en tant que package npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=fr).
* Ajout de la prise en charge d’une option `out` lors de la configuration du consentement par défaut](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), qui supprime tous les événements jusqu’à réception du consentement (l’option `pending` existante place les événements en file d’attente et les envoie une fois le consentement reçu).[
* Le rappel [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) peut désormais être utilisé pour empêcher l’envoi d’un événement.
* Désormais, utilise un groupe de champs de schéma XDM au lieu de `meta.personalization` lors de l’envoi d’événements au sujet du contenu personnalisé rendu ou sur lequel l’utilisateur a cliqué.
* La [commande getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) renvoie désormais l’identifiant de région de périphérie avec l’identité.
* Les avertissements et erreurs reçus du serveur ont été améliorés et sont gérés de manière plus appropriée.
* Ajout de la prise en charge de la norme [Consentement de l’Adobe 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Une fois reçues, les préférences de consentement sont hachées et stockées dans un espace de stockage local afin d’optimiser l’intégration entre les CMP, le SDK web Platform et le réseau Platform Edge. Si vous collectez les préférences de consentement, nous vous encourageons maintenant à appeler `setConsent` à chaque chargement de page.
* Deux [hooks de surveillance](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` et `onCommandRejected` ont été ajoutés.
* Bug Fix : Les événements de notification d’interaction de personnalisation contiendraient des informations en double sur la même activité lorsqu’un utilisateur accédait à une nouvelle vue d’application d’une seule page, revenait à la vue d’origine et cliquait sur un élément admissible à la conversion.
* Bug Fix : Si `documentUnloading` du premier événement envoyé par le SDK est défini sur `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) est utilisé pour envoyer l’événement, ce qui entraîne une erreur concernant l’absence d’identification.

## Version 2.3.0 - Novembre 2020

* Ajout de la prise en charge de la valeur à usage unique pour permettre des stratégies de sécurité du contenu plus strictes.
* Ajout de la prise en charge de la personnalisation pour les applications d’une seule page.
* Amélioration de la compatibilité avec d’autres codes JavaScript sur la page qui peuvent remplacer les API `window.console`.
* Bug Fix : `sendBeacon` n’était pas utilisé lorsque `documentUnloading` était défini sur `true` ou lorsque les clics sur les liens étaient automatiquement suivis.
* Bug Fix : Un lien ne serait pas automatiquement suivi si l’élément d’ancrage contenait du contenu HTML.
* Bug Fix : Certaines erreurs de navigateur contenant une propriété `message` en lecture seule n’ont pas été traitées correctement, ce qui a entraîné une erreur différente qui a été exposée au client.
* Bug Fix : L’exécution du SDK dans un iframe entraîne une erreur si la page HTML de l’iframe provient d’un sous-domaine différent de la page HTML de la fenêtre parente.

## Version 2.2.0 - Octobre 2020

* Bug Fix : L’objet Opt-in empêchait Alloy d’effectuer des appels lorsque `idMigrationEnabled` est `true`.
* Bug Fix : Rendre à Alloy conscient des demandes qui doivent renvoyer des offres de personnalisation pour éviter un problème de scintillement.

## Version 2.1.0 - Août 2020

* Supprimez la commande `syncIdentity` et prenez en charge le transfert de ces ID dans la commande `sendEvent`.
* Prise en charge de la norme de consentement IAB 2.0.
* Prise en charge de la transmission d’identifiants supplémentaires dans la commande `setConsent`.
* Prise en charge du remplacement de `datasetId` dans la commande `sendEvent`.
* Moniteurs d’affectation de prise en charge ([En savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Transmettez `environment: browser` dans les données contextuelles des détails de mise en oeuvre.
