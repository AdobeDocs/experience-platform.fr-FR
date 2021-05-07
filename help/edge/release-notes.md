---
title: Notes de mise à jour du SDK web Adobe Experience Platform
description: Notes de mise à jour les plus récentes pour le SDK Web Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK ; Platform Web SDK ; Web SDK ; notes de mise à jour ;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---

# Notes de mise à jour

## Version 2.4.0, mars 2021

* Le SDK peut désormais être [installé en tant que package npm](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Prise en charge Ajoutée d&#39;une option `out` lorsque [la configuration du consentement par défaut](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), qui abandonne tous les événements jusqu&#39;à ce que le consentement soit reçu (l&#39;option `pending` existante met en file d&#39;attente les événements et les envoie une fois le consentement reçu).
* Le rappel [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) peut maintenant être utilisé pour empêcher l&#39;envoi d&#39;un événement.
* Utilise désormais un groupe de champs de schéma XDM au lieu de `meta.personalization` lors de l’envoi de événements sur le rendu ou l’activation du contenu personnalisé.
* La commande [getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) renvoie désormais l&#39;identifiant de région du bord à côté de l&#39;identité.
* Les avertissements et les erreurs reçus du serveur ont été améliorés et sont gérés de manière plus appropriée.
* Prise en charge Ajoutée de [le Adobe Confort a envoyé la norme 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Une fois reçues, les préférences de consentement sont hachées et stockées dans l’enregistrement local pour une intégration optimisée entre les CMP, le SDK Web de plate-forme et le réseau Edge de plate-forme. Si vous collectez des préférences de consentement, nous vous encourageons maintenant à appeler `setConsent` à chaque chargement de page.
* Deux hameçons de surveillance [](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` et `onCommandRejected` ont été ajoutés.
* Correctif : Les événements de notification d’interaction de personnalisation contiennent des informations de duplicata sur la même activité lorsqu’un utilisateur accède à une nouvelle vue d’application d’une seule page, revient à la vue d’origine et clique sur un élément pouvant faire l’objet d’une conversion.
* Correctif : Si le premier événement envoyé par le SDK avait `documentUnloading` défini sur `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) serait utilisé pour envoyer le événement, ce qui provoquerait une erreur concernant l&#39;absence d&#39;identification d&#39;une identité.

## Version 2.3.0, novembre 2020

* Prise en charge des nonce Ajoutée pour permettre des stratégies de sécurité du contenu plus strictes.
* Prise en charge de la personnalisation Ajoutée pour les applications d’une seule page.
* Amélioration de la compatibilité avec d’autres codes JavaScript sur la page susceptibles de remplacer les API `window.console`.
* Correctif : `sendBeacon` n&#39;était pas utilisé lorsque `documentUnloading` était défini sur `true` ou lorsque les clics sur les liens étaient automatiquement suivis.
* Correctif : Un lien ne serait pas automatiquement suivi si l’élément d’ancrage contenait du contenu HTML.
* Correctif : Certaines erreurs de navigateur contenant une propriété `message` en lecture seule n&#39;ont pas été gérées correctement, ce qui a provoqué une autre erreur exposée au client.
* Correctif : L’exécution du SDK dans un iframe provoquerait une erreur si la page HTML de l’iframe provenait d’un sous-domaine différent de celui de la page HTML de la fenêtre parent.

## Version 2.2.0, octobre 2020

* Correctif : L’objet d’inclusion empêchait Alloy d’effectuer des appels lorsque `idMigrationEnabled` est `true`.
* Correctif : Sensibilisez Alloy aux demandes qui doivent renvoyer des offres de personnalisation afin d’éviter un problème de scintillement.

## Version 2.1.0, août 2020

* Supprimez la commande `syncIdentity` et prenez en charge la transmission de ces identifiants dans la commande `sendEvent`.
* Prise en charge de la norme de consentement IAB 2.0.
* Prise en charge de la transmission d’identifiants supplémentaires dans la commande `setConsent`.
* Prise en charge du remplacement de `datasetId` dans la commande `sendEvent`.
* Moniteurs d’alliage d’assistance ([En savoir plus](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Transmettez `environment: browser` dans les données contextuelles des détails d’implémentation.
