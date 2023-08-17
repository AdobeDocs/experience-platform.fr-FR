---
title: Réengagement intelligent
description: Diffusez des expériences attrayantes et connectées au cours des moments de conversion clés pour réengager intelligemment les clients les plus rares.
hide: true
hidefromtoc: true
source-git-commit: 43e365e20a2fd91a0e822eb6f66bb7db6fc218f5
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 5%

---

# Réengagez intelligemment vos clients pour qu’ils reviennent

Réengager les clients qui ont abandonné une conversion avant de la terminer de manière intelligente et responsable. Engagez des clients obsolètes par le biais d’expériences plutôt que de rappels afin d’améliorer la conversion et de stimuler la croissance de la valeur de durée de vie du client.

Utilisez des considérations en temps réel, prenez en compte toutes les qualités et comportements des consommateurs et proposez une réqualification rapide basée sur des événements en ligne et hors ligne.

![Présentation visuelle de haut niveau du réengagement intelligent étape par étape.](../intelligent-re-engagement/images/step-by-step.png)

## Présentation du cas d’utilisation

Vous allez créer des schémas, des jeux de données et des audiences à mesure que vous utilisez des exemples de parcours de réengagement. Vous découvrirez également les fonctionnalités nécessaires à la configuration d’exemples de parcours dans [!DNL Adobe Journey Optimizer] et ceux nécessaires pour créer des publicités médiatiques payantes dans les destinations. Ce guide utilise des exemples de réengagement des clients dans les parcours de cas d’utilisation décrits ci-dessous :

* **Parcours de réengagement** - Cible les clients qui ont abandonné la navigation sur le site web et dans l’application mobile.
* **Parcours de panier abandonné** - Cible les clients qui ont placé des produits dans le panier mais qui n’ont pas encore été achetés sur le site web et l’application mobile.
* **Parcours de confirmation de commande** - Se concentre sur les achats de produits effectués par le biais du site web et de l’application mobile.

## Prérequis et planification {#prerequisites-and-planning}

À mesure que vous réalisez les étapes de mise en oeuvre du cas d’utilisation, vous utiliserez les fonctionnalités et éléments d’interface utilisateur de Real-Time CDP suivants (répertoriés dans l’ordre dans lequel vous les utiliserez). Assurez-vous de disposer des autorisations de contrôle d’accès en fonction des attributs nécessaires pour toutes ces zones ou demandez à votre administrateur système de vous octroyer les autorisations nécessaires.

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) : agrège les données entre les sources de données pour alimenter la campagne. Ces données sont ensuite utilisées pour créer les audiences de campagne et faire apparaître les éléments de données personnalisés utilisés dans l&#39;email et les mosaïques de promotion web (par exemple, le nom ou les informations liées au compte). La plateforme de données clients (CDP) est également utilisée pour activer les audiences par courrier électronique et sur le web (via Adobe Target).
   * [Schémas](/help/xdm/home.md)
   * [Profils](/help/profile/home.md)
   * [Jeux de données](/help/catalog/datasets/overview.md)
   * [Audiences](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr)
   * [Destinations](/help/destinations/home.md)
   * [Déclencheur d’événement ou d’audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Audiences/Événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Actions de parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr)

### Comment réaliser le cas d’utilisation : aperçu de haut niveau {#achieve-the-use-case-high-level}

Vous trouverez ci-dessous un aperçu général des trois exemples de parcours de réengagement.

>[!BEGINTABS]

>[!TAB Parcours de réengagement]

Le parcours de réengagement cible la navigation des produits abandonnés sur le site web et dans l’application mobile. Ce parcours est déclenché lorsqu’un produit a été consulté mais n’a pas été acheté ni ajouté au panier. L’engagement de la marque est déclenché au bout de trois jours s’il n’y a aucun ajout de liste au cours des dernières 24 heures.<p>![Présentation visuelle de haut niveau du parcours de réengagement intelligent du client.](../intelligent-re-engagement/images/re-engagement-journey.png "Présentation visuelle de haut niveau du parcours de réengagement intelligent du client."){width="1920" zoomable="yes"}</p>

1. Vous créez des schémas et des jeux de données marqués pour [!UICONTROL Profil].
2. Les données sont agrégées dans Experience Platform par le biais du SDK Web, du SDK Mobile Edge ou de l’API. Le connecteur de données Analytics peut également être utilisé, mais peut entraîner une latence de parcours.
3. Vous chargez des profils dans Real-Time CDP et créez des stratégies de gouvernance pour garantir une utilisation responsable.
4. Vous créez des audiences ciblées à partir de la liste des profils pour vérifier si un **client** a fait un engagement au cours des trois derniers jours.
5. Vous créez un parcours de réengagement dans [!DNL Adobe Journey Optimizer].
6. Si nécessaire, travaillez avec la fonction **partenaire de données** pour activer les audiences vers les destinations de médias payants souhaitées.
7. [!DNL Adobe Journey Optimizer] recherche le consentement et envoie les différentes actions configurées.

>[!TAB Parcours de panier abandonné]

Le parcours de panier abandonné cible les produits qui ont été placés dans le panier mais qui n’ont pas encore été achetés sur le site web et sur l’application mobile. En outre, les campagnes de médias payants sont lancées et arrêtées à l’aide de cette méthode.<p>![Présentation visuelle de haut niveau du parcours de panier abandonné par le client.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Présentation visuelle de haut niveau du parcours de panier abandonné par le client."){width="1920" zoomable="yes"}</p>

1. Vous créez des schémas et des jeux de données marqués pour [!UICONTROL Profil].
2. Les données sont agrégées dans Experience Platform par le biais du SDK Web, du SDK Mobile Edge ou de l’API. Le connecteur de données Analytics peut également être utilisé, mais peut entraîner une latence de parcours.
3. Vous chargez des profils dans Real-Time CDP et créez des stratégies de gouvernance pour garantir une utilisation responsable.
4. Vous créez des audiences ciblées à partir de la liste des profils pour vérifier si un **client** a placé un élément dans son panier mais n’a pas terminé l’achat. La variable **[!UICONTROL Ajouter au panier]** démarre un minuteur qui attend pendant 30 minutes, puis vérifie l’achat. Si aucun achat n’a été effectué, la variable **client** est ajouté à la variable **[!UICONTROL Abandonner le panier]** audiences.
5. Vous créez un parcours de panier abandonné dans Adobe Journey Optimizer
6. Si nécessaire, travaillez avec la fonction **partenaire de données** pour activer les audiences vers les destinations de médias payants souhaitées.
7. [!DNL Adobe Journey Optimizer] recherche le consentement et envoie les différentes actions configurées.

>[!TAB Parcours de confirmation de commande]

Le parcours de confirmation de commande se concentre sur les achats de produits effectués par le biais du site web et de l’application mobile.<p>![Présentation visuelle de haut niveau du parcours de confirmation de commande du client.](../intelligent-re-engagement/images/order-confirmation-journey.png "Présentation visuelle de haut niveau du parcours de confirmation de commande du client."){width="1920" zoomable="yes"}</p>

1. Vous créez des schémas et des jeux de données marqués pour [!UICONTROL Profil].
2. Les données sont agrégées dans Experience Platform par le biais du SDK Web, du SDK Mobile Edge ou de l’API. Le connecteur de données Analytics peut également être utilisé, mais peut entraîner une latence de parcours.
3. Vous chargez des profils dans Real-Time CDP et créez des stratégies de gouvernance pour garantir une utilisation responsable.
4. Vous créez des audiences ciblées à partir de la liste des profils pour vérifier si un **client** a effectué un achat.
5. Vous créez un parcours de confirmation dans Adobe Journey Optimizer.
6. [!DNL Adobe Journey Optimizer] envoie un message de confirmation de commande à l’aide du canal préféré.

>[!ENDTABS]

## Comment réaliser le cas d’utilisation : instructions détaillées {#step-by-step-instructions}

Pour terminer chacune des étapes des présentations de haut niveau ci-dessus, consultez les sections ci-dessous, qui proposent des liens vers des informations supplémentaires et des instructions plus détaillées.

### Fonctionnalités et éléments de l’interface utilisateur que vous utiliserez {#ui-functionality-and-elements}

Lorsque vous terminerez les étapes de mise en oeuvre du cas d’utilisation, vous utiliserez les fonctionnalités de Real-Time CDP et les éléments d’IU répertoriés au début de ce document. Assurez-vous de disposer des autorisations de contrôle d’accès en fonction des attributs nécessaires pour toutes ces zones ou demandez à votre administrateur système de vous octroyer les autorisations nécessaires.

### Création d’une conception de schéma et spécification de groupes de champs

Les ressources du modèle de données d’expérience (XDM) sont gérées dans le [!UICONTROL Schémas] espace de travail dans Adobe Experience Platform. Vous pouvez afficher et explorer les ressources de base fournies par Adobe et créer des ressources et des schémas personnalisés pour votre organisation.

Pour plus d’informations sur la création de schémas, consultez la section [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md)

Quatre conceptions de schéma sont utilisées pour le parcours de réengagement. Chaque schéma nécessite la configuration de champs spécifiques et certains champs fortement recommandés.

#### Schéma des attributs du client

Le schéma des attributs du client est représenté par une [!UICONTROL XDM Individual Profile] , qui inclut les groupes de champs suivants :

+++Détails du contact personnel (groupe de champs)

[Détails du contact personnel](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile qui décrit les coordonnées d’une personne.

| Champs | Exigence | Description |
| --- | --- | --- |
| `mobilePhone.number` | Obligatoire | Numéro de téléphone portable de la personne, qui sera utilisé pour les SMS. |
| `personalEmail.address` | Obligatoire | Adresse électronique de la personne. |

+++

+++Détails démographiques (groupe de champs)

[Détails démographiques](/help/xdm/field-groups/profile/demographic-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile. Le groupe de champs fournit un objet person de niveau racine, dont les sous-champs décrivent les informations sur une personne.

| Champs | Exigence |
| --- | --- |
| `person.name.firstName` | Suggérée |
| `person.name.lastName` | Suggérée |

+++

+++Détails de l’audit du système source externe (groupe de champs)

[Attributs d’audit du système de source externe](/help/xdm/data-types/external-source-system-audit-attributes.md) est un type de données XDM (Experience Data Model) standard qui capture les détails de l’audit sur un système source externe.

+++

+++Groupes de champs de consentement et de préférence (groupe de champs)

[Consentements et préférences](/help/xdm/field-groups//profile/consents.md) Le groupe de champs fournit un champ de type objet unique, les consentements, pour capturer les informations de consentement et de préférence.

| Champs | Exigence |
| --- | --- |
| `consents.marketing.email.val` | Obligatoire |
| `consents.marketing.preferred` | Obligatoire |
| `consents.marketing.push.val` | Obligatoire |
| `consents.marketing.sms.val` | Obligatoire |
| `consents.personalize.content.val` | Obligatoire |
| `consents.share.val` | Obligatoire |

+++

+++Détails du test de profil (groupe de champs)

Ce groupe de champs est utilisé pour les bonnes pratiques.

+++

#### Schéma des transactions numériques client

Le schéma des transactions numériques client est représenté par une [!UICONTROL XDM ExperienceEvent] , qui inclut les groupes de champs suivants :

+++Adobe Experience Platform Web SDK ExperienceEvent (groupe de champs)

| Champs | Exigence |
| --- | --- |
| `device.model` | Suggérée |
| `environment.browserDetails.userAgent` | Suggérée |

+++

+++Détails web (groupe de champs)

Détails web est un groupe de champs de schéma standard pour la classe XDM ExperienceEvent, utilisé pour décrire les informations concernant les événements de détails web tels que l’interaction, les détails de page et le référent.

| Champs | Exigence | Description |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Suggérée | Identifiant du lien web ou de l’URL qui correspond à l’interaction. |
| `web.webInteraction.linkClicks.value` | Suggérée | Nombre de clics pour le lien web ou l’URL qui correspond à l’interaction. |
| `web.webInteraction.name` | Suggérée | Nom de la page web. |
| `web.webInteraction.URL` | Suggérée | URL de la page web. |
| `web.webPageDetails.name` | Suggérée | Nom de la page web sur laquelle l’interaction web s’est produite. |
| `web.webPageDetails.URL` | Suggérée | URL de la page web sur laquelle l’interaction web s’est produite. |
| `web.webReferrer.URL` | Suggérée | Décrit le référent d’une interaction web, c’est-à-dire l’URL d’origine d’un visiteur juste avant l’enregistrement de l’interaction web actuelle. |

+++

+++Événement d’expérience client (groupe de champs)

| Champs | Exigence |
| --- | --- |
| `commerce.cart.cartID` | Suggérée |
| `commerce.cart.cartSource` | Suggérée |
| `commerce.cartAbandons.id` | Suggérée |
| `commerce.cartAbandons.value` | Suggérée |
| `commerce.order.orderType` | Suggérée |
| `commerce.order.payments.paymentAmount` | Suggérée |
| `commerce.order.payments.paymentType` | Suggérée |
| `commerce.order.payments.transactionID` | Suggérée |
| `commerce.order.priceTotal` | Suggérée |
| `commerce.order.purchaseID` | Suggérée |
| `commerce.productListAdds.id` | Suggérée |
| `commerce.productListAdds.value` | Suggérée |
| `commerce.productListOpens.id` | Suggérée |
| `commerce.productListOpens.value` | Suggérée |
| `commerce.productListRemoval.id` | Suggérée |
| `commerce.productListRemoval.value` | Suggérée |
| `commerce.productListViews.id` | Suggérée |
| `commerce.productListViews.value` | Suggérée |
| `commerce.productViews.id` | Suggérée |
| `commerce.productViews.value` | Suggérée |
| `commerce.purchases.id` | Suggérée |
| `commerce.purchases.value` | Suggérée |
| `marketing.campaignGroup` | Suggérée |
| `marketing.campaignName` | Suggérée |
| `marketing.trackingCode` | Suggérée |
| `productListItems.name` | Suggérée |
| `productListItems.priceTotal` | Suggérée |
| `productListItems.product` | Suggérée |
| `productListItems.quantity` | Suggérée |

+++

+++Détails de l’ID utilisateur final (groupe de champs)

| Champs | Exigence | Description |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Obligatoire | ID d’adresse électronique de l’utilisateur final état authentifié. |
| `endUserIDs._experience.emailid.id` | Obligatoire | ID de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.emailid.namespace.code` | Obligatoire | Code d’espace de noms de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoire | État d’authentification du Adobe Marketing Cloud ID (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoire | Adobe Marketing Cloud ID (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoire | Code d’espace de noms Adobe Marketing Cloud ID (MCID). |

+++

+++Valeur de classe (groupe de champs)

| Champs | Exigence |
| --- | --- |
| `eventType` | Obligatoire |
| `timestamp` | Obligatoire |

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

#### Schéma des transactions hors ligne client

Le schéma des transactions hors ligne du client est représenté par une [!UICONTROL XDM ExperienceEvent] , qui inclut les groupes de champs suivants :

+++Détails du commerce (groupe de champs)

| Champs | Exigence | Description |
| --- | --- | --- |
| `commerce.cart.cartID` | Obligatoire | Identifiant du panier. |
| `commerce.order.orderType` | Obligatoire | Objet décrivant le type de commande de produit. |
| `commerce.order.payments.paymentAmount` | Obligatoire | Objet décrivant le montant du paiement de la commande de produit. |
| `commerce.order.payments.paymentType` | Obligatoire | Objet décrivant le type de paiement de la commande de produit. |
| `commerce.order.payments.transactionID` | Obligatoire | Identifiant de transaction de commande de produit objet. |
| `commerce.order.purchaseID` | Obligatoire | Identifiant d’achat de commande de produit objet. |
| `productListItems.name` | Obligatoire | Liste de noms d’éléments représentant le ou les produits sélectionnés par un client. |
| `productListItems.priceTotal` | Obligatoire | Prix total de la liste d’articles représentant le ou les produits sélectionnés par un client. |
| `productListItems.product` | Obligatoire | Le ou les produits sélectionnés. |
| `productListItems.quantity` | Obligatoire | La quantité de la liste d’éléments représentant le ou les produits sélectionnés par un client. |

+++

+++Détails du contact personnel (groupe de champs)

| Champs | Exigence | Description |
| --- | --- | --- |
| `mobilePhone.number` | Obligatoire | Numéro de téléphone portable de la personne, qui sera utilisé pour les SMS. |
| `personalEmail.address` | Obligatoire | Adresse électronique de la personne. |

+++

+++Valeur de classe (groupe de champs)

| Champs | Exigence |
| --- | --- |
| `eventType` | Obligatoire |
| `timestamp` | Obligatoire |

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

#### Schéma du connecteur web Adobe

Le schéma du connecteur web Adobe est représenté par une [!UICONTROL XDM ExperienceEvent] , qui inclut les groupes de champs suivants :

+++Modèle ExperienceEvent Adobe Analytics (groupe de champs)

| Champs | Exigence | Description |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Suggérée | Identifiant du lien web ou de l’URL qui correspond à l’interaction. |
| `web.webInteraction.linkClicks.value` | Suggérée | Nombre de clics pour le lien web ou l’URL qui correspond à l’interaction. |
| `web.webInteraction.name` | Suggérée | Nom de la page web. |
| `web.webInteraction.URL` | Suggérée | URL de la page web. |
| `web.webPageDetails.name` | Suggérée | Nom de la page web sur laquelle l’interaction web s’est produite. |
| `web.webPageDetails.URL` | Suggérée | URL de la page web sur laquelle l’interaction web s’est produite. |
| `web.webReferrer.URL` | Suggérée | Décrit le référent d’une interaction web, c’est-à-dire l’URL d’origine d’un visiteur juste avant l’enregistrement de l’interaction web actuelle. |
| `commerce.cart.cartID` | Suggérée | |
| `commerce.cart.cartSource` | Suggérée | |
| `commerce.cartAbandons.id` | Suggérée | |
| `commerce.cartAbandons.value` | Suggérée | |
| `commerce.order.orderType` | Suggérée | |
| `commerce.order.payments.paymentAmount` | Suggérée | |
| `commerce.order.payments.paymentType` | Suggérée | |
| `commerce.order.payments.transactionID` | Suggérée | |
| `commerce.order.priceTotal` | Suggérée | |
| `commerce.order.purchaseID` | Suggérée | |
| `commerce.productListAdds.id` | Suggérée | |
| `commerce.productListAdds.value` | Suggérée | |
| `commerce.productListOpens.id` | Suggérée | |
| `commerce.productListOpens.value` | Suggérée | |
| `commerce.productListRemoval.id` | Suggérée | |
| `commerce.productListRemoval.value` | Suggérée | |
| `commerce.productListViews.id` | Suggérée | |
| `commerce.productListViews.value` | Suggérée | |
| `commerce.productViews.id` | Suggérée | |
| `commerce.productViews.value` | Suggérée | |
| `commerce.purchases.id` | Suggérée | |
| `commerce.purchases.value` | Suggérée | |
| `marketing.campaignGroup` | Suggérée | |
| `marketing.campaignName` | Suggérée | |
| `marketing.trackingCode` | Suggérée | |
| `productListItems.name` | Suggérée | |
| `productListItems.priceTotal` | Suggérée | |
| `productListItems.product` | Suggérée | |
| `productListItems.quantity` | Suggérée | |
| `endUserIDs._experience.emailid.authenticatedState` | Obligatoire | ID d’adresse électronique de l’utilisateur final état authentifié. |
| `endUserIDs._experience.emailid.id` | Obligatoire | ID de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.emailid.namespace.code` | Obligatoire | Code d’espace de noms de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoire | État d’authentification du Adobe Marketing Cloud ID (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoire | Adobe Marketing Cloud ID (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoire | Code d’espace de noms Adobe Marketing Cloud ID (MCID). |

+++

+++Valeur de classe (groupe de champs)

| Champs | Exigence |
| --- | --- |
| `eventType` | Obligatoire |
| `timestamp` | Obligatoire |

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

### Création d’un jeu de données à partir d’un schéma

Un jeu de données est une structure de stockage et de gestion pour un groupe de données, souvent un tableau avec des champs (lignes) et un schéma (colonnes). Chaque schéma pour les parcours de réengagement intelligents comporte un seul jeu de données.

Pour plus d’informations sur la création d’un jeu de données à partir d’un schéma, consultez la section [Guide de l’interface utilisateur des jeux de données](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Tout comme l’étape de création d’un schéma, vous devez activer l’inclusion du jeu de données dans le profil client en temps réel. Pour plus d’informations sur l’activation du jeu de données à utiliser dans Real-Time Customer Profile, consultez la section [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Confidentialité, consentement et gouvernance des données

#### Stratégies de consentement

>[!IMPORTANT]
>
>Disposer aux clients de la possibilité de se désabonner de la réception de communications d’une marque est une obligation légale, et garantir le respect de ce choix. Pour en savoir plus sur la législation applicable, consultez la [documentation Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Lors de la création d’un chemin de réengagement, les stratégies de consentement suivantes doivent être prises en compte et utilisées :

* If `consents.marketing.email.val = "Y"` alors peut envoyer un courrier électronique
* If `consents.marketing.sms.val = "Y"` alors peut envoyer des SMS
* If `consents.marketing.push.val = "Y"` Push
* If `consents.share.val = "Y"` puis peuvent faire la publicité
* Besoin défini par l’implémentation client

#### Libellé DULE et application

Les adresses électroniques personnelles sont utilisées comme données d’identification directe utilisées pour identifier ou contacter une personne spécifique plutôt qu’un appareil.

* `personalEmail.address = I1`

#### Stratégies marketing

Aucune autre stratégie marketing n’est nécessaire pour les parcours de réengagement. Toutefois, les éléments suivants doivent être pris en compte comme vous le souhaitez :

* Limitation des données sensibles
* Limitation de la publicité Onsite
* Limitation du ciblage des emails
* Limitation du ciblage intersite
* Restreindre la combinaison de données directement identifiables avec des données anonymes

### Création d’une audience

#### Création d’audiences pour les parcours de réengagement de marque

Les parcours de réengagement utilisent des audiences pour définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de clients potentiels de votre base. Les audiences peuvent être créées de deux manières différentes sur Adobe Experience Platform : soit directement composées en tant qu’audiences, soit par le biais de définitions de segment dérivées de Platform.

Pour plus d’informations sur la façon de composer directement des audiences, lisez le [Guide de l’interface utilisateur de composition d’audience](/help/segmentation/ui/audience-composition.md).

Pour plus d’informations sur la création d’audiences par le biais de définitions de segment dérivées de Platform, consultez la section [Guide de l’interface utilisateur d’Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Parcours de réengagement]

Les événements suivants sont utilisés pour le parcours de réengagement où les utilisateurs ont consulté des produits en ligne et n’ont pas ajouté au panier au cours des 24 heures suivantes, suivi d’aucun engagement de marque au cours des 3 jours suivants.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.productListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

Le descripteur du parcours de réengagement apparaît comme suit :

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Parcours de panier abandonné]

Les événements suivants sont utilisés pour le parcours de panier abandonné, où les utilisateurs ont ajouté un produit à leur panier, mais n’ont pas effectué l’achat ou vidé leur panier au cours des dernières 24 heures.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 30 minutes before now and <= 1440 minutes before now`
* `EventType: commerce.purchases`
   * `Timestamp: <= 30 minutes before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 30 minutes before now`

Le descripteur du parcours de panier abandonné apparaît comme suit :

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!ENDTABS]

### Configuration des parcours dans Adobe Journey Optimizer

>[!NOTE]
>
>Adobe Journey Optimizer n’englobe pas tout ce qui est affiché dans les diagrammes en haut de cette page. Toutes les publicités multimédia payantes sont créées dans [!UICONTROL Destinations].

Adobe Journey Optimizer vous aide à offrir à vos clients des expériences connectées, contextuelles et personnalisées. Le parcours client correspond à l’ensemble du processus des interactions d’un client avec la marque. Chaque parcours de cas d’utilisation nécessite des informations spécifiques. Vous trouverez ci-dessous les données précises nécessaires à chaque branche de Parcours.

>[!BEGINTABS]

>[!TAB Parcours de réengagement]

+++Événements

* Consultations produits
   * Schéma : transactions numériques client
   * Champs:
      * `EventType`
   * Condition:
      * `EventType = commerce.productViews`
      * Champs:
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Ajouter au panier
   * Schéma : transactions numériques client
   * Champs:
      * `EventType`
   * Condition:
      * `EventType = commerce.productListAdds`
      * Champs:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Engagement de marque
   * Schéma : transactions numériques client
   * Champs:
      * `EventType`
   * Condition:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Champs:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Logique du Parcours clé

* Logique d’entrée de parcours
   * Événement d’affichage de produit

* Conditions
   * Recherchez au moins un événement d’achat en ligne ou hors ligne depuis la dernière consultation du produit.
      * Schéma : transactions numériques client
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Recherchez au moins un achat hors ligne depuis la dernière consultation du produit :
      * Schéma : Transactions hors ligne client v.1
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Conditions - Sélectionnez le canal cible
      * E-mail
         * `consents.marketing.email.val = y`
      * Push
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Personnalisation des canaux
      * Contenu de canal personnalisé basé sur la consultation du produit.

+++

>[!TAB Parcours de panier abandonné]

+++Événements

* Ajouter au panier
   * Schéma : transactions numériques client
   * Champs:
      * `EventType`
   * Condition:
      * `EventType = commerce.productListAdds`
      * Champs:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Achats en ligne
   * Schéma : transactions numériques client
   * Champs:
      * `EventType`
   * Condition:
      * `EventType = commerce.purchases`
      * Champs:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Engagement de marque
   * Schéma : transactions numériques client
   * Champs:
      * `EventType`
   * Condition:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Champs:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Logique de Parcours clé

* Logique d’entrée de parcours
   * `AddToCart` Événement

* AuthenticatedState dans authentifié

* Condition : achats hors ligne depuis la dernière abandon du panier :
   * Schéma : Transactions hors ligne client v.1
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Condition : le panier est effacé depuis la dernière abandon du panier :
   * Schéma : Transactions numériques client v.1
   * `eventType = commerce.cartCleared`
   * `cartID` (Identifiant du panier)
   * `timestamp > timestamp of cart was last abandoned`

* Sélectionner le canal cible (sélectionnez un ou plusieurs canaux pour une portée plus large)
   * E-mail
      * `consents.marketing.email.val = y`
   * Push
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Personnalisation des canaux
      * Affichez les informations détaillées du panier et affichez plusieurs produits sous la forme d’un tableau.

+++

>[!TAB Parcours de confirmation de commande]

+++Événements

* Achats en ligne
   * Schéma : transactions numériques client
   * Champs:
      * `EventType`
   * Condition:
      * `EventType = commerce.purchases`
      * Champs:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++Logique du Parcours clé

* Logique d’entrée de parcours
   * Événement de commande

* Conditions
   * Sélectionnez Canal cible (sélectionnez un ou plusieurs canaux pour une portée plus large).
      * La confirmation de commande est considérée comme étant de nature à servir. La vérification du consentement est donc généralement inutile.
      * E-mail
      * Push
      * SMS

   * Personnalisation du contenu du canal
      * Affichez les informations sur les commandes et affichez une liste de produits au format tabulaire.

+++

>[!ENDTABS]

Pour plus d’informations sur la création de parcours dans [Adobe Journey Optimizer], lisez le [Guide de prise en main de parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr).

### Configuration des publicités multimédia payantes dans les destinations

La structure des destinations est utilisée pour les publicités multimédia payantes. Une fois le consentement vérifié, il est envoyé vers les différentes destinations configurées. Par exemple, courrier, courrier électronique, notification push et SMS.

#### Données requises pour les destinations

Les destinations d’exportation de segments en flux continu (telles que Facebook, Google Customer Match, Google DV360) prennent en charge diverses identités à partir des données client :

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Le segment Abandon du panier est en flux continu et peut donc être utilisé par la structure Destination pour ce cas d’utilisation.

* Diffusion/Déclenché
   * [Publicité](/help/destinations/catalog/advertising/overview.md)/[Médias payants et réseaux sociaux](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destination de diffusion en continu](/help/destinations/catalog/streaming/http-destination.md)
   * [Destination SDK personnalisée](/help/destinations/destination-sdk/overview.md)

* Fichier/Planifié toutes les trois heures
   * [Marketing par e-mail](/help/destinations/catalog/email-marketing/overview.md)
