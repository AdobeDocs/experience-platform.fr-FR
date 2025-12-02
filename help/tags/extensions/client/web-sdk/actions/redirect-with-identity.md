---
title: Rediriger avec identité
description: Permet de partager un identifiant visiteur sur les domaines de votre organisation.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Rediriger avec identité

Le type d’action **[!UICONTROL Redirect with identity]** vous permet de partager un identifiant visiteur de la page en cours avec un autre domaine appartenant à votre organisation. Il est conçu pour être utilisé avec un événement de clic et une condition de comparaison de valeurs. Sur le plan fonctionnel, elle est similaire à la commande [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) de la bibliothèque JavaScript.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant du [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Action type] sur **[!UICONTROL Redirect with identity]**.

## Cas d’utilisation

* **Identifier un individu à travers plusieurs domaines** : si un visiteur clique d’un domaine à un autre appartenant à votre organisation, vous pouvez utiliser cette action afin qu’ils soient toujours considérés comme la même personne. Cette méthode d’identification est particulièrement utile si vous disposez de rapports qui combinent des données provenant de plusieurs domaines, empêchant ainsi l’inflation des visiteurs.
* **Identification d&#39;une personne d&#39;une application mobile à une application web** : si une personne est dans votre application mobile et qu&#39;elle clique sur un lien vers votre application web, vous pouvez utiliser cette action afin que la SDK web reconnaisse qu&#39;il s&#39;agit de la même personne. Ce workflow offre une expérience cohérente en matière de création de rapports et de personnalisation.

## Champs disponibles

* **[!UICONTROL Instance]** : instance SDK à laquelle l’action s’applique. Ce menu déroulant est désactivé si votre implémentation utilise une seule instance SDK.
* **[!UICONTROL Datastream configuration overrides]** : cette commande prend en charge les remplacements de configuration des trains de données, ce qui vous permet de contrôler les applications et services qui reçoivent ces données. Lorsque vous définissez un remplacement de configuration de train de données à la fois dans une commande individuelle et dans les paramètres de configuration de l’extension de balise, la commande individuelle est prioritaire. Consultez [&#x200B; Remplacements de configuration de train de données &#x200B;](../configure/configuration-overrides.md) pour plus d’informations.

## Exemple de règle

Cette commande est généralement utilisée avec une règle spécifique qui écoute les clics et vérifie les domaines souhaités.

+++Critères d’événement de règle

Se déclenche lorsqu’un utilisateur clique sur une balise d’ancrage avec une propriété `href`.

* **[!UICONTROL Extension]** : Core
* **[!UICONTROL Event type]** : cliquez sur
* **[!UICONTROL When the user clicks on]** : éléments spécifiques
* **[!UICONTROL Elements matching the CSS selector]** : `a[href]`

![Événement de règle](../assets/id-sharing-event-configuration.png)

+++

+++Condition de règle

Déclenche uniquement sur les domaines souhaités.

* **[!UICONTROL Logic type]** : Régulier
* **[!UICONTROL Extension]** : Core
* **[!UICONTROL Condition Type]** : comparaison de valeurs
* **[!UICONTROL Left Operand]** : `%this.hostname%`
* **[!UICONTROL Operator]** : Correspond à l’expression régulière
* **[!UICONTROL Right Operand]** : expression régulière correspondant aux domaines souhaités. Par exemple : `adobe.com$|behance.com$`

![Condition de règle](../assets/id-sharing-condition-configuration.png)

+++

+++Action de la règle

Ajoutez l’identité à l’URL.

* **[!UICONTROL Extension]** : Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]** : redirection avec identité

![Action de la règle](../assets/id-sharing-action-configuration.png)

+++
