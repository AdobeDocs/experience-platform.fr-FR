---
title: Vue Edge Delivery
description: Ce guide contient des informations détaillées sur la vue Edge Delivery dans Adobe Experience Platform Assurance.
exl-id: 570c1bcb-ec6d-465e-84ff-ed910d4f7e8a
source-git-commit: a11f469cb54421e0ca30c7c5878128e216470f7f
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---

# Vue Edge Delivery dans Assurance

La vue **[!UICONTROL Edge Delivery]** à l’intérieur de **[!UICONTROL Adobe Experience Platform Assurance]** permet d’inspecter et de valider la diffusion de messages [!UICONTROL AJO Inbound] vers vos applications web et mobiles. Cet affichage est particulièrement utile pour résoudre les problèmes liés à la diffusion de parcours et campagnes web et mobiles [!UICONTROL AJO Inbound].

## Commencer

Avant de poursuivre, vérifiez que vous avez accès aux services suivants :

- [Interface utilisateur de collecte de données Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Pour savoir comment installer **[!UICONTROL Assurance]** dans votre application, consultez le [guide d’assurance d’implémentation](../tutorials/implement-assurance.md).

## Utilisation de l’assurance avec Edge Delivery

Une fois que vous avez ouvert une session **[!UICONTROL Assurance]**, vous pouvez ajouter la vue **[!UICONTROL Edge Delivery]** à **[!UICONTROL Assurance]**. Au bas du panneau de gauche, sélectionnez **[!UICONTROL Configurer]** pour ajouter la vue **[!UICONTROL Edge Delivery]** et **Enregistrer**.

![Ajoutez le module externe en sélectionnant Configurer en bas à gauche](./images/edge-delivery/add-plugin.png)

Une fois ajouté, sélectionnez la vue **[!UICONTROL Edge Delivery]** dans la section **[!UICONTROL Adobe Journey Optimizer]** pour valider la diffusion entrante Edge.

![Edge Delivery est accessible dans le groupe de vues Adobe Journey Optimizer](./images/edge-delivery/ajo-plugins.png)

## Liste de requêtes

Dans le volet principal de la vue, la liste des demandes de diffusion Edge s’affiche. Cette liste répertorie toutes les requêtes [!UICONTROL AJO entrantes] envoyées à Experience Edge et traitées par le ****, y compris les requêtes de récupération des décisions de personnalisation, ainsi que le suivi des interactions de proposition de personnalisation (affichage, clic, déclenchement ou abandon, par exemple).

Les requêtes sont triées par horodatage, les requêtes les plus récentes se trouvant en haut. Outre l’horodatage, la liste comprend également une colonne ID de demande, ainsi qu’un Type de demande, qui peut être l’un des suivants :

- **[!UICONTROL Diffusion d’expérience]** : une requête pour récupérer les décisions de personnalisation
- **[!UICONTROL Interactions d’expérience]** : demande de suivi des interactions de propositions de personnalisation
- **[!UICONTROL Diffusion d’expérience et interactions]** : demande de récupération des décisions de personnalisation comprenant également des interactions de propositions de personnalisation
- **[!UICONTROL Preview Delivery]** : demande de récupération des décisions de personnalisation de prévisualisation

Les requêtes peuvent également être filtrées en saisissant un terme de recherche dans la barre de recherche située en haut de la liste. Cela s’avère utile lors du filtrage selon des valeurs spécifiques, telles que les identifiants.

![La liste des requêtes entrantes s’affiche dans la vue principale](./images/edge-delivery/request-list.png)

## Affichage détaillé des requêtes

Une fois qu’une requête est sélectionnée dans la vue principale, des informations détaillées sur la requête sélectionnée s’affichent à droite. Cette vue comprend les sections suivantes :

### Présentation des requêtes

Cette section donne un aperçu général de la requête sélectionnée, y compris [!UICONTROL ID d’organisation], [!UICONTROL cluster Edge], [!UICONTROL ID de requête] et [!UICONTROL Type de requête], [!UICONTROL ID de sandbox], [!UICONTROL Nom de sandbox], [!UICONTROL ID de requête], ainsi que la liste des surfaces de requête Cas des demandes [!UICONTROL Diffusion d’expérience].

![La section de présentation des requêtes fournit des détails de requête de haut niveau](./images/edge-delivery/request-overview.png)

### Profile

Cette section fournit des informations sur les données de profil utilisées lors du traitement de la demande, notamment le mappage d’identité, l’appartenance au segment et les paramètres de consentement.\
La section [!UICONTROL Profil] s’avère très utile pour résoudre des problèmes tels que le dysfonctionnement de la diffusion en raison de paramètres d’adhésion au segment manquants ou retardés ou de consentement pour l’exclusion.

![ La section Profil comprend la carte d’identité, l’adhésion au segment et les paramètres de consentement ](./images/edge-delivery/profile.png)

### Activités qualifiées

Cette section fournit une liste des activités qui ont été qualifiées pour la requête sélectionnée, notamment le type d’activité, les identifiants, l’espace de noms d’identité, les surfaces, la planification et les audiences. Vous trouverez des informations plus détaillées sur l’activité dans la [section trace d’exécution brute](#execution).

![La section Activités qualifiées contient les détails des activités qualifiées](./images/edge-delivery/qualified-activities.png)

### Activités non qualifiées

Cette section fournit une liste des activités qui ont été exclues de la qualification. Outre le type d’activité, les identifiants, les espaces de noms d’identité, les surfaces, les plannings et les audiences, cette section comprend également une liste des raisons pour lesquelles l’activité n’a pas été qualifiée.

![ La section sur les activités non qualifiées contient des détails sur les activités non qualifiés et des raisons d&#39;exclusion](./images/edge-delivery/unqualified-activities.png)

### Détails du message

Cette section fournit des informations détaillées sur les messages qui ont été remis pour la requête sélectionnée. Il inclut les identifiants de message, les fragments, les stratégies de décision, les paramètres [!UICONTROL Offer decisioning], ainsi que le contexte de sélection des messages.

![ Section contenant des détails sur les messages diffusés tels que les ID de message et le contexte de sélection, les fragments, les stratégies de décision et les paramètres de prise de décision ](./images/edge-delivery/message-details.png)

### Interactions

Cette section fournit des informations détaillées sur les interactions qui ont été suivies dans la requête sélectionnée. Il comprend le type d’interaction (sous `propositionEventType`), ainsi que les métadonnées de proposition associées, telles que les métadonnées d’activité (sous `scopeDetails.activity`) et le jeton d’événement de proposition (dans `scopeDetails.characteristics.eventToken`).

![Les interactions sont suivies par le biais de jetons de proposition et de métadonnées d’activité associées](./images/edge-delivery/interactions.png)

### Les traces brutes

Cette section fournit les traces brutes de la requête sélectionnée. Elle inclut la trace complète de la requête, y compris la requête réelle telle qu’elle a été reçue dans **[!UICONTROL Inbound Delivery Service]**, la trace de l’exécution et la trace de la réponse. Cela s’avère utile pour le dépannage avancé, tel que la diffusion ne fonctionnant pas comme prévu en raison de l’indisponibilité du service de diffusion, de données manquantes ou incorrectes, ou pour comprendre le flux complet du traitement des demandes.

#### Requête

Le suivi de la requête inclut la demande complète telle qu’elle a été reçue par le **[!UICONTROL service de remise en entrée]** **[!UICONTROL Konductor]** en amont. Il inclut les en-têtes de requête, le corps et d’autres métadonnées. Par exemple, la charge utile XDM de la requête peut être inspectée dans le champ `event.body.xdm` .

![ Des informations détaillées sur les requêtes, y compris les en-têtes et le corps, se trouvent dans la trace de requête](./images/edge-delivery/request.png)

#### Exécution

La trace de l’exécution inclut la trace complète de la demande telle qu’elle a été traitée par le **[!UICONTROL Inbound Delivery Service]**. Il affiche le contexte d’exécution, la qualification de l’activité, la sélection des messages et d’autres étapes de traitement. Les erreurs ou avertissements qui se sont produits pendant le traitement de la requête se trouvent dans les champs `context.messages` et `context.exceptions` . Vous trouverez des informations détaillées sur la qualification des activités dans les champs `context.qualifiedActivitiesDetailed` et `context.unqualifiedActivitiesDetailed` .

![Le suivi de l’exécution comprend le contexte d’exécution, la qualification de l’activité, la sélection des messages et d’autres détails de traitement](./images/edge-delivery/execution.png)

#### Réponse

La trace de la réponse inclut la réponse complète, car elle a été renvoyée par **[!UICONTROL Inbound Delivery Service]** en aval de **[!UICONTROL Konductor]**. Il comprend les en-têtes de réponse, le corps et d’autres métadonnées. Le corps complet de la réponse peut être inspecté en copiant le message avec l’ID `1` dans le Presse-papiers à l’aide du bouton **[!UICONTROL Copier la valeur]** et en le collant dans une visionneuse JSON.

![La trace de réponse contient le corps de réponse complet renvoyé en aval](./images/edge-delivery/response.png)
