---
title: Notes de mise à jour de l’extension du SDK Web Adobe Experience Platform
description: Extension de la balise SDK Web Adobe Experience Platform
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 8fd86a170433c4eb07a7370dbd3aa2cb3ef10922
workflow-type: ht
source-wordcount: '2580'
ht-degree: 100%

---

# Notes de mise à jour de l’extension du SDK Web Adobe Experience Platform

Ce document contient les notes de mise à jour de l’extension de balises du SDK Web Adobe Experience Platform. Pour obtenir les dernières notes de mise à jour sur le SDK lui-même, voir les [notes de mise à jour du SDK Web Platform](/help/web-sdk/release-notes.md).

## Version 2.29.0 - 5 mars 2025

**Nouvelles fonctionnalités**

- Vous pouvez désormais créer des versions SDK web personnalisées et choisir les composants dont vous avez besoin à partir de l’interface d’utilisation de l’extension des balises. Vous pouvez ainsi obtenir des versions plus petites en excluant des composants non utilisés. Consultez la documentation sur la [création de versions SDK web personnalisées](web-sdk-extension-configuration.md#custom-build).
- Contient la [version 2.26.0](../../../../web-sdk/release-notes.md#2-26-0) du SDK web d’Adobe Experience Platform.

**Correctifs et améliorations**

- Ajout de la gestion gracieuse des éléments de données manquants dans les actions [Mettre à jour la variable](action-types.md#update-variable). Auparavant, la modification d’une action Mettre à jour la variable contenant un élément de données manquant s’affichait comme message d’erreur. À présent, vous pouvez choisir un autre élément de données afin d’appliquer l’action Mettre à jour la variable à tous les paramètres. Des éléments de données peuvent être manquants s’ils sont supprimés ou si une propriété Balises est en double.
- Ajout de la prise en charge de l’ouverture d’un nouvel onglet avec l’action [Redirection vers une identité](action-types.md#redirect-with-identity). À présent, si vous utilisez cette action, l’attribut `target` de la balise d’ancrage est utilisé pour rediriger le navigateur.
- Correction d’un problème en raison duquel Adobe Audience Manager ne pouvait pas être désactivé dans les remplacements de la configuration.

## Version 2.28.0 - vendredi 23 janvier 2025

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les remplacements du conteneur de synchronisation des identifiants ne pouvaient pas être définis sans activer Audience Manager.
- Correction d’un problème en raison duquel les remplacements de configuration des trains de données étaient désactivés lors de la mise à niveau vers la dernière version.
- Correction d’un problème en raison duquel les utilisateurs et les utilisatrices ne pouvaient pas enregistrer les paramètres de collecte de clics automatiques de Target.

**Nouvelles fonctionnalités**

- Ajout d’une nouvelle fonctionnalité permettant de basculer entre les noms techniques et les noms d’affichage dans l’objet XDM.
- Contient la [version 2.25.0](../../../../web-sdk/release-notes.md#2-25-0) du SDK web d’Adobe Experience Platform.

## Version 2.27.0 - 31 octobre 2024

**Nouvelles fonctionnalités**

- Les [remplacements de train de données](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides) comprennent désormais des paramètres pour désactiver les solutions Experience Cloud et les services Adobe Experience Platform.
- Vous pouvez en effet créer des [remplacements de train de données](../web-sdk/web-sdk-extension-configuration.md) pour les sessions de médias.

Contient la version 2.24.0 du SDK web d’Adobe Experience Platform.

## Version 2.26.1 - 19 septembre 2024

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les cookies n’étaient pas correctement écrits lors de l’exécution locale du SDK web.

Contient la version 2.23.0 du SDK web d’Adobe Experience Platform.

## Version 2.26.0 - vendredi 22 août 2024

**Nouvelles fonctionnalités**

- Ajout du point de contrôle de l’événement `triggered`.
- Les fonctionnalités [Événements guidés](action-types.md#instance), [Demander une personnalisation par défaut](action-types.md#personalization), [S’abonner aux éléments de l’ensemble de règles](event-types.md#subscribe-ruleset-items), et [Évaluer les ensembles de règles](action-types.md#evaluate-rulesets) sont désormais généralement disponibles.

**Correctifs et améliorations**

- Correction d’un problème où des éléments de données variables dupliqués pouvaient se remplacer les uns les autres.
- En utilisant l’événement guidé [ Demander la personnalisation par défaut](action-types.md#personalization), les choix de personnalisation visuelle sont maintenant activés automatiquement.

Contient la version 2.22.0 du SDK web d’Adobe Experience Platform.

## Version 2.25.0 - vendredi 18 juillet 2024

**Nouvelles fonctionnalités**

- Ajout de la prise en charge du suivi automatique de la personnalisation dans Adobe Journey Optimizer.
- Ajout de nouveaux paramètres pour gérer la collecte de clics améliorée.

Contient la version 2.21.1 du SDK web d’Adobe Experience Platform.

## Version 2.24.0 - jeudi 5 juin 2024

**Correctifs et améliorations**

- Correction d’une erreur qui se produisait lors de la modification de la configuration de l’extension lorsque des remplacements de configuration étaient définis.
- Permet de définir des valeurs vides pour les intervalles de ping de la collecte de médias.
- Correction d’une erreur qui se produisait lors de la modification d’une action de variable de mise à jour.
- Permet la réinitialisation du conteneur de synchronisation des identifiants dans les remplacements de configuration.

Contient la version 2.20.0 du SDK web d’Adobe Experience Platform.

## Version 2.23.1 - 28 mai 2024

**Nouvelles fonctionnalités**

- Ajout de la prise en charge du composant [`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media) dans la configuration de l’extension.
- Ajout de l’action [`Send Media Event`](action-types.md#send-media-event) pour la fonctionnalité [!DNL Streaming Media Collection].
- Ajout de l’élément de données [`Media: Quality of Experience`](data-element-types.md#quality-experience) pour la fonctionnalité [!DNL Streaming Media Collection].

Contient la version 2.20.0 du SDK web d’Adobe Experience Platform.

**Correctifs et améliorations**

- Correction d’une erreur qui se produisait lors de la recherche d’éléments de données dans l’action [Mettre à jour la variable](action-types.md#update-variable).
- Suppression des types d’événement [!UICONTROL Médias] parmi les types d’événement proposés à l’utilisation dans l’action `sendEvent`.

## Version 2.22.0 - 3 mai 2024

**Nouvelles fonctionnalités**

- Étendez des éléments de données de variables pour prendre en charge les objets de données.
- L’action de mise à jour de variable prend désormais en charge la modification des données via Adobe Analytics, Adobe Audience Manager et Adobe Target.

Contient la version 2.19.2 du SDK web d’Adobe Experience Platform.

## Version 2.21.4 - 10 janvier 2024

**Correctifs et améliorations**

- Correction d’un problème en raison duquel l’enregistrement des remplacements de configuration sans les trois environnements définis bloquait l’interface utilisateur de l’extension.
- Correction d’un problème en raison duquel la case à cocher Effacer la valeur existante de la racine n’était pas renseignée lors de la modification d’une action de mise à jour de variable.

Contient la version 2.19.2 du SDK web d’Adobe Experience Platform.

## Version 2.21.3 - 10 novembre 2023

Contient la version 2.19.1 du SDK web d’Adobe Experience Platform.

**Correctifs et améliorations**

- Correction d’un problème en raison duquel le tableau de propositions disponible dans les événements `Send event complete` était toujours vide.

## Version 2.21.2 - 1er novembre 2023

**Nouvelles fonctionnalités**

- Ajout de l’option `Request default personalization` pour envoyer une action d’événement.
- Ajout de la prise en charge des événements de haut et de bas de page dans l’action d’événement d’envoi.
- Ajout de l’action `Apply propositions`.
- Ajout de l’action `Evaluate rulesets` et de l’événement `Subscribe ruleset items` pour les messages in-app.
- Ajout de `Decision context` pour envoyer une action d’événement.

**Correctifs et améliorations**

- Contient la version 2.19.0 du SDK web d’Adobe Experience Platform.

## Version 2.20.3 - 8 août 2023

**Correctifs et améliorations**

- Correction d’un problème en raison duquel les éléments de données ne pouvaient pas être enregistrés dans le champ de remplacement de l’ID de conteneur de synchronisation des identifiants.

## Version 2.20.1 - 3 août 2023

**Correctifs et améliorations**

- Amélioration de la validation des paramètres de remplacement du train de données enregistré.

## Version 2.20.0 - 31 juillet 2023

**Nouvelles fonctionnalités**

- Ajout de la prise en charge des [remplacements par commande de l’identifiant de train de données](../../../../datastreams/overrides.md).

**Correctifs et améliorations**

- `edgeConfigId` est devenu obsolète et est remplacé par `datastreamId` dans la configuration du SDK.
- Plusieurs améliorations de l’expérience client pour la configuration du train de données qui remplace l’interface utilisateur.

## Version 2.19.0 - 21 juin 2023

- L’élément de données **[!UICONTROL Variable]** et les actions **[!UICONTROL Mettre à jour la variable]** sont désormais disponibles pour toutes les personnes utilisatrices.

## Version 2.18.0 - 18 mai 2023

- Contient la version 2.17.0 du SDK web d’Adobe Experience Platform.

## Version 2.17.0 - 25 avril 2023

**Nouvelles fonctionnalités**

- Contient la version 2.16.0 du SDK web d’Adobe Experience Platform.
- Ajout de la prise en charge des [remplacements de la configuration du train de données](/help/datastreams/overrides.md).
- Ajout d’un avis d’obsolescence à l’option `datasetId` de la commande `sendEvent`.

**Correctifs et améliorations**

- Correction d’un problème en raison duquel le défilement dans Safari fermait le sélecteur de train de données.

## Version 2.16.1 - 14 avril 2023

- Correction d’un problème lié aux éléments de données Objet XDM et Variable en raison duquel il était impossible de sélectionner un schéma dans une sandbox autre que la sandbox par défaut.

## Version 2.16.0 - 30 mars 2023

**Nouvelles fonctionnalités**

- (Beta) Ajout de l’action **[!UICONTROL Mettre à jour la variable]** et de l’élément de données **[!UICONTROL Variable]**.
- Ajout de la configuration pour la fonction de rappel [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).

**Correctifs et améliorations**

- Correction d’un problème en raison duquel le fait de cliquer sur les éléments d’une balise d’ancrage ne fonctionnait pas lors de l’utilisation de l’action **[!UICONTROL Rediriger avec l’identité]**.
- Correction d’un problème en raison duquel les éléments de données d’objet XDM ne fonctionnaient pas lorsqu’un seul schéma était présent.
- Contient la version 2.15.0 du SDK web d’Adobe Experience Platform.

## Version 2.15.1, - 26 Janvier 2023

- Correction d’un problème en raison duquel les utilisateurs et utilisatrices n’ayant pas accès aux flux de données ne pouvaient pas modifier la configuration de l’extension.
- Ajout de la prise en charge des surfaces dans l’action `sendEvent`.

Contient la version 2.14.0 du SDK Web Adobe Experience Platform.

## Version 2.14.1 - 13 octobre 2022

- Correction d’un problème dans lequel le SDK Web n’honore pas l’ID d’Experience Cloud ID Service.

Contient la version 2.13.1 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.14.0 - 28 septembre 2022

- Ajout d’une nouvelle configuration `targetMigrationEnabled` qui active la migration complète page par page.
- Ajout d’une action d’application de réponse pour activer les implémentations hybrides serveur-client.
- Ajout de l’option contextuelle des indices clients d’agent utilisateur à entropie élevée.

Contient la version 2.13.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.13.0 - 29 juin 2022

- Correction de l’ordre de tri des propriétés numériques dans l’élément de données d’objet XDM, telles que les eVars.

Contient la version 2.12.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.12.0 - 13 juin 2022

- Mise à jour de l’élement de données `identityMap` pour renseigner les options d’espace de noms en fonction des sandbox définis par les paramètres d’extension.
- Ajout de l’action **[!UICONTROL Redirection avec une identité]** pour permettre le partage d’identités inter-domaines.
- Ajout de liens vers de la documentation à l’action `sendEvent`.
- Mise à niveau de la bibliothèque de l’IU React Spectrum.
- Plusieurs améliorations de l’interface utilisateur.

Contient la version 2.11.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.11.2 - 3 mai 2022

Contient la version 2.10.1 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.11.1 - 22 avril 2022

- Correction de l’erreur de la commande de configuration de la version 2.11.0.

Contient la version 2.10.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.11.0 - 22 avril 2022

- Amélioration des performances de l’interface utilisateur des balises.
- Ajout de sélecteurs de sandbox à la configuration de l’extension de flux de données.

Contient la version 2.10.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.10.0 - 10 mars 2022

- Mise à jour de l’extrait de masquage préalable qui peut être copié sur la page de configuration pour fonctionner avec l’éditeur VEC d’Adobe Target mis à jour.

Contient la version 2.9.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.9.0 - 19 janvier 2022

Contient la version 2.8.0 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.8.0 - 26 octobre 2021

Contient la version 2.7.0 de la bibliothèque SDK Web Adobe Experience Platform.

- Des informations supplémentaires provenant d’Edge Network sont disponibles dans l’événement d’envoi d’événement terminé, notamment `inferences` et `destinations`. Le format de ces propriétés peut changer, car ces fonctionnalités sont actuellement déployées dans le cadre d’une version bêta.

## Version 2.7.3 - 7 septembre 2021

Contient la version 2.6.4 de la bibliothèque SDK Web Adobe Experience Platform.

- Il n’existe plus d’avertissement d’obsolescence pour `container.buildInfo.environment.`

## Version 2.7.0 - 16 août 2021

Contient la version 2.6.3 de la bibliothèque SDK Web Adobe Experience Platform.

- Lors de l’utilisation du type d’élément de données de mappage dʼidentités, les identifiants dont les ID se résolvent en valeurs qui ne sont pas des chaînes renseignées sont désormais automatiquement supprimés du mappage d’identités.
- Correction d’une erreur qui se produisait lors de la tentative d’enregistrement d’un élément de données à l’aide du type d’élément de données de l’objet XDM alors qu’aucun schéma n’était sélectionné.
- Amélioration de la typographie de l’interface utilisateur.

## Version 2.6.2 - 4 août 2021

Contient la version 2.6.2 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.6.1 - 29 juillet 2021

Contient la version 2.6.1 de la bibliothèque SDK Web Adobe Experience Platform.

## Version 2.6.0 - 27 juillet 2021

Contient la version 2.6.0 de la bibliothèque SDK Web Adobe Experience Platform.

- Les étiquettes, descriptions et messages d’erreur utilisant le terme Configuration de périphérie ont été modifiés afin d’utiliser le terme Flux de données pour s’aligner sur la terminologie Adobe Experience Platform la plus récente.
- Dans la vue de configuration de l’extension, la prise en charge a été ajoutée pour la gestion d’un grand nombre de flux de données et d’environnements de flux de données.
- Dans la vue d’élément de données de l’objet XDM, la prise en charge de la gestion d’un grand nombre de schémas a été ajoutée.
- Un type d’événement d’envoi d’événement terminé a été ajouté, qui peut être utilisé pour exécuter une règle après l’envoi d’un événement au serveur et la réception d’une réponse. D’autres documents seront bientôt disponibles.
- Le type d’événement de décisions reçues a été abandonné. Utilisez plutôt le type d’événement d’envoi d’événement terminé.
- De manière générale, l’interface utilisateur et la gestion des erreurs ont été améliorées.

## Version 2.5.0 - 1er juin 2021

Contient la version 2.5.0 de la bibliothèque SDK Web Adobe Experience Platform.

- Ajout d’un champ `data` à l’action Envoyer l’événement. La documentation à venir décrit l’utilisation de cette fonctionnalité dans certains scénarios.
- Sur la vue d’élément de données de l’objet XDM, le problème suivant a été corrigé : une erreur était générée si l’utilisateur avait accès aux sandbox Adobe Experience Platform, mais pas au sandbox configuré par défaut pour l’organisation.
- Sur la vue d’élément de données de l’objet XDM, le problème suivant a été corrigé : un champ de schéma obligatoire était considéré comme non valide, même si l’objet parent ne contenait aucune valeur.

## Version 2.4.0 - 9 mars 2021

Contient la version 2.4.0 de la bibliothèque SDK Web Adobe Experience Platform.

- Ajout de la case à cocher [« Déchargement de document »](/help/web-sdk/commands/sendevent/documentunloading.md) à l’interface d’utilisation de l’action Envoyer l’événement.
- Ajout de la prise en charge d’une option `out` lors de la [configuration du consentement par défaut](/help/web-sdk/commands/configure/defaultconsent.md) qui supprime tous les événements jusqu’à ce que le consentement soit reçu (l’option `pending` existante met les événements en file d’attente et les envoie une fois le consentement reçu).
- Ajout d’une info-bulle au champ de consentement par défaut.
- Ajout de la prise en charge de la norme de consentement 2.0 d’Adobe lors de l’utilisation de la commande [`setConsent`](/help/web-sdk/commands/setconsent.md).
- Une erreur mieux formulée s’affiche désormais dans l’interface utilisateur de l’élément de données de l’objet XDM si le jeton d’accès de l’utilisateur n’est pas valide ou a été configuré de manière incorrecte.
- Correction d’une erreur d’origine croisée (n’affectant pas le fonctionnement de l’extension) qui s’affichait sur la Developer Console du navigateur lors de l’affichage d’un élément de données de l’objet XDM.

## Version 2.3.0 - 4 novembre 2020

Contient la version 2.3.0 de la bibliothèque SDK Web Adobe Experience Platform.

- Ajout de la prise en charge de l’utilisation d’un élément de données lors de la configuration du consentement par défaut.
- Ajout de la possibilité de rechercher des schémas XDM avec le type d’élément de données Objet XDM.
- Ajout du clonage des données XDM dans le type d’action ‘Envoyer l’événement’ pour s’assurer que les modifications ultérieures apportées à l’objet de données XDM ne seront pas prises en compte dans la requête.

## Version 2.2.0 - 1er octobre 2020

- Lorsque les clients et les clientes tentaient de créer un objet XDM à partir de schémas sandbox, ils rencontraient des problèmes d’authentification. L’API qui appelle Platform prend désormais en charge les environnements, de sorte que les utilisateurs ne reçoivent que les schémas qu’ils sont autorisés à modifier.
- Lors de l’utilisation de l’élément de données `identityMap`, les espaces de noms sont maintenant préremplis dans une liste déroulante, ce qui évite d’avoir à les remplir manuellement.
- Optimisation de l’interface utilisateur pour l’élément de données `xdmObject`. Dans la nouvelle interface utilisateur, vous pouvez identifier les champs qui ont été renseignés sans avoir à entrer chaque élément dans l’objet.

## Version 2.1.1 - 26 août 2020

- Correction d’un problème en raison duquel les sandbox Adobe Experience Platform sur la vue Objet XDM s’affichaient incorrectement. Si, lors de l’utilisation de cette version de l’extension, un sandbox attendu n’est pas affiché dans la liste, l’utilisateur doit vérifier auprès de son administrateur Adobe Experience Platform pour s’assurer que les autorisations d’accès sont correctement définies.

## Version 2.1.0 - 5 août 2020

- Changement important : supprimez l’action `syncIdentity` et privilégiez plutôt le transfert de ces identifiants vers l’action `sendEvent`. Veuillez désactiver toute règle existante qui utilise cette action avant de mettre à niveau votre extension.
- Mise à jour vers Alloy v. 2.1.0 ([Notes de mise à jour](/help/web-sdk/release-notes.md))
- Prise en charge de la norme de consentement IAB 2.0 dans l’action `setConsent`.
- Prise en charge du remplacement de l’identifiant de jeu de données dans l’action `sendEvent`.
- Ajout d’un nouvel élément de données de type `IdentityMap` qui peut être utilisé pour renseigner l’entrée `identityMap` dans l’élément de données de l’objet XDM (qui est maintenant activé) et dans l’action `setConsent`.
- Prise en charge de la transmission d’une carte d’identité dans l’action `setConsent`.
- Prise en charge du choix d’un sandbox Platform dans l’élément de données de l’objet XDM.

## Version 1.0.0 - 26 mai 2020

- Prise en charge de la sélection de l’environnement à partir du service de configuration.

## Version 0.1.2 - 4 mai 2020

- Renommé `configId` en `edgeConfigId`.
- Renommé `viewStart` en `renderDecisions`, défini sur false par défaut. Si la valeur est définie sur true, les offres de personnalisation sont récupérées et rendues automatiquement.
- Changements liés à `Get Decisions` :
   - Suppression de la commande `getDecisions`.
   - Ajout d’une option `scopes` à la commande `sendEvent`. Les décisions sont renvoyées dans la promesse `sendEvent` résolue.
   - Ajout d’une portée intégrée `__view__` qui résultera en un renvoi d’offres à l’échelle de la page/vue. (Offres du compositeur d’expérience visuelle dans Target, par exemple).
Ces décisions sont renvoyées à partir de la commande `sendEvent` uniquement si `renderDecisions` est défini sur false.
   - Ajout d’un événement `Decisions Received`, qui se déclenche lorsque des décisions deviennent disponibles.
- Combinaison de plusieurs notifications de personnalisation sous un seul appel de serveur.
- Correction d’un problème en raison duquel l’ID de fusion des événements était réinitialisé chaque fois que l’élément de données était référencé.
- L’action `setCustomerIds` a été renommée `syncIdentity`.
- Ajout d’une commande `getIdentity`. Pour l’instant, elle ne peut être consommée que via du Custom Code (code personnalisé).
- L’activation du débogage à l’aide de `_satellite` active maintenant le débogage dans le SDK Web Adobe Experience Platform.
- Ajout de la prise en charge des valeurs saisies dans l’objet XDM : booléens, nombres et décimales.

## Version 0.0.10 - 16 mars 2020

- Combinaison des concepts opt-in et opt-out sous `Consent` et ajout d’une nouvelle commande `setConsent`.
- Ajout d’un nouvel élément de données de type `XDM Object` qui permet le mappage de JavaScript/JSON à XDM.

## Version 0.0.7 - 18 février 2020

- Les options idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled et cookieDestinationsEnabled ont été supprimées.
- Les tirets sont maintenant pris en charge dans la valeur de l’option edgeDomain.
- La requête effectuée lors de la migration des identifiants est envoyée au point d’entrée demdex afin d’améliorer l’identification inter-domaines lorsque le cookie demdex n’est pas défini.
- La requête effectuée lors de la migration des identifiants attend toujours une réponse afin de s’assurer que le cookie d’identité est défini.
- Lors de l’exécution d’une commande non valide, une liste de noms de commande valides sera enregistrée dans la console.
- Ajout d’une case à cocher afin d’activer ou de désactiver la prise en charge des cookies tiers dans l’extension de balises. Cela désactive les appels vers demdex.net.

## Version 0.0.5 - 20 décembre 2019

- Ajout des configurations de suivi d’activité à l’extension de balises
- Exposition d’EventType et EventMergeId sur la commande d’événement.
- Ajout d’une configuration onBeforeEventSend à l’extension de balises
- Ajout d’une configuration edgeBasePath à l’extension de balises

## Version 0.0.3 - 25 novembre 2019

- Nouveaux champs ID de fusion et Type dans l’action Envoyer un événement. L’ID de fusion est mappé sur `xdm.eventMergeID` et le Type est mappé sur `xdm.eventType` dans le schéma XDM.

## Version 0.0.2 - 18 novembre 2019

- Version initiale
