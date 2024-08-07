---
title: Types d’action dans l’extension SDK Web Adobe Experience Platform
description: Découvrez les différents types d’actions fournis par l’extension de balise du SDK Web de Adobe Experience Platform.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 760484bb7f95df97701f81f78783f0214aecaf5b
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 2%

---


# Types d’actions

Après avoir configuré l’ [extension de balise du SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md), vous devez configurer vos types d’actions.

Cette page décrit les types d’actions pris en charge par l’ [extension de balise SDK Web Adobe Experience Platform](web-sdk-extension-configuration.md).

## Appliquer les propositions {#apply-propositions}

Le type d’action **[!UICONTROL Appliquer les propositions]** vous permet de générer des propositions dans des applications d’une seule page sans incrémenter de mesures.

Ce type d’action est utile lorsque vous utilisez des applications d’une seule page dans lesquelles des parties de la page sont régénérées, ce qui peut remplacer toute personnalisation déjà appliquée à la page.

Vous pouvez utiliser ce type d’action pour divers cas d’utilisation, tels que :

1. **Rendre les offres d’HTML de mbox**. Les propositions explicitement demandées via une portée ou une surface à partir d’une action **[!UICONTROL Envoyer l’événement]** ne sont pas automatiquement rendues. Vous pouvez utiliser le type d’action **[!UICONTROL Appliquer les propositions]** pour indiquer au SDK Web où les rendre en spécifiant les métadonnées de proposition.
2. **Effectuez le rendu des offres pour une vue sur une application d’une seule page**. Lors du rendu d’un événement view change, si les données d’analyse ne sont pas encore prêtes, vous pouvez utiliser l’action **[!UICONTROL Appliquer les propositions]** pour effectuer le rendu des propositions d’affichage en haut de la page. Pour plus d’informations, voir [top and bottom of page events (deuxième page vue - Option 2)](../../../../web-sdk/use-cases/top-bottom-page-events.md) . Pour l’utiliser, saisissez un **[!UICONTROL nom d’affichage]** dans le formulaire.
3. **Renouveler les propositions**. Lorsque votre site utilise une structure telle que React pour effectuer le rendu du contenu, vous devrez peut-être réappliquer la personnalisation. Dans ce cas, vous pouvez utiliser le type d’action **[!UICONTROL Appliquer les propositions]** pour effectuer cette opération.

Ce type d’action n’envoie pas d’événement d’affichage pour les propositions générées. Il effectue le suivi des propositions générées afin qu’elles puissent être incluses dans les appels **[!UICONTROL Send event]** suivants.


![L’interface utilisateur des balises de plateforme affiche le type d’action Appliquer les propositions.](assets/apply-propositions.png)

Ce type d’action prend en charge les champs suivants :

* **[!UICONTROL Propositions]** : un tableau d’objets de proposition que vous souhaitez rendre à nouveau.
* **[!UICONTROL Nom de la vue]** : nom de la vue à afficher.
* **[!UICONTROL Métadonnées de proposition]** : objet qui détermine la manière dont les offres d’HTML peuvent être appliquées. Vous pouvez fournir ces informations par le biais du formulaire ou d’un élément de données. Il contient les propriétés suivantes :
   * **[!UICONTROL Périmètre]**
   * **[!UICONTROL Sélecteur]**
   * **[!UICONTROL Type d’action]**

## Appliquer la réponse {#apply-response}

Utilisez le type d’action **[!UICONTROL Appliquer la réponse]** lorsque vous souhaitez effectuer diverses actions en fonction d’une réponse de l’Edge Network. Ce type d’action est généralement utilisé dans les déploiements hybrides où le serveur effectue un appel initial vers l’Edge Network, puis ce type d’action prend la réponse de cet appel et initialise le SDK Web dans le navigateur.

L’utilisation de ce type d’action peut réduire les temps de chargement des clients pour les cas d’utilisation de personnalisation hybride.

![Image de l&#39;interface utilisateur Experience Platform montrant le type d&#39;action Appliquer la réponse.](assets/apply-response.png)

Ce type d’action prend en charge les options de configuration suivantes :

* **[!UICONTROL Instance]** : sélectionnez l’instance du SDK Web que vous utilisez.
* **[!UICONTROL En-têtes de réponse]** : sélectionnez l’élément de données qui renvoie un objet contenant les clés d’en-tête et les valeurs renvoyées par l’appel serveur Edge Network.
* **[!UICONTROL Corps de la réponse]** : sélectionnez l’élément de données qui renvoie l’objet contenant la charge utile JSON fournie par la réponse de l’Edge Network.
* **[!UICONTROL Rendre les décisions de personnalisation visuelle]** : activez cette option pour effectuer automatiquement le rendu du contenu de personnalisation fourni par l’Edge Network et pré-masquer le contenu pour empêcher le scintillement.

## Évaluation des jeux de règles {#evaluate-rulesets}

Ce type d’action déclenche manuellement l’évaluation de l’ensemble de règles. Les jeux de règles sont renvoyés par Adobe Journey Optimizer pour prendre en charge des fonctionnalités telles que les messages dans le navigateur.

![Image de l’interface utilisateur de l’Experience Platform montrant le type d’action de réponse Évaluer les jeux de règles.](assets/evaluate-rulesets.png)

Ce type d’action prend en charge les options suivantes :

* **[!UICONTROL Rendre les décisions de personnalisation visuelle]** : activez cette option pour effectuer le rendu des décisions de personnalisation visuelle pour les éléments de l’ensemble de règles qui correspondent.
* **[!UICONTROL Contexte de décision]** : il s’agit d’un mappage clé-valeur utilisé lors de l’évaluation des jeux de règles Adobe Journey Optimizer pour la prise de décision sur l’appareil. Vous pouvez fournir le contexte de décision manuellement ou par le biais d’un élément de données.

## Obtention du suivi de Media Analytics {#get-media-analytics-tracker}

Cette action est utilisée pour obtenir l’API Media Analytics héritée. Lors de la configuration de l’action et qu’un nom d’objet est fourni, l’API Media Analytics héritée est exportée vers cet objet de fenêtre. Si aucun fichier n’est fourni, il sera exporté vers `window.Media` comme le fait la bibliothèque Media JS actuelle.

![Image de l’interface utilisateur de la plateforme montrant le type d’action Get Media Analytics Tracker.](assets/get-media-analytics-tracker.png)

## Redirection vers une identité {#redirect-with-identity}

Utilisez ce type d’action pour partager les identités de la page active avec d’autres domaines. Cette action est conçue pour être utilisée avec un type d’événement **[!UICONTROL click]** et une condition de comparaison de valeurs. Voir [Ajout d’une identité à une URL à l’aide de l’extension SDK Web](../../../../web-sdk/commands/appendidentitytourl.md#extension) pour plus d’informations sur l’utilisation de ce type d’action.

## Envoyer un événement {#send-event}

Envoie un événement à Experience Platform afin que Platform puisse collecter les données que vous envoyez et agir sur la base de ces informations. Toutes les données que vous souhaitez envoyer peuvent être envoyées dans le champ **[!UICONTROL XDM Data]**. Utilisez un objet [!DNL JSON] conforme à la structure de votre schéma [!DNL XDM]. Cet objet peut être créé sur votre page ou par l’intermédiaire d’un **** **[!UICONTROL élément de données]**.

Le type d’action **[!UICONTROL Envoyer l’événement]** prend en charge les champs et paramètres décrits ci-dessous. Ces champs sont tous facultatifs.

### Paramètres des instances {#instance}

Utilisez le sélecteur **[!UICONTROL Instance]** pour choisir l’instance de SDK Web que vous souhaitez configurer. Si vous n’avez qu’une seule instance, elle est présélectionnée.

![Image de l’interface utilisateur des balises de plateforme montrant les paramètres de l’instance pour le type d’action Envoyer l’événement.](assets/instance-settings.png)

* **[!UICONTROL Instance]** : sélectionnez l’instance du SDK Web que vous souhaitez configurer. Si vous n’avez qu’une seule instance, elle sera présélectionnée.
* **[!UICONTROL Utiliser des événements guidés]** : activez cette option pour renseigner ou masquer automatiquement certains champs afin d’activer un cas d’utilisation spécifique. L’activation de cette option déclenche l’affichage des paramètres suivants.
   * **[!UICONTROL Demander la personnalisation]** : cet événement est conçu pour être appelé en haut de la page. Lorsqu’il est sélectionné, cet événement définit les champs suivants :
      * **[!UICONTROL Type]** : **[!UICONTROL Récupération de proposition de prise de décision]**
      * **[!UICONTROL Envoyer automatiquement un événement d’affichage]** : **[!UICONTROL false]**
      * Pour effectuer automatiquement le rendu de la personnalisation dans ce cas, activez l’option **[!UICONTROL Render Visual personalization Decisions]** (Rendre les décisions de personnalisation visuelle).
   * **[!UICONTROL Collect analytics]** : cet événement est conçu pour être appelé au bas de la page. Lorsqu’il est sélectionné, cet événement définit les champs suivants :
      * **[!UICONTROL Inclure les propositions rendues]** : **[!UICONTROL true]**
      * Les paramètres **[!UICONTROL Personalization]** sont masqués

  >[!NOTE]
  >
  >Les événements guidés sont liés aux [événements de haut et de bas de page](../../../../web-sdk/use-cases/top-bottom-page-events.md).


### Données {#data}

![Image de l’interface utilisateur des balises de plateforme montrant les paramètres de l’élément de données pour le type d’action Envoyer l’événement.](assets/data.png)

* **[!UICONTROL Type]** : ce champ vous permet de spécifier un type d’événement qui sera enregistré dans votre schéma XDM. Voir [`type`](/help/web-sdk/commands/sendevent/type.md) dans la commande `sendEvent` pour plus d’informations.
* **[!UICONTROL XDM]** :
* **[!UICONTROL Data]** : utilisez ce champ pour envoyer des données qui ne correspondent pas à un schéma XDM. Ce champ est utile si vous essayez de mettre à jour un profil Adobe Target ou d’envoyer des attributs Recommendations Target. Voir [`data`](/help/web-sdk/commands/sendevent/data.md) dans la commande `sendEvent` pour plus d’informations.
* **[!UICONTROL Inclure les propositions rendues]** : activez cette option pour inclure toutes les propositions qui ont été rendues, mais aucun événement d’affichage n’a été envoyé. Utilisez-le en tandem avec **[!UICONTROL Envoi automatique d’un événement d’affichage]** désactivé. Ce paramètre met à jour le champ XDM `_experience.decisioning` avec des informations sur les propositions générées.
* **[!UICONTROL Le document va se décharger]** : activez cette option pour vous assurer que les événements atteignent le serveur même si l’utilisateur quitte la page. Cela permet aux événements d’atteindre le serveur, mais les réponses sont ignorées.
* **[!UICONTROL ID de fusion]** : **Ce champ est obsolète**. Cela renseignera le champ XDM `eventMergeId`.

### Personnalisation {#personalization}

![Image de l’interface utilisateur des balises de plateforme montrant les paramètres Personalization pour le type d’action Envoyer l’événement.](assets/personalization-settings.png)

* **[!UICONTROL Portées]** : sélectionnez les portées (Adobe Target [!DNL mboxes]) que vous souhaitez demander explicitement à la personnalisation. Vous pouvez saisir les portées manuellement ou en fournissant un élément de données.
* **[!UICONTROL Surfaces]** : définissez les surfaces web disponibles sur la page pour la personnalisation. Pour plus d’informations, consultez la [documentation Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) .
* **Rendre les décisions de personnalisation visuelle :** Si vous souhaitez effectuer le rendu du contenu personnalisé sur votre page, cochez la case **[!UICONTROL Render Visual personalization Decisions]** . Vous pouvez également spécifier des portées de décision et/ou des surfaces si nécessaire. Pour plus d’informations sur le rendu du contenu personnalisé, consultez la [documentation de personnalisation](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) .
* **[!UICONTROL Demander la personnalisation par défaut]** : utilisez cette section pour contrôler si la portée à l’échelle de la page (mbox globale) et la surface par défaut (surface web en fonction de l’URL actuelle) sont demandées. Par défaut, cette demande est automatiquement effectuée lors du premier appel `sendEvent` du chargement de la page. Vous pouvez choisir parmi les options suivantes :
   * **[!UICONTROL Automatique]** : il s’agit du comportement par défaut. Ne demandez la personnalisation par défaut que si elle n’a pas encore été demandée. Cela correspond à `requestDefaultPersonalization` non défini dans la commande du SDK Web.
   * **[!UICONTROL Activé]** : demandez explicitement la portée de la page et la surface par défaut. Cela met à jour le cache d’affichage SPA. Cela correspond à `requestDefaultPersonalization` défini sur `true`.
   * **[!UICONTROL Désactivé]** : supprimez explicitement la demande pour la portée de la page et la surface par défaut. Cela correspond à `requestDefaultPersonalization` défini sur `false`.
* **[!UICONTROL Contexte de décision]** : il s’agit d’un mappage clé-valeur utilisé lors de l’évaluation des jeux de règles Adobe Journey Optimizer pour la prise de décision sur l’appareil. Vous pouvez fournir le contexte de décision manuellement ou par le biais d’un élément de données.

### Remplacements de la configuration des flux de données {#datastream-overrides}

Les remplacements de trains de données vous permettent de définir des configurations supplémentaires pour vos trains de données, qui sont transmises au réseau Edge via le SDK Web.

Vous pouvez ainsi déclencher différents comportements de flux de données par rapport aux comportements par défaut, sans créer de flux de données ni modifier vos paramètres existants. Pour plus d’informations, consultez la documentation sur la [configuration des remplacements de la banque de données](web-sdk-extension-configuration.md#datastream-overrides) .

## Envoyer un événement multimédia {#send-media-event}

Envoie un événement multimédia à Adobe Experience Platform et/ou Adobe Analytics. Cette action est utile lorsque vous effectuez le suivi des événements multimédia sur votre site web. Sélectionnez une instance (si vous en avez plusieurs). L’action nécessite un `playerId` qui représente un identifiant unique pour une session multimédia trackée. Elle nécessite également une **[!UICONTROL qualité de l’expérience]** et un élément de données `playhead` lors du démarrage d’une session multimédia.

![Image de l’interface utilisateur de la plateforme montrant l’écran d’événement de média envoyé.](assets/send-media-event.png)

Le type d’action **[!UICONTROL Envoyer un événement multimédia]** prend en charge les propriétés suivantes :

* **[!UICONTROL Instance]** : instance du SDK Web utilisée.
* **[!UICONTROL Type d’événement multimédia]** : type de l’événement multimédia suivi.
* **[!UICONTROL ID du lecteur]** : identifiant unique de la session multimédia.
* **[!UICONTROL Curseur de lecture]** : position actuelle de la lecture du média, en secondes.
* **[!UICONTROL Détails de la session multimédia]** : lors de l’envoi d’un événement de démarrage du média, les détails requis de la session multimédia doivent être spécifiés.
* **[!UICONTROL Détails du chapitre]** : dans cette section, vous pouvez spécifier les détails du chapitre lors de l’envoi d’un événement multimédia de début de chapitre.
* **[!UICONTROL Détails Advertising]** : lors de l’envoi d’un événement `AdBreakStart`, vous devez spécifier les détails publicitaires requis.
* **[!UICONTROL Détails de la capsule Advertising]** : détails de la capsule publicitaire lors de l’envoi d’un événement `AdStart`.
* **[!UICONTROL Détails de l’erreur]** : détails sur l’erreur de lecture qui est suivie.
* **[!UICONTROL Détails de mise à jour de l’état]** : état du lecteur mis à jour.
* **[!UICONTROL Métadonnées personnalisées]** : métadonnées personnalisées de l’événement multimédia en cours de suivi.
* **[!UICONTROL Qualité de l’expérience]** : qualité multimédia des données d’expérience suivies.

## Définition du consentement {#set-consent}

Une fois que vous avez reçu le consentement de votre utilisateur, ce consentement doit être communiqué au SDK Web de Adobe Experience Platform à l’aide du type d’action &quot;Définir le consentement&quot;. Actuellement, deux types de standards sont pris en charge : « Adobe » et « IAB TCF ». Voir [Prise en charge des préférences de consentement du client](../../../../web-sdk/commands/setconsent.md). Lors de l’utilisation d’Adobe version 2.0, seule une valeur d’élément de données est prise en charge. Vous devez créer un élément de données qui résout l’objet de consentement.

Dans cette action, vous recevez également un champ facultatif pour inclure une carte des identités afin que les identités puissent être synchronisées une fois le consentement reçu. La synchronisation est utile lorsque le consentement est configuré comme &quot;En attente&quot; ou &quot;Sortie&quot;, car l’appel de consentement est probablement le premier appel à se déclencher.

## Mettre à jour la variable {#update-variable}

Utilisez cette action pour modifier un objet XDM suite à un événement. Cette action est destinée à créer un objet qui peut être référencé ultérieurement à partir d’une action **[!UICONTROL Envoyer l’événement]**, pour enregistrer l’objet XDM d’événement.

Pour utiliser ce type d’action, vous devez avoir défini un élément de données [variable](data-element-types.md#variable) . Une fois que vous avez choisi un élément de données de variable à modifier, un éditeur s’affiche, semblable à l’éditeur de l’élément de données [objet XDM](data-element-types.md#xdm-object) .

![](assets/update-variable.png)

Le schéma XDM utilisé pour l’éditeur est le schéma sélectionné sur l’élément de données [!UICONTROL variable] . Vous pouvez définir une ou plusieurs propriétés de l’objet en cliquant sur l’une des propriétés de l’arborescence à gauche, puis en modifiant la valeur à droite. Par exemple, dans la capture d’écran ci-dessous, la propriété producBy est définie sur l’élément de données &quot;Produit par l’élément de données&quot;.

![](assets/update-variable-set-property.png)

Il existe des différences entre l’éditeur dans l’action de mise à jour de variable et l’éditeur dans l’élément de données de l’objet XDM. Tout d’abord, l’action de mise à jour de variable comporte un élément de niveau racine intitulé &quot;xdm&quot;. Si vous cliquez sur cet élément, vous pouvez spécifier un élément de données à utiliser pour définir l’objet entier. Deuxièmement, l’action de mise à jour de variable comporte des cases à cocher pour effacer les données de l’objet xdm. Cliquez sur l’une des propriétés à gauche, puis cochez la case à droite pour effacer la valeur. Cela permet d’effacer la valeur actuelle avant de définir des valeurs sur la variable.

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer vos actions. Ensuite, découvrez comment [configurer vos types d’éléments de données](data-element-types.md).
