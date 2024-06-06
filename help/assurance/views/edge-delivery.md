---
title: Vue de la diffusion Edge
description: Ce guide contient des informations détaillées sur la vue Edge Delivery dans Adobe Experience Platform Assurance.
source-git-commit: d6b5894a5c5ba3907a8e6dd0d1864f773dd6325c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---

# Vue Edge Delivery dans Assurance

La variable **[!UICONTROL Diffusion Edge]** afficher à l’intérieur **[!UICONTROL Adobe Experience Platform Assurance]** permet d’inspecter et de valider [!UICONTROL AJO entrant] Diffusion de messages de périphérie vers vos applications web et mobiles. Ce mode est particulièrement utile pour résoudre les problèmes liés à la diffusion de [!UICONTROL AJO entrant] campagnes et parcours web et mobiles.

## Commencer

Avant de poursuivre, vérifiez que vous avez accès aux services suivants :

- La variable [Interface utilisateur de la collecte de données Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Pour savoir comment installer **[!UICONTROL Assurance]** dans votre application, veuillez lire la [guide d’assurance d’implémentation](../tutorials/implement-assurance.md).

## Utilisation de l’assurance avec la diffusion Edge

Une fois que vous avez ouvert une **[!UICONTROL Assurance]** vous pouvez ajouter la fonction **[!UICONTROL Diffusion Edge]** afficher à **[!UICONTROL Assurance]**. Au bas du panneau de gauche, sélectionnez **[!UICONTROL Configurer]** pour ajouter la variable **[!UICONTROL Diffusion Edge]** afficher et **Enregistrer** c&#39;est le cas.

![Ajoutez le plug-in en sélectionnant Configurer en bas à gauche.](./images/edge-delivery/add-plugin.png)

Une fois l’ajout effectué, sélectionnez la variable **[!UICONTROL Diffusion Edge]** dans la **[!UICONTROL Adobe Journey Optimizer]** pour valider la diffusion entrante Edge.

![La diffusion Edge est accessible dans le groupe de vues Adobe Journey Optimizer](./images/edge-delivery/ajo-plugins.png)

## Liste de requêtes

Dans le volet principal de la vue, la liste des demandes de diffusion Edge s’affiche. Cette liste affiche toutes les [!UICONTROL AJO entrant] demandes effectuées à Experience Edge et traitées par la variable **[!UICONTROL Service de diffusion entrante]**, y compris les demandes de récupération des décisions de personnalisation, ainsi que le suivi des interactions de proposition de personnalisation (affichage, clic, déclenchement ou abandon, par exemple).

Les requêtes sont triées par horodatage, les requêtes les plus récentes se trouvant en haut. Outre l’horodatage, la liste comprend également une colonne ID de demande, ainsi qu’un Type de demande, qui peut être l’un des suivants :

- **[!UICONTROL Diffusion d’expérience]**: une requête pour récupérer les décisions de personnalisation ;
- **[!UICONTROL Interactions d’expérience]**: demande de suivi des interactions de proposition de personnalisation
- **[!UICONTROL Diffusion d’expérience et interactions]**: une requête pour récupérer les décisions de personnalisation, y compris les interactions de propositions de personnalisation ;
- **[!UICONTROL Prévisualiser la diffusion]**: une requête pour récupérer les décisions de personnalisation de prévisualisation

Les requêtes peuvent également être filtrées en saisissant un terme de recherche dans la barre de recherche située en haut de la liste. Cela s’avère utile lors du filtrage selon des valeurs spécifiques, telles que les identifiants.

![La liste des requêtes entrantes s’affiche dans la vue principale.](./images/edge-delivery/request-list.png)

## Affichage détaillé des requêtes

Une fois qu’une requête est sélectionnée dans la vue principale, des informations détaillées sur la requête sélectionnée s’affichent à droite. Cette vue comprend les sections suivantes :

### Présentation des requêtes

Cette section donne un aperçu général de la requête sélectionnée, y compris : [!UICONTROL ID d’organisation], [!UICONTROL Grappe Edge], [!UICONTROL ID de demande] et [!UICONTROL Type de requête], [!UICONTROL ID de sandbox], [!UICONTROL Nom du sandbox], [!UICONTROL Identifiant du flux de données], ainsi que la liste des surfaces de requête en cas de [!UICONTROL Diffusion d’expérience] requêtes.

![La section Présentation de la requête fournit des détails de requête de haut niveau.](./images/edge-delivery/request-overview.png)

### Profile

Cette section fournit des informations sur les données de profil utilisées lors du traitement de la demande, notamment le mappage d’identité, l’appartenance au segment et les paramètres de consentement.\
La variable [!UICONTROL Profil] est très utile lorsque des problèmes de dépannage tels que la diffusion ne fonctionnent pas comme prévu en raison de paramètres d’adhésion aux segments manquants ou retardés ou de consentement pour l’exclusion.

![La section Profil comprend le mappage d’identité, l’appartenance au segment et les paramètres de consentement.](./images/edge-delivery/profile.png)

### Activités qualifiées

Cette section fournit une liste des activités qui ont été qualifiées pour la requête sélectionnée, notamment le type d’activité, les identifiants, l’espace de noms d’identité, les surfaces, la planification et les audiences. Vous trouverez des informations plus détaillées sur l’activité dans la section [section trace d’exécution brute](#execution).

![La section Activités qualifiées contient les détails des activités qualifiées](./images/edge-delivery/qualified-activities.png)

### Activités non qualifiées

Cette section fournit une liste des activités qui ont été exclues de la qualification. Outre le type d’activité, les identifiants, les espaces de noms d’identité, les surfaces, les plannings et les audiences, cette section comprend également une liste des raisons pour lesquelles l’activité n’a pas été qualifiée.

![La section sur les activités non qualifiées contient des informations sur les activités non qualifiées et des raisons d&#39;exclusion.](./images/edge-delivery/unqualified-activities.png)

### Détails du message

Cette section fournit des informations détaillées sur les messages qui ont été remis pour la requête sélectionnée. Il comprend les ID de message, les fragments, les stratégies de décision, [!UICONTROL Offer decisioning] , ainsi que le contexte de sélection des messages.

![Section contenant les détails des messages envoyés, tels que les ID de message et le contexte de sélection, les fragments, les stratégies de décision et les paramètres de prise de décision](./images/edge-delivery/message-details.png)

### Interactions

Cette section fournit des informations détaillées sur les interactions qui ont été suivies dans la requête sélectionnée. Il inclut le type d’interaction (sous `propositionEventType`), ainsi que les métadonnées de proposition associées, telles que les métadonnées d’activité (sous `scopeDetails.activity`) et jeton d’événement de proposition (dans `scopeDetails.characteristics.eventToken`).

![Les interactions sont suivies au moyen de jetons de proposition et de métadonnées d’activité associées.](./images/edge-delivery/interactions.png)

### Les traces brutes

Cette section fournit les traces brutes de la requête sélectionnée. Elle inclut la trace complète de la demande, y compris la demande réelle telle qu’elle a été reçue dans **[!UICONTROL Service de diffusion entrante]**, trace d’exécution et trace de réponse. Cela s’avère utile pour le dépannage avancé, tel que la diffusion ne fonctionnant pas comme prévu en raison de l’indisponibilité du service de diffusion, de données manquantes ou incorrectes, ou pour comprendre le flux complet du traitement des demandes.

#### Requête

La trace de la requête inclut la requête complète telle qu’elle a été reçue par la fonction **[!UICONTROL Service de diffusion entrante]** **[!UICONTROL Konductor]** en amont. Il inclut les en-têtes de requête, le corps et d’autres métadonnées. Par exemple, le payload XDM de la requête peut être inspecté dans la variable `event.body.xdm` champ .

![Vous trouverez des informations détaillées sur les requêtes, y compris les en-têtes et le corps, dans la trace de requête.](./images/edge-delivery/request.png)

#### Exécution

La trace de l’exécution inclut la trace complète de la requête telle qu’elle a été traitée par le **[!UICONTROL Service de diffusion entrante]**. Il affiche le contexte d’exécution, la qualification de l’activité, la sélection des messages et d’autres étapes de traitement. Les erreurs ou avertissements qui se sont produits pendant le traitement de la requête se trouvent dans `context.messages` et `context.exceptions` des champs. Vous trouverez des informations détaillées sur la qualification des activités dans la section `context.qualifiedActivitiesDetailed` et `context.unqualifiedActivitiesDetailed` des champs.

![Le suivi d’exécution comprend le contexte d’exécution, la qualification de l’activité, la sélection des messages et d’autres détails de traitement.](./images/edge-delivery/execution.png)

#### Réponse

La trace de la réponse inclut la réponse complète, car elle a été renvoyée par **[!UICONTROL Service de diffusion entrante]** en aval vers **[!UICONTROL Konductor]**. Il comprend les en-têtes de réponse, le corps et d’autres métadonnées. Le corps complet de la réponse peut être inspecté en copiant le message avec l’identifiant `1` dans le Presse-papiers à l’aide de la fonction **[!UICONTROL Copier la valeur]** et de le coller dans une visionneuse JSON.

![La trace de réponse contient le corps de réponse complet renvoyé en aval](./images/edge-delivery/response.png)
