---
title: Notes de mise à jour de l’extension SDK Web Adobe Experience Platform
description: Extension de balise SDK Web Adobe Experience Platform
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 18f7e32c8922b254d68655aeb2b633c12a97d2a7
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 46%

---

# Notes de mise à jour de l’extension SDK Web Adobe Experience Platform

Ce document couvre les notes de mise à jour de l’extension de balise SDK Web Adobe Experience Platform. Pour obtenir les dernières notes de mise à jour sur le SDK lui-même, voir la section [Notes de mise à jour du SDK Web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Version 2.11.2 - 3 mai 2022

Contient la version 2.10.1 de la bibliothèque SDK Web de Adobe Experience Platform.

## Version 2.11.1 - 22 avril 2022

* Correction de l’erreur de configuration des commandes de la version 2.11.0.

Contient la version 2.10.0 de la bibliothèque SDK Web de Adobe Experience Platform.

## Version 2.11.0 - 22 avril 2022

* Amélioration des performances de l’interface utilisateur des balises.
* Ajoutez des sélecteurs sandbox à la configuration de l’extension datastreams.

Contient la version 2.10.0 de la bibliothèque SDK Web de Adobe Experience Platform.

## Version 2.10.0 - 10 mars 2022

* Mettez à jour le fragment de code de masquage préalable qui peut être copié sur la page de configuration pour fonctionner avec l’éditeur du VEC d’Adobe Target mis à jour.

Contient la version 2.9.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.9.0 - 19 janvier 2022

Contient la version 2.8.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.8.0 - 26 octobre 2021

Contient la version 2.7.0 de la bibliothèque SDK Web Adobe Experience Platform.

* Des informations supplémentaires provenant d’Experience Edge sont disponibles dans l’événement Send Event Complete , notamment `inferences` et `destinations`. Le format de ces propriétés peut changer, car ces fonctionnalités sont actuellement déployées dans le cadre d’une version bêta. Pour plus d’informations, voir [Suivi des événements.](../fundamentals/tracking-events.md)

## Version 2.7.3 - 7 septembre 2021

Contient la version 2.6.4 de la bibliothèque SDK Web Adobe Experience Platform.

* Il n’existe plus d’avertissement d’obsolescence pour `container.buildInfo.environment.`

## Version 2.7.0 - 16 août 2021

Contient la version 2.6.3 de la bibliothèque SDK Web Adobe Experience Platform.

* Lors de l’utilisation du type d’élément de données de carte des identités, les identifiants dont les identifiants se résolvent en valeurs qui ne sont pas des chaînes renseignées sont désormais automatiquement supprimés de la carte des identités.
* Correction d’une erreur qui se produisait lors de la tentative d’enregistrement d’un élément de données à l’aide du type d’élément de données Objet XDM alors qu’aucun schéma n’était sélectionné.
* Amélioration de la typographie de l’interface utilisateur.

## Version 2.6.2 - 4 août 2021

Contient la version 2.6.2 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.6.1 - 29 juillet 2021

Contient la version 2.6.1 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.6.0 - 27 juillet 2021

Contient la version 2.6.0 de la bibliothèque SDK Web Adobe Experience Platform.

* Les libellés, descriptions et messages d’erreur utilisant le terme &quot;configuration de périphérie&quot; ont été modifiés afin d’utiliser le terme &quot;flux de données&quot; pour s’aligner sur la terminologie Adobe Experience Platform la plus récente.
* Dans la vue de configuration de l’extension, la prise en charge a été ajoutée pour la gestion d’un grand nombre de jeux de données et d’environnements de flux de données.
* Dans la vue d’élément de données Objet XDM, la prise en charge du traitement d’un grand nombre de schémas a été ajoutée.
* Un type d’événement Send Event Complete a été ajouté. Il peut être utilisé pour exécuter une règle après l’envoi d’un événement au serveur et la réception d’une réponse. D’autres documents seront bientôt disponibles.
* Le type d’événement Decisions Received a été abandonné. Utilisez plutôt le type d’événement Send Event Complete .
* L’interface utilisateur et la gestion des erreurs ont généralement été améliorées.

## Version 2.5.0 - 1er juin 2021

Contient la version 2.5.0 de la bibliothèque SDK Web Adobe Experience Platform.

* Ajout d’une `data` à l’action Envoyer l’événement . La documentation à venir décrit l’utilisation de cette fonctionnalité dans certains scénarios.
* Sur la vue d’élément de données d’objet XDM, un problème a été corrigé en raison duquel une erreur était générée si l’utilisateur avait accès aux environnements de test Adobe Experience Platform, mais pas à l’environnement de test configuré par défaut pour l’organisation.
* Sur la vue d’élément de données Objet XDM, un problème a été résolu, en raison duquel un champ de schéma obligatoire était considéré comme non valide même si l’objet parent ne contenait aucune valeur.

## Version 2.4.0 - 9 mars 2021

Contient la version 2.4.0 de la bibliothèque SDK Web Adobe Experience Platform.

* Ajout [&quot;déchargement de document&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) pour envoyer l’interface utilisateur de l’action d’événement.
* Ajout de la prise en charge d’une `out` lorsque [configuration du consentement par défaut](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) qui supprime tous les événements jusqu’à ce que le consentement soit reçu (le `pending` option met les événements en file d’attente et les envoie une fois le consentement reçu).
* Ajout d’une info-bulle au champ de consentement par défaut.
* Ajout de la prise en charge de [Adobe Consentement envoyé 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Une meilleure erreur s’affiche désormais dans l’interface utilisateur de l’élément de données de l’objet XDM si le jeton d’accès de l’utilisateur n’est pas valide ou a été configuré de manière incorrecte.
* Correction d’une erreur d’origine croisée (qui n’affecte pas le fonctionnement de l’extension) qui s’affichait sur la console de développement du navigateur lors de l’affichage d’un élément de données d’objet XDM.

## Version 2.3.0 - 4 novembre 2020

Contient la version 2.3.0 de la bibliothèque SDK Web Adobe Experience Platform.

* Ajout de la prise en charge de l’utilisation d’un élément de données lors de la configuration du consentement par défaut.
* Ajout de la possibilité de rechercher des schémas XDM avec le type d’élément de données Objet XDM.
* Ajout du clonage des données XDM dans le type d’action ‘Envoyer l’événement’ pour s’assurer que les modifications ultérieures apportées à l’objet de données XDM ne seront pas prises en compte dans la requête.

## Version 2.2.0 - 1er octobre 2020

* Lorsque les clients tentaient de créer un objet XDM à partir de schémas sandbox, ils se heurtaient à des problèmes d’authentification. L’API qui appelle Platform connaît désormais les environnements, de sorte que les utilisateurs ne reçoivent que les schémas qu’ils ont accès à la modification.
* Lors de l’utilisation de la variable `identityMap` , les espaces de noms sont maintenant préremplis dans une liste déroulante, ce qui évite d’avoir à les remplir manuellement.
* Optimisation de l’interface utilisateur pour l’élément de données `xdmObject`. Dans la nouvelle interface utilisateur, vous pouvez identifier les champs qui ont été renseignés sans avoir à entrer chaque élément dans l’objet.

## Version 2.1.1 - 26 août 2020

* Correction d’un problème en raison duquel les environnements de test Adobe Experience Platform sur la vue Objet XDM s’affichaient incorrectement. Si, lors de l’utilisation de cette version de l’extension, un environnement de test attendu n’est pas affiché dans la liste, l’utilisateur doit vérifier auprès de son administrateur Adobe Experience Platform pour s’assurer que les autorisations d’accès sont correctement définies.

## Version 2.1.0 - 5 août 2020

* Changement important : supprimez l’action `syncIdentity` et privilégiez plutôt le transfert de ces identifiants vers l’action `sendEvent`. Veuillez désactiver toute règle existante qui utilise cette action avant de mettre à niveau votre extension.
* Mise à jour vers Alloy v. 2.1.0 ([Notes de mise à jour](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Prise en charge de la norme de consentement IAB 2.0 dans l’action `setConsent`.
* Prise en charge du remplacement de l’identifiant de jeu de données dans l’action `sendEvent`.
* Ajout d’un nouvel élément de données de type `IdentityMap` qui peut être utilisé pour renseigner l’entrée `identityMap` dans l’élément de données de l’objet XDM (qui est maintenant activé) et dans l’action `setConsent`.
* Prise en charge de la transmission d’une carte d’identité dans l’action `setConsent`.
* Prise en charge du choix d’un environnement de test Platform dans l’élément de données d’objet XDM.

## Version 1.0.0 - 26 mai 2020

* Prise en charge de la sélection de l’environnement à partir du service de configuration.

## Version 0.1.2 - 4 mai 2020

* Renommé `configId` en `edgeConfigId`.
* Renommé `viewStart` en `renderDecisions`, défini sur false par défaut. Si la valeur est définie sur true, les offres de personnalisation sont récupérées et rendues automatiquement.
* Changements liés à `Get Decisions` :
   * Suppression de la commande `getDecisions`.
   * Ajout d’une option `scopes` à la commande `sendEvent`. Les décisions sont renvoyées dans la promesse `sendEvent` résolue.
   * Ajout d’une portée intégrée `__view__` qui résultera en un renvoi d’offres à l’échelle de la page/vue. (offres du compositeur d’expérience visuelle dans Target, par exemple.)
Ces décisions ne sont renvoyées par la commande `sendEvent` que si `renderDecisions` est défini sur false.
   * Ajout d’un événement `Decisions Received`, qui se déclenche lorsque des décisions deviennent disponibles.
* Combinaison de plusieurs notifications de personnalisation sous un seul appel de serveur.
* Correction d’un problème en raison duquel l’ID de fusion des événements était réinitialisé chaque fois que l’élément de données était référencé.
* L’action `setCustomerIds` a été renommée `syncIdentity`.
* Ajout d’une commande `getIdentity`. Pour l’instant, elle ne peut être consommée que via du Custom Code (code personnalisé).
* Activation du débogage à l’aide de `_satellite` active désormais le débogage dans le SDK Web de Adobe Experience Platform.
* Ajout de la prise en charge des valeurs saisies dans l’objet XDM : Booléens, Nombres et Décimales.

## Version 0.0.10 - 16 mars 2020

* Combinaison des concepts opt-in et opt-out sous `Consent` et ajout d’une nouvelle commande `setConsent`.
* Ajout d’un nouvel élément de données de type `XDM Object` qui permet le mappage de JavaScript/JSON à XDM.

## Version 0.0.7 - 18 février 2020

* Les options idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled et cookieDestinationsEnabled ont été supprimées.
* Les tirets sont maintenant pris en charge dans la valeur de l’option edgeDomain.
* La requête effectuée lors de la migration des identifiants est envoyée au point de terminaison demdex afin d’améliorer l’identification inter-domaines lorsque le cookie demdex n’est pas défini.
* La requête effectuée lors de la migration des identifiants attend toujours une réponse afin de s’assurer que le cookie d’identité est défini.
* Lors de l’exécution d’une commande non valide, une liste de noms de commande valides sera enregistrée dans la console.
* Ajout d’une case à cocher pour activer ou désactiver la prise en charge des cookies tiers dans l’extension de balise. Ceci désactive les appels vers demdex.net.

## Version 0.0.5 - 20 décembre 2019

* Ajout des configurations de suivi d’activité à l’extension de balise
* Exposition d’EventType et EventMergeId sur la commande d’événement.
* Ajouter la configuration onBeforeEventSend à l’extension de balise
* Ajouter une configuration edgeBasePath à l’extension de balise

## Version 0.0.3 - 25 novembre 2019

* Nouveaux champs ID de fusion et Type dans l’action Envoyer un événement. L’ID de fusion est mappé sur `xdm.eventMergeID` et le Type est mappé sur `xdm.eventType` dans le schéma XDM.

## Version 0.0.2 - 18 novembre 2019

* Version initiale
