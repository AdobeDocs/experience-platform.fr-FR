---
title: Faire évoluer la valeur client unique vers la valeur de durée de vie
description: Découvrez comment créer des campagnes personnalisées pour offrir les meilleurs produits ou services complémentaires en fonction des attributs, du comportement et des achats passés d’un client spécifique.
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3181'
ht-degree: 2%

---

# Faire évoluer la valeur client unique vers la valeur de durée de vie

>[!IMPORTANT]
> 
>* Cette page présente un exemple d’implémentation de Real-Time CDP et Adobe Journey Optimizer pour réaliser le cas d’utilisation décrit. Utilisez les chiffres, les critères de qualification et les autres champs fournis sur la page comme guide, et non comme des chiffres normatifs.
>* Pour réaliser ce cas d’utilisation, vous devez disposer d’une licence pour Real-Time CDP et Adobe Journey Optimizer. Pour en savoir plus, consultez la section [Conditions préalables et planification](#prerequisites-and-planning) ci-dessous.

Implémentez le cas d’utilisation de valeur client unique à valeur de durée de vie pour stimuler l’engagement et la fidélité de la marque. Créez une expérience client connectée sur plusieurs canaux ou parcours en utilisant la puissance d’Experience Platform, augmentée de [Real-Time CDP](/help/rtcdp/home.md) et [Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/ajo-home).

Les personnes que vous ciblez sont les visiteurs occasionnels de vos propriétés qui ont effectué des achats au cours des trois derniers mois.

Pensez à ces clients qui visitent vos propriétés et qui achètent de façon sporadique les produits ou services que vous offrez. Vous pouvez créer des campagnes personnalisées pour séduire ces clients afin que votre marque puisse leur offrir une valeur à plus long terme plutôt qu’une valeur unique. Découvrez comment :

* Collecter et gérer des données
* Créer des audiences
* Créez des parcours pour cibler ces audiences dans Adobe Journey Optimizer et les activer dans Real-Time CDP.

![Faites évoluer pas à pas la valeur unique vers la valeur de durée de vie. Aperçu visuel de haut niveau.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## Prérequis et planification {#prerequisites-and-planning}

En considérant qu’en interne, vous avez défini un objectif commercial afin d’accroître la fidélité à la marque. Cela peut se traduire par l’exécution d’un cas d’utilisation pour stimuler l’engagement et la fidélité des clients.

Pour ce faire, la technologie requise se compose des deux applications Experience Platform [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=fr). Vous trouverez ci-dessous divers éléments de fonctionnalité et d’interface utilisateur des deux applications que vous utiliserez lors de l’implémentation du cas d’utilisation.

>[!TIP]
>
>Assurez-vous que vous disposez des [autorisations de contrôle d’accès basées sur des attributs](/help/access-control/abac/end-to-end-guide.md) pour toutes ces zones ou demandez à votre administrateur ou administratrice système de vous accorder les autorisations nécessaires.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) : Intégrez des données entre les sources de données pour alimenter la campagne. Ces données sont ensuite utilisées pour créer les audiences de la campagne et les éléments de données personnalisés de la surface utilisés dans l’e-mail et les vignettes de promotion web (par exemple, les informations relatives au nom ou au compte). Enfin, Real-Time CDP est également utilisé pour activer des audiences vers des destinations de médias achetés.
   * [Schémas](/help/xdm/home.md)
   * [Profils](/help/profile/home.md)
   * [Jeux de données](/help/catalog/datasets/overview.md)
   * [Audiences](/help/segmentation/home.md)
   * [Destinations](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) : concevez des parcours, configurez des déclencheurs et créez les messages adéquats pour répondre aux besoins de vos visiteurs.
   * [Déclencheur d’événement ou d’audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [ Audiences et événements ](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=fr)
   * [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Architecture de Real-Time CDP et de Journey Optimizer

Vous trouverez ci-dessous une vue d’ensemble de l’architecture des différents composants de Real-Time CDP et Journey Optimizer. Ce diagramme montre le flux de données entre les deux applications Experience Platform, de la collecte de données jusqu’au point où elles sont activées par le biais de parcours ou de campagnes vers les destinations, afin de réaliser le cas d’utilisation décrit sur cette page.

![Présentation visuelle de haut niveau de l’architecture.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## Comment réaliser le cas d’utilisation : vue d’ensemble de haut niveau {#achieve-the-use-case-high-level}

Vous trouverez ci-dessous une présentation générale du workflow, qui combine un workflow de parcours et un workflow d’activation.

Dans l’exemple de workflow illustré ci-dessous, vous recherchez les clients qui répondent à un certain critère et vous souhaitez les inciter à revenir sur votre site web ou votre application. Vous souhaitez les définir sur un parcours où, au lieu d’une activité limitée sur votre propriété, ils reviennent de manière plus récurrente. Vous tentez de les ramener à votre propriété, puis une fois qu&#39;ils sont de retour, vous les faites entrer dans le parcours pour faire des achats récurrents sur votre site. La campagne configurée ici est limitée à un engagement avec les clients par mois.

Commencez par envoyer un message à votre audience de clients à forte valeur ajoutée et à faible fréquence. Vous pouvez ensuite vérifier s’ils ont reçu ce message au cours des trente derniers jours. Si ce n&#39;est pas le cas, vous pouvez les inscrire dans un parcours portant, par exemple, sur un nouveau programme d&#39;abonnement. Vous pouvez ensuite attendre quelques jours (sept jours dans cet exemple). Passé ce délai, s’il n’a pas acheté l’abonnement pour lequel vous lui avez envoyé un message, vous pouvez diffuser des annonces publicitaires médias payantes via des destinations. S’il a acheté l’abonnement, vous pouvez lui demander de saisir un parcours de confirmation de commande, complétant ainsi le cas d’utilisation.

>[!IMPORTANT]
>
>Comme décrit plus en détail ci-dessous sur cette page, en disposant d’un [groupe de champs de consentement dédié](#customer-attributes-schema) dans votre schéma et en [implémentant des politiques de consentement](#privacy-consent), toutes les actions et tous les workflows sont implémentés de manière respectueuse de la confidentialité et en accordant la priorité au consentement.

>[!BEGINSHADEBOX]

![Faites évoluer pas à pas la valeur unique vers la valeur de durée de vie. Aperçu visuel de haut niveau.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. Vous créez des schémas et des jeux de données, puis vous les marquez pour [!UICONTROL Profil].
2. Les données sont collectées et intégrées dans Experience Platform via Web SDK, Mobile Edge SDK ou l’API. Analytics Data Connector peut également être utilisé, mais peut entraîner une latence du parcours.
3. Vous chargez des profils dans Real-Time CDP et créez des politiques de gouvernance pour en assurer une utilisation responsable.
4. Vous créez des audiences ciblées à partir de la liste des profils pour rechercher des clients à forte valeur ajoutée et à faible fréquence.
5. Vous créez deux parcours dans [!DNL Adobe Journey Optimizer] : l’un pour informer les utilisateurs d’un nouveau programme d’abonnement et l’autre pour leur envoyer un message afin de confirmer l’achat ultérieurement.
6. Si vous le souhaitez, vous activez l’audience des clients qui n’ont pas acheté votre abonnement aux destinations de médias achetés souhaitées.

>[!ENDSHADEBOX]

## Comment réaliser le cas d’utilisation {#achieve-use-case-instruction}

Pour suivre chacune des étapes de la présentation de haut niveau ci-dessus, lisez les sections ci-dessous qui contiennent des liens vers des informations supplémentaires et des instructions plus détaillées.

### Fonctionnalités et éléments de l’interface utilisateur que vous utiliserez {#ui-functionality-and-elements}

Au fur et à mesure que vous mettrez en œuvre le cas d’utilisation, vous utiliserez le Real-Time CDP, la fonctionnalité Adobe Journey Optimizer et les éléments de l’interface utilisateur répertoriés au début de ce document. Assurez-vous de disposer des autorisations de contrôle d’accès basé sur les attributs nécessaires pour toutes ces zones ou demandez à votre administrateur système de vous accorder les autorisations nécessaires.

### Créer une conception de schéma et spécifier des groupes de champs {#schema-design}

Les ressources du modèle de données d’expérience (XDM) sont gérées dans l’espace de travail [!UICONTROL Schémas] de [!DNL Adobe Experience Platform]. Vous pouvez afficher et explorer les ressources de base fournies par [!DNL Adobe] (par exemple, [!UICONTROL groupes de champs]) et créer des ressources et des schémas personnalisés pour votre organisation.

Pour plus d’informations sur la création de [schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr), consultez le tutoriel [création de schémas](/help/xdm/tutorials/create-schema-ui.md).

Il existe plusieurs conceptions de schéma que vous pouvez utiliser dans cet exemple d’implémentation pour le cas d’utilisation afin de transformer une valeur unique en valeur de durée de vie. Chaque schéma comprend des champs spécifiques requis à configurer, ainsi que certains champs suggérés.

En fonction d’exemples d’implémentation, Adobe vous suggère de créer les trois schémas suivants pour réaliser ce cas d’utilisation :

* [Schéma des attributs du client](#customer-attributes-schema) (schéma de profil)
* [Schéma de transactions numériques client](#customer-digital-transactions-schema) (schéma d’événement d’expérience)
* [Schéma des transactions client hors ligne](#customer-offline-transactions-schema) (schéma d’événement d’expérience)

#### Schéma des attributs du client {#customer-attributes-schema}

Utilisez ce schéma pour structurer et référencer les données de profil qui constituent vos informations client. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via votre CRM ou un système similaire et sont nécessaires pour référencer les détails des clients utilisés pour la personnalisation, le consentement marketing et les fonctionnalités améliorées de segmentation.

![Schéma Attributs du client avec les groupes de champs mis en surbrillance](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

Le schéma des attributs du client est représenté par une classe [!UICONTROL XDM Individual Profile] qui comprend les groupes de champs suivants :

+++Détails démographiques (groupe de champs)

[Détails démographiques](/help/xdm/field-groups/profile/demographic-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile. Le groupe de champs fournit un objet personne au niveau racine, dont les sous-champs décrivent des informations sur une personne individuelle.

+++

+++Coordonnées personnelles (groupe de champs)

[Coordonnées personnelles](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile, qui décrit les informations de contact d’une personne individuelle.

+++

+++Détails de l’audit du système Source externe (groupe de champs)

[Attributs d’audit du système Source externe](/help/xdm/data-types/external-source-system-audit-attributes.md) est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails d’audit d’un système source externe.

+++

+++Groupes de champs de consentement et de préférence (groupe de champs)

Le groupe de champs [ Consentements et préférences ](/help/xdm/field-groups/profile/consents.md) fournit un seul champ de type objet, consentements, pour capturer les informations de consentement et de préférence.

+++

#### Schéma des transactions numériques client {#customer-digital-transactions-schema}

Ce schéma est utilisé pour structurer et référencer les données d’événement qui composent l’activité de votre client ou cliente qui se produit sur votre site web ou sur d’autres plateformes numériques associées. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via [Web SDK](/help/web-sdk/home.md) et sont nécessaires pour référencer les différents événements de navigation et de conversion utilisés pour le déclenchement de parcours, l’analyse détaillée des clients en ligne et les fonctionnalités améliorées de segmentation.

![Schéma de transactions numériques client avec les groupes de champs mis en surbrillance](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

Le schéma des transactions numériques client est représenté par une classe [!UICONTROL XDM ExperienceEvent] qui comprend les groupes de champs suivants :

ExperienceEvent Adobe Experience Platform Web SDK (groupe de champs)

| Champs | Exigence |
| --- | --- |
| `device.model` | Suggéré |
| `environment.browserDetails.userAgent` | Suggéré |

+++

+++Détails web (groupe de champs)

[Détails web](/help/xdm/field-groups/event/web-details.md) est un groupe de champs de schéma standard pour la classe XDM ExperienceEvent, utilisé pour décrire les informations concernant les événements de détails web tels que les interactions, les détails de page et le référent.

+++

+++Événement d’expérience client (groupe de champs)

Ce groupe de champs comprend diverses informations sur les actions (comme les événements d’achat ou de navigation) effectuées par les utilisateurs sur votre propriété web.

| Champ | Exigence |
| --- | --- |
| `commerce.cart.cartID` | Suggéré |
| `commerce.cart.cartSource` | Suggéré |
| `commerce.cartAbandons.id` | Suggéré |
| `commerce.cartAbandons.value` | Suggéré |
| `commerce.order.orderType` | Suggéré |
| `commerce.order.payments.paymentAmount` | Suggéré |
| `commerce.order.payments.paymentType` | Suggéré |
| `commerce.order.payments.transactionID` | Suggéré |
| `commerce.order.priceTotal` | Suggéré |
| `commerce.order.purchaseID` | Suggéré |
| `commerce.productListAdds.id` | Suggéré |
| `commerce.productListAdds.value` | Suggéré |
| `commerce.productListOpens.id` | Suggéré |
| `commerce.productListOpens.value` | Suggéré |
| `commerce.productListRemoval.id` | Suggéré |
| `commerce.productListRemoval.value` | Suggéré |
| `commerce.productListViews.id` | Suggéré |
| `commerce.productListViews.value` | Suggéré |
| `commerce.productViews.id` | Suggéré |
| `commerce.productViews.value` | Suggéré |
| `commerce.purchases.id` | Suggéré |
| `commerce.purchases.value` | Suggéré |
| `marketing.campaignGroup` | Suggéré |
| `marketing.campaignName` | Suggéré |
| `marketing.trackingCode` | Suggéré |
| `productListItems.name` | Suggéré |
| `productListItems.priceTotal` | Suggéré |
| `productListItems.product` | Suggéré |
| `productListItems.quantity` | Suggéré |

+++

+++Détails de l’ID de l’utilisateur final (groupe de champs)

Le groupe de champs [Détails de l’ID de l’utilisateur final](/help/xdm/field-groups/event/enduserids.md) comprend différentes informations sur vos utilisateurs, telles que s’ils sont authentifiés sur votre site lors de leur visite, et des informations sur leur identité.

+++

+++Détails de l’audit du système Source externe (groupe de champs)

Attributs d’audit du système Source externe est un type de données standard des modèles de données d’expérience (XDM) qui capture les détails d’audit d’un système source externe.

+++

#### Schéma des transactions client hors ligne {#customer-offline-transactions-schema}

Ce schéma est utilisé pour structurer et référencer les données d’événement qui composent l’activité de votre client ou cliente qui se produit sur des plateformes en dehors de votre site web. Ces données sont généralement ingérées dans des [!DNL Adobe Experience Platform] à partir d’un point de vente (ou d’un système similaire) et le plus souvent diffusées en continu dans Experience Platform via une connexion API. En savoir plus sur l’[ingestion par lots](/help/ingestion/batch-ingestion/getting-started.md). Son objectif est de référencer les différents événements de conversion hors ligne utilisés pour déclencher des parcours, une analyse client approfondie en ligne et hors ligne, ainsi que des fonctionnalités améliorées de segmentation.

![Schéma des transactions hors ligne du client avec les groupes de champs mis en surbrillance](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

Le schéma des transactions hors ligne du client est représenté par une classe [!UICONTROL XDM ExperienceEvent] qui comprend les groupes de champs suivants :

Détails du Commerce (groupe de champs)

[Détails Commerce](/help/xdm/field-groups/event/commerce-details.md) est un groupe de champs de schéma standard pour la classe [!DNL XDM ExperienceEvent], utilisé pour décrire des données commerciales telles que des informations sur le produit (SKU, nom, quantité) et des opérations de panier standard (commande, passage en caisse, abandon).

+++

+++Coordonnées personnelles (groupe de champs)

[[!UICONTROL Coordonnées personnelles]](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe [!DNL XDM Individual Profile], qui décrit les informations de contact d’une personne individuelle.

+++

+++Détails de l’audit du système Source externe (groupe de champs)

Attributs d’audit du système Source externe est un type de données standard des modèles de données d’expérience (XDM) qui capture les détails d’audit d’un système source externe.

+++

#### Schéma du connecteur web Adobe {#adobe-web-connector-schema}

>[!NOTE]
>
>Il s’agit d’une implémentation facultative si vous utilisez le [!DNL Adobe Analytics Data Connector] .

Ce schéma est utilisé pour structurer et référencer les données d’événement qui composent l’activité de votre client ou cliente qui se produit sur votre site web ou sur d’autres plateformes numériques associées. Ce schéma est similaire au schéma Transactions numériques client , mais il diffère en ce qu’il peut lorsque SDK Web n’est pas une option pour la collecte de données. Par conséquent, vous pouvez utiliser ce schéma lorsque vous utilisez le [!DNL Adobe Analytics Data Connector] pour envoyer vos données en ligne dans [!DNL Adobe Experience Platform] en tant que flux de données principal ou secondaire.

![Schéma du connecteur web Adobe avec groupes de champs mis en surbrillance](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

Le schéma de connecteur web [!DNL Adobe] est représenté par une classe [!UICONTROL XDM ExperienceEvent] qui comprend les groupes de champs suivants :

Modèle ExperienceEvent Adobe Analytics (groupe de champs)

[[!UICONTROL Extension complète Adobe Analytics ExperienceEvent]](/help/xdm/field-groups/event/analytics-full-extension.md) est un groupe de champs de schéma standard, qui capture les mesures courantes collectées par Adobe Analytics.

+++

### Création d’un jeu de données à partir d’un schéma {#dataset-from-schema}

Un jeu de données est une structure de stockage et de gestion pour un groupe de données. Chaque schéma utilisé pour réaliser cet exemple d’implémentation comporte un seul jeu de données.

Pour plus d’informations sur la création d’un [jeu de données](/help/catalog/datasets/overview.md) à partir d’un schéma, consultez le [guide de l’interface utilisateur des jeux de données](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Comme pour l’étape de création d’un schéma, vous devez activer l’inclusion du jeu de données dans le profil client en temps réel. Pour plus d’informations sur l’activation du jeu de données en vue de son utilisation dans le profil client en temps réel, consultez le tutoriel [création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Confidentialité, consentement et gouvernance des données {#privacy-consent}

#### Politiques de consentement

>[!IMPORTANT]
>
>La possibilité pour les clients de se désabonner de la réception des communications d’une marque, ainsi que le respect de ce choix, sont des exigences légales. Pour en savoir plus sur la législation applicable, consultez la [présentation des réglementations relatives à la confidentialité](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Pensez à mettre en œuvre les [politiques de consentement](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) suivantes et à demander le consentement de vos visiteurs avant de communiquer avec eux :

* Si `consents.marketing.email.val = "Y"`, peut envoyer un e-mail à
* Si `consents.marketing.sms.val = "Y"`, peut envoyer des SMS.
* Si `consents.marketing.push.val = "Y"`, peut envoyer une notification push.
* Si `consents.share.val = "Y"`, peut publier

#### Étiquette et application de la gouvernance des données

Envisagez d’ajouter et d’appliquer les [libellés de gouvernance des données](/help/data-governance/labels/overview.md) suivants :

* Les adresses e-mail personnelles sont utilisées comme données directement identifiables utilisées pour identifier ou entrer en contact avec un individu spécifique plutôt qu’avec un appareil.
   * `personalEmail.address = I1`

#### Politiques marketing

Aucune [ politique marketing ](/help/data-governance/policies/overview.md) n’est requise pour les parcours que vous créez dans le cadre de ce cas d’utilisation. Cependant, vous pouvez tenir compte des politiques suivantes selon vos besoins :

* Limitation Des Données Sensibles
* Restreindre l’Advertising sur site
* Restreindre le ciblage par e-mail
* Limiter le ciblage intersite
* Limiter la combinaison de données directement identifiables avec des données anonymes

### Créer des audiences {#create-audiences}

Ce cas d’utilisation nécessite la création de deux audiences pour définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de clients potentiels. Les audiences peuvent être créées de plusieurs manières dans Adobe Experience Platform :

* Pour plus d’informations sur la création d’une audience, consultez le [guide de l’interface utilisateur du service d’audience](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).
* Pour plus d’informations sur la composition d’audiences [audiences](/help/segmentation/home.md), consultez le [guide de l’interface utilisateur sur la composition d’audiences](/help/segmentation/ui/audience-composition.md).
* Pour plus d’informations sur la création d’audiences par le biais de définitions de segment dérivées d’Experience Platform, consultez le [guide de l’interface utilisateur du créateur d’audience](/help/segmentation/ui/segment-builder.md).

Plus précisément, vous devez créer et utiliser deux audiences à différentes étapes du cas d’utilisation, comme illustré dans l’image ci-dessous.

![Audiences mises en surbrillance.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Audience admissible Adobe Journey Optimizer]

Cette audience à forte valeur ajoutée et à faible fréquence inclut les profils que vous souhaitez contacter par le biais d’un parcours, pour les informer d’un nouveau programme d’abonnement. Les détails de l’audience sont les suivants :

* Description : profils ayant dépensé plus de 250 $ au total au cours des 3 derniers mois
* Champs et conditions nécessaires dans l’audience :
   * Événement : `commerce.order.payments.paymentamount`
* Somme Totale : >= 250 $
   * EventType : `commerce.purchases`
* Date et heure : moins de 3 mois avant maintenant


>[!TAB Audience média payante]

Cette audience est créée pour inclure les profils qui ont dépensé plus de 250 $ au total au cours des 3 derniers mois et qui n’ont pas effectué d’achat au cours des 7 derniers jours. Les détails de l’audience sont les suivants :

* Description : profils qui ont dépensé plus de 250 $ au total au cours des 3 derniers mois et qui n’ont pas effectué d’achat au cours des 7 derniers jours.
* Champs et conditions nécessaires :
   * EventType : `journey.feedback`
      * Opérande : = true
   * Événement : `experience.journeyOrchestration.stepEvents.nodeName`
      * Opérande : = JourneyStepEventTracker - Abonnement non acheté
      * Date et heure : au cours des 7 derniers jours
   * EventType n’est pas : `commerce.purchases`
      * Date et heure : &lt;= 7 jours avant maintenant
   * Événement : SKU
      * Valeur : = `subscription`

>[!ENDTABS]

### Configuration du parcours dans Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] n’englobe pas tout ce qui est indiqué dans les diagrammes. Toutes les [annonces publicitaires médias payantes](/help/destinations/catalog/social/overview.md) sont créées dans l’espace de travail [!UICONTROL destinations] [. ](/help/destinations/ui/destinations-workspace.md)

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) vous permet de proposer des expériences connectées, contextuelles et personnalisées à vos clients. Le parcours client est l’ensemble du processus d’interaction d’un client avec la marque. Chaque parcours de cas d’utilisation nécessite des informations spécifiques.

Pour accomplir ce cas d’utilisation, vous devez créer deux parcours distincts :

* Le parcours de durée de vie, qui inclut le message que vous envoyez à vos clients haute valeur et basse fréquence
* Le parcours de confirmation de commande pour les utilisateurs qui répondent à votre appel et achètent un abonnement.

![Parcours mis en surbrillance.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

Vous trouverez ci-dessous les données précises nécessaires pour chaque branche de Parcours.

>[!BEGINTABS]

>[!TAB Parcours de vie]

Le parcours de durée de vie s’adresse à l’audience des clients à forte valeur ajoutée et à faible fréquence qui n’ont pas été ciblés au cours des 30 derniers jours. Un message s’affiche pour ces clients. Si, au bout de 7 jours, ils ne procèdent toujours pas à leur achat, vous pouvez inclure les non-acheteurs dans une audience à laquelle vous pouvez afficher des annonces publicitaires payantes. S&#39;il effectue un achat, vous pouvez définir les acheteurs sur un parcours de confirmation de commande, détaillé dans l&#39;onglet séparé.

![Présentation visuelle de haut niveau du parcours de durée de vie.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "Présentation visuelle de haut niveau de la valeur ponctuelle au parcours de durée de vie."){zoomable="yes"}

+++Logique de Parcours détaillée

Le parcours illustré ci-dessus suit la logique suivante.

1. Lecture d’audience : utilisez une [activité Lecture d’audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=en) pour la première audience créée dans la section audiences ci-dessus.

2. Condition - Canal préféré : utilisez une [activité de condition](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html) pour déterminer comment contacter les clients, que ce soit par e-mail, SMS ou notifications push. Utilisez trois activités d’action pour créer les trois branches.

3. Attente : utilisez une [activité d’attente](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html) pour attendre d’écouter les achats.

4. Condition - Abonnement acheté au cours des 7 derniers jours ? : utilisez une activité de condition pour écouter les achats de produits au cours des 7 derniers jours.

5. JourneyStepEventTracker - Abonnement non acheté : utilisez une [action personnalisée](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html) pour les visiteurs qui n’ont pas encore acheté votre abonnement, bien qu’ils aient reçu votre message. Dans le cadre de la condition personnalisée en fin de parcours, créez un événement `journey.feedback` et ajoutez-le à un jeu de données basé sur le schéma [!UICONTROL Événement d’étape de Parcours &#x200B;]. Vous utiliserez cet événement pour segmenter l’audience qui n’a pas acheté l’abonnement et que vous pouvez cibler via des annonces médias payantes.

+++

>[!TAB Parcours de confirmation de commande]

Le parcours de confirmation de commande se concentre sur le fait de savoir si un achat a été effectué via le site web ou l&#39;application mobile. Une fois qu’un client a effectué avec succès l’achat, par exemple, d’un abonnement auprès de votre société, vous pouvez le configurer sur un parcours de confirmation de commande.

![Présentation visuelle de haut niveau du parcours de confirmation de commande client.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "Présentation visuelle de haut niveau du parcours de confirmation de commande client."){zoomable="yes"}

Logique de Parcours ++

Utilisez les événements, champs et actions suggérés ci-dessous dans votre parcours de confirmation :

* Le parcours est déclenché par un événement d’achat en ligne
   * Schéma : Transactions numériques client
   * Champs :
      * `EventType`
   * Condition :
      * `EventType = commerce.purchases`
      * Champs :
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

+++Logique de Parcours de clé

* Logique d&#39;entrée de parcours
   * Événement de commande

* Conditions
   * Sélectionnez Canal cible (vous pouvez sélectionner un ou plusieurs canaux pour une portée plus large).
      * La confirmation de commande étant considérée comme une diffusion par nature, la vérification du consentement est généralement inutile.
      * E-mail
      * Notification push
      * SMS

   * Personalization de contenu de canal
      * Affichez les informations détaillées sur la commande et pouvez afficher une liste de produits au format tableau.

+++

>[!ENDTABS]

Pour plus d’informations sur la création de parcours dans [!DNL Adobe Journey Optimizer], consultez le guide [Prise en main des parcours ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) .

### Configurer une destination pour l’affichage des publicités multimédia payantes {#paid-media-ads}

Il se peut que certains utilisateurs n’aient pas acheté votre abonnement même après leur avoir notifié le nouveau programme. Après un certain nombre de jours d’attente (sept dans cet exemple de cas d’utilisation), vous pouvez décider de montrer des annonces publicitaires médias payantes à ces utilisateurs ou utilisatrices, afin de les encourager à acheter votre abonnement.

Utilisez le framework de destinations dans Real-Time CDP pour les annonces publicitaires multimédia payantes. Sélectionnez l’une des nombreuses destinations publicitaires disponibles pour afficher des annonces de médias payants à vos clients et activer l’audience de médias payants que vous [avez créée précédemment](#create-audiences) vers une destination de votre choix. Consultez un aperçu des destinations [publicitaires](/help/destinations/catalog/advertising/overview.md) et [sociales](/help/destinations/catalog/social/overview.md) disponibles.

Pour savoir comment activer des données vers des destinations (par exemple [The Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) ou [Google Customer Match](/help/destinations/catalog/advertising/google-customer-match.md)), lisez la documentation ci-dessous :

* [Créer une connexion à une destination](/help/destinations/ui/connect-destination.md)
* [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md)

## Étapes suivantes {#next-steps}

En plaçant vos utilisateurs peu fréquents et à forte valeur ajoutée sur un parcours et en affichant des annonces publicitaires multimédia payantes pour un sous-ensemble d’entre eux, vous avez, espérons-le, fait passer certains d’entre eux de la valeur ponctuelle à la valeur à vie, améliorant ainsi les mesures de fidélité à la marque et d’engagement client.

Ensuite, vous pouvez explorer d’autres cas d’utilisation pris en charge par Real-Time CDP, tels que [réengagement intelligent des clients](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) ou [affichage de contenu personnalisé pour les utilisateurs non authentifiés](/help/rtcdp/partner-data/onsite-personalization.md) sur vos propriétés web.
