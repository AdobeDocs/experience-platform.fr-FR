---
title: Événement d’envoi
description: Envoyez les données à Adobe Experience Platform Edge Network.
exl-id: 4ac7750e-48ab-4eb6-873d-bb2556dbf788
TQID: https://experienceleague.adobe.com/wigmBsoROqaLGEVNIgAn2b6BJ3lhAAKFBW9cj12iZZs
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: d556b755-390a-43f0-be32-a08cf6236126
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: b3a93754-a8b8-46eb-9421-7eccaeeb3dff
  - id: b572b7ff-a413-4173-b2b4-d7d3874f1b9b
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e9001ce2-5245-4a8e-8601-dd958009072f
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 838
ht-degree: 1%

---

# Événement d’envoi

L’action **[!UICONTROL Send event]** envoie une payload à un flux de données sur l’Edge Network Adobe Experience Platform. Il s’agit d’une fonctionnalité clé de la collecte et de la personnalisation des données. Presque toutes les organisations utilisent cette action dans le cadre de leur implémentation de Web SDK.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant du [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Action type] sur **[!UICONTROL Send event]**.

## Champs généraux

![Image de l’interface utilisateur Experience Platform Tags montrant les paramètres d’instance pour le type d’action Envoyer l’événement.](../assets/instance-settings.png)

* **[!UICONTROL Instance]** : instance SDK à laquelle l’action s’applique. Ce menu déroulant est désactivé si votre implémentation utilise une seule instance SDK.
* **[!UICONTROL Use guided events]** : activez cette option pour remplir ou masquer automatiquement certains champs afin d’activer un cas d’utilisation particulier. Ce paramètre peut contribuer à réduire le bruit des options disponibles lors de la configuration de l’action pour chaque objectif respectif et suit les bonnes pratiques d’Adobe en matière d’[événements de page supérieure/inférieure](/help/collection/use-cases/personalization/top-bottom-page-events.md). L’activation de cette case à cocher déclenche l’affichage des boutons radio suivants :
   * **[!UICONTROL Request personalization]** : obtenez les dernières décisions de personnalisation sans enregistrer d’événement Adobe Analytics. Elle est généralement appelée en haut de la page. Lorsqu&#39;il est sélectionné, ce bouton radio définit les champs suivants :
      * [!UICONTROL Type] est verrouillé sur [!UICONTROL Decisioning Proposition Fetch]
      * [!UICONTROL Render visual personalization decisions] est verrouillé pour activé
      * [!UICONTROL Automatically send a display event] est verrouillé sur désactivé
   * **[!UICONTROL Collect analytics]** : enregistrez un événement sans obtenir de décisions de personnalisation. Elle est généralement appelée en bas de la page. Lorsqu&#39;il est sélectionné, ce bouton radio définit les champs suivants :
      * [!UICONTROL Include rendered propositions] est verrouillé pour activé

## Champs de données

![Image de l’interface utilisateur Experience Platform Tags montrant les paramètres d’élément de données pour le type d’action Envoyer l’événement.](../assets/data.png)

* **[!UICONTROL Type]** : type d’événement. Vous pouvez effectuer une sélection à partir d’un ensemble prédéfini de valeurs ou définir votre propre valeur. Pour plus d’informations, voir [Valeurs acceptées pour `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype). La bibliothèque JavaScript équivalente à ce champ est [`eventType`](/help/collection/js/commands/sendevent/eventtype.md).
* **[!UICONTROL XDM]** : payload XDM à envoyer à Adobe. Vous pouvez utiliser un [objet XDM](../data-element-types.md#xdm-object) ou [Variable](../data-element-types.md#variable) dans ce champ. Si vous disposez de règles qui renseignent plusieurs objets XDM, vous pouvez utiliser [Objets fusionnés](../../core/overview.md#merged-objects) pour les combiner.
* **[!UICONTROL Data]** : payload de données à envoyer à Adobe. Certains services et applications ne nécessitent pas de respecter un schéma XDM, comme Adobe Analytics ou Adobe Target. Utilisez un type d’élément de données [Variable](../data-element-types.md#variable) pour ce champ.
* **[!UICONTROL Include rendered propositions]** : activez cette case à cocher pour utiliser cet événement en tant qu’événement d’affichage, y compris les propositions générées lorsque l’option « Envoyer automatiquement un événement d’affichage » n’était pas cochée. Le champ XDM `_experience.decisioning` est renseigné avec des informations sur la personnalisation rendue.
* **[!UICONTROL Document will unload]** : cochez cette case pour vous assurer que l’événement atteint le serveur même si l’utilisateur quitte la page. Ce paramètre permet aux événements d’atteindre le serveur, mais les réponses d’Edge Network sont ignorées.
* **[!UICONTROL Merge ID]** _(obsolète)_ : renseigne le champ XDM `eventMergeId`.

## Champs de personnalisation

![Image de l’interface utilisateur Experience Platform Tags montrant les paramètres Personalization pour le type d’action Envoyer l’événement.](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]** : tableau des portées que vous souhaitez demander explicitement à la personnalisation. Vous pouvez saisir les portées manuellement ou fournir un élément de données. Lors de la saisie manuelle des portées, chaque champ représente une portée. Sélectionnez **[!UICONTROL Add scope]** pour ajouter d’autres portées à l’action.
* **[!UICONTROL Surfaces]** : tableau de surfaces à interroger avec l’événement. Voir [Création d’expériences web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html?lang=fr) dans la documentation de Adobe Journey Optimizer pour plus d’informations. Lors de la saisie manuelle de surfaces, chaque champ représente une surface. Sélectionnez **[!UICONTROL Add surface]** pour ajouter d’autres surfaces à l’action.
* **Rendre les décisions de personnalisation visuelle :** une case à cocher qui, lorsqu’elle est activée, vous permet de rendre du contenu personnalisé sur la page. Pour plus d’informations[&#128279;](/help/collection/use-cases/personalization/render-auto-pers-content.md) consultez la section Rendu automatique des actions DOM .
* **[!UICONTROL Request default personalization]** : contrôle si la portée à l’échelle de la page et la surface par défaut sont demandées. Par défaut, elle est demandée automatiquement lors du premier appel `sendEvent` du chargement de la page. La bibliothèque JavaScript équivalente à ces boutons radio est [`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md). Vous pouvez choisir parmi les options suivantes :
   * **[!UICONTROL Automatic]** : comportement par défaut. Ne demandez la personnalisation par défaut que si elle n’a pas encore été demandée.
   * **[!UICONTROL Enabled]** : demander explicitement la portée de la page et la surface par défaut. Cette opération met à jour le cache de l’affichage SPA.
   * **[!UICONTROL Disabled]** : supprimer explicitement la demande pour la portée de page et la surface par défaut.
* **[!UICONTROL Decision context]** : mappage clé-valeur utilisé lors de l’évaluation des ensembles de règles Adobe Journey Optimizer pour la prise de décision sur l’appareil. Vous pouvez fournir le contexte de décision manuellement ou par le biais d&#39;un élément de données.

## Champs Advertising

![L’interface utilisateur des balises Experience Platform affiche les paramètres publicitaires de l’action Envoyer l’événement](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]** : détermine quand (ou si) la bibliothèque ajoute des informations publicitaires à la payload XDM. Vous pouvez choisir parmi les options suivantes :
   * **[!UICONTROL Automatic]** : toutes les données publicitaires disponibles au moment de l’événement sont ajoutées à la payload de l’événement.
   * **[!UICONTROL Wait]** : retardez l’envoi de l’événement jusqu’à la réception des données de publicité.
   * **[!UICONTROL Disabled]** : n’ajoutez pas de données publicitaires à la payload de l’événement. Sélectionnez cette option si votre implémentation n’utilise ni Adobe Analytics ni Customer Journey Analytics.

## Remplacements de la configuration du train de données

Cette commande prend en charge les remplacements de la configuration des trains de données, ce qui vous permet de contrôler les applications et services qui reçoivent ces données. Lorsque vous définissez un remplacement de configuration de train de données à la fois dans une commande individuelle et dans les paramètres de configuration de l’extension de balise, la commande individuelle est prioritaire. Consultez [&#x200B; Remplacements de configuration de train de données &#x200B;](../configure/configuration-overrides.md) pour plus d’informations.
