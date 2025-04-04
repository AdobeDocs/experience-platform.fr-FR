---
title: Types d’actions dans l’extension Adobe Experience Platform Web SDK
description: Découvrez les différents types d’actions fournis par l’extension de balises Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 2%

---


# Types d’actions

Après avoir configuré l’extension de balise [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), vous devez configurer vos types d’action.

Cette page décrit les types d’actions pris en charge par l’extension de balises [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md).

## Appliquer les propositions {#apply-propositions}

Le type d’action **[!UICONTROL Appliquer des propositions]** vous permet d’effectuer le rendu des propositions dans des applications d’une seule page sans incrémenter de mesures.

Ce type d’action est utile lorsque vous travaillez avec des applications monopages où des parties de la page sont rendues de nouveau, ce qui peut remplacer toutes les personnalisations déjà appliquées à la page.

Vous pouvez utiliser ce type d’action pour différents cas d’utilisation, tels que :

1. **Rendu des offres de mbox HTML**. Les propositions explicitement demandées via une portée ou une surface à partir d’une action **[!UICONTROL Envoyer l’événement]** ne sont pas automatiquement rendues. Vous pouvez utiliser le type d’action **[!UICONTROL Appliquer des propositions]** pour indiquer à Web SDK où effectuer leur rendu en spécifiant les métadonnées de proposition.
2. **Effectuez le rendu des offres pour une vue sur une application monopage**. Lors du rendu d’un événement de changement de vue, si les données d’analyse ne sont pas encore prêtes, vous pouvez utiliser l’action **[!UICONTROL Appliquer les propositions]** pour effectuer le rendu des propositions d’affichage en haut de la page. Voir [événements en haut et en bas de la page (Deuxième page vue - Option 2)](../../../../web-sdk/use-cases/top-bottom-page-events.md) pour plus d’informations. Pour l&#39;utiliser, saisissez un **[!UICONTROL Nom de la vue]** dans le formulaire.
3. **Restituer des propositions**. Lorsque votre site utilise un framework comme React pour effectuer à nouveau le rendu du contenu, vous devrez peut-être appliquer une nouvelle personnalisation. Dans ce cas, vous pouvez utiliser le type d&#39;action **[!UICONTROL Appliquer les propositions]**.

Ce type d’action n’envoie pas d’événement d’affichage pour les propositions rendues. Il effectue le suivi des propositions générées afin qu’elles puissent être incluses dans les appels **[!UICONTROL Envoyer l’événement]** suivants.


![L’interface utilisateur d’Experience Platform Tags affiche le type d’action Appliquer les propositions.](assets/apply-propositions.png)

Ce type d&#39;action prend en charge les champs suivants :

* **[!UICONTROL Propositions]** : tableau d’objets de proposition dont vous souhaitez effectuer à nouveau le rendu.
* **[!UICONTROL Nom de la vue]** : nom de la vue dont le rendu doit être effectué.
* **[!UICONTROL Métadonnées de proposition]** : objet qui détermine la manière dont les offres HTML peuvent être appliquées. Vous pouvez fournir ces informations par le biais du formulaire ou d’un élément de données. Il contient les propriétés suivantes :
   * **[!UICONTROL Périmètre]**
   * **[!UICONTROL Sélecteur]**
   * **[!UICONTROL Type d’action]**

## Appliquer la réponse {#apply-response}

Utilisez le type d’action **[!UICONTROL Appliquer la réponse]** lorsque vous souhaitez effectuer diverses actions en fonction d’une réponse d’Edge Network. Ce type d’action est généralement utilisé dans les déploiements hybrides où le serveur effectue un appel initial à l’Edge Network, puis ce type d’action prend la réponse de cet appel et initialise le SDK Web dans le navigateur.

L’utilisation de ce type d’action peut réduire les temps de chargement des clients pour les cas d’utilisation de personnalisation hybride.

![Image de l’interface utilisateur d’Experience Platform affichant le type d’action Appliquer la réponse.](assets/apply-response.png)

Ce type d’action prend en charge les options de configuration suivantes :

* **[!UICONTROL Instance]** : sélectionnez l’instance Web SDK que vous utilisez.
* **[!UICONTROL En-têtes de réponse]** : sélectionnez l’élément de données qui renvoie un objet contenant les clés et les valeurs d’en-tête renvoyées par l’appel au serveur Edge Network.
* **[!UICONTROL Corps de la réponse]** : sélectionnez l’élément de données qui renvoie l’objet contenant la payload JSON fournie par la réponse Edge Network.
* **[!UICONTROL Rendre les décisions de personnalisation visuelle]** : activez cette option pour effectuer automatiquement le rendu du contenu de personnalisation fourni par Edge Network et pré-masquer le contenu pour éviter le scintillement.

## Évaluation d’ensembles de règles {#evaluate-rulesets}

Ce type d’action déclenche manuellement l’évaluation de l’ensemble de règles. Les ensembles de règles sont renvoyés par Adobe Journey Optimizer pour prendre en charge des fonctionnalités telles que les messages dans le navigateur.

![Image de l’interface utilisateur d’Experience Platform affichant le type d’action de réponse Évaluer des ensembles de règles.](assets/evaluate-rulesets.png)

Ce type d’action prend en charge les options suivantes :

* **[!UICONTROL Rendre les décisions de personnalisation visuelle]** : activez cette option pour rendre les décisions de personnalisation visuelle pour les éléments d’ensemble de règles qui correspondent.
* **[!UICONTROL Contexte de décision]** : il s’agit d’un mappage clé-valeur utilisé lors de l’évaluation des ensembles de règles Adobe Journey Optimizer pour la prise de décision sur l’appareil. Vous pouvez fournir le contexte de décision manuellement ou par le biais d&#39;un élément de données.

## Obtention du suivi Media Analytics {#get-media-analytics-tracker}

Cette action est utilisée pour obtenir l’API Media Analytics héritée. Lors de la configuration de l’action et si un nom d’objet est fourni, l’API Media Analytics héritée est exportée vers cet objet de fenêtre. Si aucun n’est fourni, il est exporté vers `window.Media` comme le fait la bibliothèque JS Media actuelle.

![Image de l’interface utilisateur d’Experience Platform montrant le type d’action Get Media Analytics Tracker.](assets/get-media-analytics-tracker.png)

## Rediriger avec identité {#redirect-with-identity}

Utilisez ce type d’action pour partager des identités de la page active vers d’autres domaines. Cette action est conçue pour être utilisée avec un type d’événement **[!UICONTROL click]** et une condition de comparaison de valeurs. Voir [Ajouter une identité à l’URL à l’aide de l’extension Web SDK](../../../../web-sdk/commands/appendidentitytourl.md#extension) pour plus d’informations sur l’utilisation de ce type d’action.

## Événement d’envoi {#send-event}

Envoie un événement à Experience Platform afin qu’Experience Platform puisse collecter les données envoyées et agir sur ces informations. Toutes les données que vous souhaitez envoyer peuvent être envoyées dans le champ **[!UICONTROL Données XDM]**. Utilisez un objet [!DNL JSON] conforme à la structure de votre schéma [!DNL XDM]. Cet objet peut être créé sur votre page ou par le biais d’un **[!UICONTROL Code personnalisé]** **[!UICONTROL Élément de données]**.

Le type d’action **[!UICONTROL Envoyer l’événement]** prend en charge les champs et paramètres décrits ci-dessous. Ces champs sont tous facultatifs.

### Paramètres des instances {#instance}

Utilisez le sélecteur **[!UICONTROL Instance]** pour choisir l’instance Web SDK à configurer. Si vous n’avez qu’une seule instance, elle est présélectionnée.

![Image de l’interface utilisateur Experience Platform Tags montrant les paramètres d’instance pour le type d’action Envoyer l’événement.](assets/instance-settings.png)

* **[!UICONTROL Instance]** : sélectionnez l’instance Web SDK à configurer. Si vous n’avez qu’une seule instance, elle sera présélectionnée.
* **[!UICONTROL Utiliser des événements guidés]** : activez cette option pour remplir ou masquer automatiquement certains champs afin d’activer un cas d’utilisation particulier. L’activation de cette option déclenche l’affichage des paramètres suivants.
   * **[!UICONTROL Demander une personnalisation]** : cet événement est conçu pour être appelé en haut de la page. Lorsqu’il est sélectionné, cet événement définit les champs suivants :
      * **[!UICONTROL Type]** : **[!UICONTROL Récupération De Proposition De Prise De Décision]**
      * **[!UICONTROL Envoyer automatiquement un événement d&#39;affichage]** : **[!UICONTROL false]**
      * Dans ce cas, pour effectuer automatiquement le rendu de la personnalisation, activez l’option **[!UICONTROL Rendre les décisions de personnalisation visuelle]**.
   * **[!UICONTROL Collecter des analyses]** : cet événement doit être appelé au bas de la page. Lorsqu’il est sélectionné, cet événement définit les champs suivants :
      * **[!UICONTROL Inclure les propositions rendues]** : **[!UICONTROL true]**
      * Les paramètres **[!UICONTROL Personalization]** sont masqués

  >[!NOTE]
  >
  >Les événements guidés sont liés aux [événements en haut et en bas de page](../../../../web-sdk/use-cases/top-bottom-page-events.md).


### Données {#data}

![Image de l’interface utilisateur Experience Platform Tags montrant les paramètres d’élément de données pour le type d’action Envoyer l’événement.](assets/data.png)

* **[!UICONTROL Type]** : ce champ vous permet de spécifier un type d’événement qui sera enregistré dans votre schéma XDM. Voir [`type`](/help/web-sdk/commands/sendevent/type.md) dans la commande `sendEvent` pour plus d’informations.
* **[!UICONTROL XDM]** :
* **[!UICONTROL Données]** : utilisez ce champ pour envoyer des données qui ne correspondent pas à un schéma XDM. Ce champ est utile si vous tentez de mettre à jour un profil Adobe Target ou d’envoyer des attributs de recommandations Target. Voir [`data`](/help/web-sdk/commands/sendevent/data.md) dans la commande `sendEvent` pour plus d’informations.
* **[!UICONTROL Inclure les propositions rendues]** : activez cette option pour inclure toutes les propositions rendues, mais qu’aucun événement d’affichage n’a été envoyé. Utilisez-la conjointement avec **[!UICONTROL Envoyer automatiquement un événement d’affichage]** désactivé. Ce paramètre met à jour le champ XDM `_experience.decisioning` avec des informations sur les propositions générées.
* **[!UICONTROL Le document sera déchargé]** : activez cette option pour vous assurer que les événements atteignent le serveur même si l’utilisateur quitte la page. Cela permet aux événements d’atteindre le serveur, mais les réponses sont ignorées.
* **[!UICONTROL ID de fusion]** : **ce champ est obsolète**. Cette opération renseigne le champ XDM `eventMergeId`.

### Personnalisation {#personalization}

![Image de l’interface utilisateur Experience Platform Tags montrant les paramètres Personalization pour le type d’action Envoyer l’événement.](assets/personalization-settings.png)

* **[!UICONTROL Portées]** : sélectionnez les portées ([!DNL mboxes] Adobe Target) que vous souhaitez demander explicitement à la personnalisation. Vous pouvez saisir les portées manuellement ou en fournissant un élément de données.
* **[!UICONTROL Surfaces]** : définissez les surfaces web qui sont disponibles sur la page pour la personnalisation. Pour plus d’informations](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) consultez la documentation de Adobe Journey Optimizer [.
* **Rendu des décisions de personnalisation visuelle :** si vous souhaitez effectuer le rendu d’un contenu personnalisé sur votre page, cochez la case **[!UICONTROL Rendre des décisions de personnalisation visuelle]**. Vous pouvez également spécifier des portées de décision et/ou des surfaces si nécessaire. Consultez la [documentation sur la personnalisation](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) pour plus d’informations sur le rendu du contenu personnalisé.
* **[!UICONTROL Demander la personnalisation par défaut]** : utilisez cette section pour contrôler si la portée de l’ensemble de la page (mbox globale) et la surface par défaut (surface web basée sur l’URL actuelle) sont demandées. Par défaut, cela est demandé automatiquement lors du premier appel de `sendEvent` du chargement de la page. Vous pouvez choisir parmi les options suivantes :
   * **[!UICONTROL Automatique]** : il s’agit du comportement par défaut. Ne demandez la personnalisation par défaut que si elle n’a pas encore été demandée. Cela correspond à `requestDefaultPersonalization` non défini dans la commande Web SDK.
   * **[!UICONTROL Activé]** : demandez explicitement la portée de la page et la surface par défaut. Cette opération met à jour le cache de l’affichage SPA. Cela correspond à `requestDefaultPersonalization` défini sur `true`.
   * **[!UICONTROL Désactivé]** : supprime explicitement la demande de la portée de page et de la surface par défaut. Cela correspond à `requestDefaultPersonalization` défini sur `false`.
* **[!UICONTROL Contexte de décision]** : il s’agit d’un mappage clé-valeur utilisé lors de l’évaluation des ensembles de règles Adobe Journey Optimizer pour la prise de décision sur l’appareil. Vous pouvez fournir le contexte de décision manuellement ou par le biais d&#39;un élément de données.

### Remplacements de la configuration des trains de données {#datastream-overrides}

Les remplacements de trains de données vous permettent de définir des configurations supplémentaires pour vos trains de données, qui sont transmises au réseau Edge via le SDK Web.

Cela vous permet de déclencher des comportements de flux de données différents des comportements par défaut, sans créer de flux de données ni modifier vos paramètres existants. Pour plus d’informations, consultez la documentation sur la [configuration des remplacements de train de données](web-sdk-extension-configuration.md#datastream-overrides).

## Envoyer l’événement multimédia {#send-media-event}

Envoie un événement multimédia à Adobe Experience Platform et/ou Adobe Analytics. Cette action est utile lorsque vous effectuez le suivi d’événements multimédia sur votre site web. Sélectionnez une instance (si vous en avez plusieurs). L’action nécessite un `playerId` qui représente un identifiant unique pour une session de médias suivie. Elle nécessite également un **[!UICONTROL Qualité d’expérience]** et un élément de données `playhead` lors du démarrage d’une session multimédia.

![Image de l’interface utilisateur d’Experience Platform affichant l’écran d’événement multimédia d’envoi.](assets/send-media-event.png)

Le type d’action **[!UICONTROL Envoyer l’événement multimédia]** prend en charge les propriétés suivantes :

* **[!UICONTROL Instance]** : instance de Web SDK en cours d’utilisation.
* **[!UICONTROL Type d’événement multimédia]** : type de l’événement multimédia suivi.
* **[!UICONTROL ID du lecteur]** : identifiant unique de la session multimédia.
* **[!UICONTROL Tête de lecture]** : position actuelle de la lecture du média, en secondes.
* **[!UICONTROL Détails de session multimédia]** : lors de l’envoi d’un événement de démarrage de média, les détails de session multimédia requis doivent être spécifiés.
* **[!UICONTROL Détails du chapitre]** : dans cette section, vous pouvez spécifier les détails du chapitre lors de l’envoi d’un événement multimédia de début de chapitre.
* **[!UICONTROL Détails Advertising]**: lors de l&#39;envoi d&#39;un événement `AdBreakStart`, vous devez spécifier les détails publicitaires requis.
* **[!UICONTROL Détails du pod Advertising]**: détails sur le pod publicitaire lors de l’envoi d’un événement `AdStart`.
* **[!UICONTROL Détails de l’erreur]** : détails sur l’erreur de lecture qui fait l’objet d’un suivi.
* **[!UICONTROL Détails de la mise à jour de l’état]** : état du lecteur mis à jour.
* **[!UICONTROL Métadonnées personnalisées]** : métadonnées personnalisées à propos de l’événement multimédia qui fait l’objet d’un suivi.
* **[!UICONTROL Qualité d’expérience]** : qualité multimédia des données d’expérience qui font l’objet d’un suivi.

## Définir le consentement {#set-consent}

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au SDK Web Adobe Experience Platform à l’aide du type d’action « Définir le consentement ». Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Voir [Prise en charge des préférences de consentement du client](../../../../web-sdk/commands/setconsent.md). Lors de l’utilisation d’Adobe version 2.0, seule une valeur d’élément de données est prise en charge. Vous devez créer un élément de données qui est résolu sur l’objet de consentement.

Dans cette action, vous recevez également un champ facultatif pour inclure un mappage d’identités afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme « En attente » ou « Expiré », car l’appel de consentement est probablement le premier appel à se déclencher.

## Mettre à jour la variable {#update-variable}

Utilisez cette action pour modifier un objet XDM suite à un événement. Cette action est destinée à créer un objet qui peut être référencé ultérieurement à partir d’une action **[!UICONTROL Envoyer l’événement]**, pour enregistrer l’objet XDM d’événement.

Pour utiliser ce type d’action, vous devez avoir défini un élément de données [variable](data-element-types.md#variable). Une fois que vous avez choisi un élément de données variable à modifier, un éditeur s’affiche, similaire à l’éditeur de l’élément de données [objet XDM](data-element-types.md#xdm-object).

![](assets/update-variable.png)

Le schéma XDM utilisé pour l’éditeur est le schéma sélectionné sur l’élément de données [!UICONTROL variable]. Vous pouvez définir une ou plusieurs propriétés de l’objet en cliquant sur l’une des propriétés de l’arborescence à gauche, puis en modifiant la valeur à droite. Par exemple, dans la capture d’écran ci-dessous, la propriété productBy est définie sur l’élément de données « Produit par l’élément de données ».

![](assets/update-variable-set-property.png)

Il existe quelques différences entre l’éditeur dans l’action de mise à jour de la variable et l’éditeur dans l’élément de données de l’objet XDM. Tout d’abord, l’action de mise à jour de variable comporte un élément de niveau racine intitulé « xdm ». Si vous cliquez sur cet élément, vous pouvez spécifier un élément de données à utiliser pour définir l’objet entier. Ensuite, l’action Mettre à jour la variable comporte des cases à cocher pour effacer les données de l’objet xdm. Cliquez sur l’une des propriétés à gauche, puis cochez la case à droite pour effacer la valeur. Cela effacera la valeur actuelle avant de définir des valeurs pour la variable.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment configurer vos actions. Découvrez ensuite comment [configurer vos types d’éléments de données](data-element-types.md).
