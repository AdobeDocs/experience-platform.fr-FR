---
title: Extension SDK Web Adobe Experience Platform
seo-title: SDK Web Adobe Experience Platform dans Adobe Experience Platform Launch
description: SDK Web Adobe Experience Platform dans Adobe Experience Platform Launch
seo-description: SDK Web Adobe Experience Platform dans Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 56f0b3abd859a6b27f0117fb6ec4c312ca93ba5d
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 100%

---


# Notes de mise à jour du SDK web Adobe Experience Platform

[En savoir plus : Notes de mise à jour du SDK web Adobe Experience Platform](https://docs.adobe.com/content/help/fr-FR/experience-platform/edge/release-notes.html)

## 4 novembre 2020

### SDK web 2.3.0 Adobe Experience Platform

Contient la version 2.3.0 de la bibliothèque SDK Web Adobe Experience Platform.

#### Fonctionnalités

* Ajout de la prise en charge de l’utilisation d’un élément de données lors de la configuration du consentement par défaut.
* Ajout de la possibilité de rechercher des schémas XDM avec le type d’élément de données Objet XDM.
* Ajout du clonage des données XDM dans le type d’action ‘Envoyer l’événement’ pour s’assurer que les modifications ultérieures apportées à l’objet de données XDM ne seront pas prises en compte dans la requête.

## 1 octobre 2020

### SDK web 2.2.0 Adobe Experience Platform

#### Correctifs

* Lorsque les clients tentaient de créer un objet XDM à partir de schémas sandbox, ils se heurtaient à des problèmes d’authentification. L’API qui appelle AEP prend désormais en charge les environnements, de sorte que les utilisateurs ne reçoivent que les schémas qu’ils sont autorisés à modifier.

#### Fonctionnalités

* Lors de l’utilisation de l’élément de données `identityMap`, les espaces de noms sont maintenant préremplis dans une liste déroulante, ce qui évite d’avoir à les remplir manuellement.
* Optimisation de l’interface utilisateur pour l’élément de données `xdmObject`. Dans la nouvelle interface utilisateur, vous pouvez identifier les champs qui ont été renseignés sans avoir à entrer chaque élément dans l’objet.


## 26 août 2020

### SDK web 2.1.1 Adobe Experience Platform

#### Fonctionnalités

* Correction d’un problème en raison duquel les environnements de test Adobe Experience Platform sur la vue Objet XDM s’affichaient incorrectement. Si, lors de l’utilisation de cette version de l’extension, un environnement de test attendu n’est pas affiché dans la liste, l’utilisateur doit vérifier auprès de son administrateur Adobe Experience Platform pour s’assurer que les autorisations d’accès sont correctement définies.


## 5 août 2020

### SDK web 2.1.0 Adobe Experience Platform

#### Fonctionnalités

* Changement important : supprimez l’action `syncIdentity` et privilégiez plutôt le transfert de ces identifiants vers l’action `sendEvent`. Veuillez désactiver toute règle existante qui utilise cette action avant de mettre à niveau votre extension.
* Mise à jour vers Alloy v. 2.1.0 ([Notes de mise à jour](https://docs.adobe.com/content/help/en/experience-platform/edge/release-notes.html))
* Prise en charge de la norme de consentement IAB 2.0 dans l’action `setConsent`.
* Prise en charge du remplacement de l’identifiant de jeu de données dans l’action `sendEvent`.
* Ajout d’un nouvel élément de données de type `IdentityMap` qui peut être utilisé pour renseigner l’entrée `identityMap` dans l’élément de données de l’objet XDM (qui est maintenant activé) et dans l’action `setConsent`.
* Prise en charge de la transmission d’une carte d’identité dans l’action `setConsent`.
* Prise en charge du choix d’une sandbox AEP dans l’élément de données de l’objet XDM.


## 26 mai 2020

### SDK web 1.0.0 Adobe Experience Platform

#### Fonctionnalités

* Prise en charge de la sélection de l’environnement à partir du service de configuration.


## 4 mai 2020

### SDK web 0.1.2 Adobe Experience Platform

#### Fonctionnalités

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
* L’activation du débogage à l’aide de `_satellite` active maintenant le débogage dans le SDK Web AEP.
* Ajout de la prise en charge des valeurs saisies dans l’objet XDM : Booléens, Nombres et Décimales.

## 16 mars 2020

### SDK web 0.0.10 Adobe Experience Platform

#### Fonctionnalités

* Combinaison des concepts opt-in et opt-out sous `Consent` et ajout d’une nouvelle commande `setConsent`.
* Ajout d’un nouvel élément de données de type `XDM Object` qui permet le mappage de JavaScript/JSON à XDM.

## 18 février 2020

### SDK web 0.0.7 Adobe Experience Platform

#### Fonctionnalités

* Les options idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled et cookieDestinationsEnabled ont été supprimées.
* Les tirets sont maintenant pris en charge dans la valeur de l’option edgeDomain.
* La requête effectuée lors de la migration des identifiants est envoyée au point de terminaison demdex afin d’améliorer l’identification inter-domaines lorsque le cookie demdex n’est pas défini.
* La requête effectuée lors de la migration des identifiants attend toujours une réponse afin de s’assurer que le cookie d’identité est défini.
* Lors de l’exécution d’une commande non valide, une liste de noms de commande valides sera enregistrée dans la console.
* Ajout d’une case à cocher afin d’activer ou de désactiver la prise en charge des cookies tiers dans l’extension d’Adobe Experience Platform Launch. Ceci désactive les appels vers demdex.net.

## 20 décembre 2019

### SDK web 0.0.5 Adobe Experience Platform

#### Fonctionnalités

* Ajout des configurations de suivi d’activité à l’extension Platform Launch.
* Exposition d’EventType et EventMergeId sur la commande d’événement.
* Ajouter une configuration onBeforeEventSend à l’extension Platform Launch.
* Ajout d’une configuration edgeBasePath à l’extension Platform Launch.

#### Mise à jour vers Alloy version 0.0.10 qui comprend les modifications suivantes :

* Implémentation du stockage client : logique de l’état et des cookies déplacée vers le serveur.
* Exposition d’EventType et EventMergeId sur la commande d’événement.
* Utilisation de sendBeacon pour le suivi des liens autres que les liens de sortie.
* Retour des synchronisations d’identifiants sans vérification de l’expiration.
* La commande setCustomerIds ne hache plus les identifiants sur les pages non-SSL (http).
* Le passage d’un domaine APEX au serveur doit être utilisé lors de la définition de l’état ou des cookies.
* La récupération de l’ECID à partir de la réponse se fait à l’aide d’une nouvelle méthode.
* Suppression des valeurs par défaut des configurations d’activation et d’identité.
* Les options de requête ont été renommées et déplacées en méta.
* Migration ECID héritée.

#### Correctifs

* Lors d’un code d’état inattendu, analyse et formatage du corps de la réponse pour le message d’erreur.
* L’exécution de la commande de débogage ou l’utilisation d’alloy_debug est écrasée par la configuration.

## 25 novembre 2019

### SDK web 0.0.3 Adobe Experience Platform

#### Fonctionnalités

* Nouveaux champs ID de fusion et Type dans l’action Envoyer un événement. L’ID de fusion est mappé sur `xdm.eventMergeID` et le Type est mappé sur `xdm.eventType` dans le schéma XDM.
* Amélioration de la gestion des erreurs et de la création de rapports.
* Utilise désormais `sendBeacon` pour tous les liens.

#### Correctifs

* Correction d’un problème en raison duquel le débogage avec basculement via un paramètre de chaîne de requête ou la commande `debug` ne persistait pas pendant la session.

## 18 novembre 2019

### SDK web 0.0.2 Adobe Experience Platform

#### Fonctionnalités

* Création de l’extension.
* Prise en charge ECID sans appel réseau ou bibliothèque supplémentaires.
* Prise en charge de l’inclusion.
* Prise en charge de l’envoi de XDM vers AEP.
* Prise en charge des domaines propriétaires.
* Collecte automatique du contexte du navigateur.
* Entièrement open source ([extension](https://github.com/adobe/reactor-extension-alloy), [SDK](https://github.com/adobe/reactor-extension-alloy)).
* Journalisation détaillée.
* Possibilité de masquer les erreurs en production.
