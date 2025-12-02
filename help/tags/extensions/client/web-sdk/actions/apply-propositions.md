---
title: Appliquer les propositions
description: Propositions de rendu dans les applications monopages sans incrémenter de mesures.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Appliquer les propositions

Le type d’action **[!UICONTROL Apply propositions]** vous permet de générer des propositions dans des applications monopages sans incrémenter de mesures. Ce type d’action est utile lorsque vous travaillez avec des applications monopages où des parties de la page sont rendues de nouveau, ce qui peut remplacer toutes les personnalisations déjà appliquées à la page.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant du [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Action type] sur **[!UICONTROL Apply propositions]**.

![L’interface utilisateur d’Experience Platform Tags affiche le type d’action Appliquer les propositions.](../assets/apply-propositions.png)

## Cas d’utilisation

Vous pouvez utiliser ce type d’action pour différents cas d’utilisation, tels que :

1. **Rendu des offres de mbox HTML**. Les propositions explicitement demandées via une portée ou une surface à partir d’une action **[!UICONTROL Send event]** ne sont pas automatiquement rendues. Vous pouvez utiliser le type d’action **[!UICONTROL Apply propositions]** pour indiquer à Web SDK où effectuer leur rendu en spécifiant les métadonnées de proposition.
2. **Effectuez le rendu des offres pour une vue sur une application monopage**. Lors du rendu d’un événement de changement de vue, si les données d’analyse ne sont pas encore prêtes, vous pouvez utiliser l’action **[!UICONTROL Apply propositions]** pour effectuer le rendu des propositions de vue en haut de la page. Voir [événements en haut et en bas de la page (Deuxième page vue - Option 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md) pour plus d’informations. Pour l’utiliser, saisissez un **[!UICONTROL View name]** dans le formulaire.
3. **Restituer des propositions**. Lorsque votre site utilise un framework comme React pour effectuer à nouveau le rendu du contenu, vous devrez peut-être appliquer une nouvelle personnalisation. Dans ce cas, vous pouvez utiliser le type d’action **[!UICONTROL Apply propositions]** pour ce faire.

Ce type d’action n’envoie pas d’événement d’affichage pour les propositions rendues. Il effectue le suivi des propositions générées afin qu’elles puissent être incluses dans les appels de **[!UICONTROL Send event]** suivants.

## Champs disponibles

Ce type d&#39;action prend en charge les champs suivants :

* **[!UICONTROL Instance]** : instance SDK à laquelle l’action s’applique. Ce menu déroulant est désactivé si votre implémentation utilise une seule instance SDK.
* **[!UICONTROL Propositions]** : tableau d’objets de proposition dont vous souhaitez effectuer à nouveau le rendu.
* **[!UICONTROL View name]** : nom de la vue à afficher.
* **[!UICONTROL Proposition metadata]** : objet qui détermine la manière dont les offres HTML peuvent être appliquées. Vous pouvez fournir ces informations par le biais du formulaire ou d’un élément de données. Il contient les propriétés suivantes :
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
