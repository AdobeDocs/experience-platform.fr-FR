---
title: Évoluer la valeur client unique à la valeur de durée de vie
description: Découvrez comment créer des campagnes personnalisées pour offrir les meilleurs produits ou services complémentaires en fonction des attributs, du comportement et des achats antérieurs d’un client spécifique.
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: 8cd0da12784d8fac3f0ce9afeb881d7a3916795f
workflow-type: tm+mt
source-wordcount: '3179'
ht-degree: 2%

---

# Évoluer la valeur client unique à la valeur de durée de vie

>[!IMPORTANT]
> 
>* Cette page présente un exemple de mise en oeuvre de Real-Time CDP et Adobe Journey Optimizer pour réaliser le cas d’utilisation décrit. Utilisez les chiffres, les critères de qualification et les autres champs figurant sur la page comme un guide et non comme des chiffres normatifs.
>* Pour remplir ce cas d’utilisation, vous devez disposer d’une licence pour Real-Time CDP et Adobe Journey Optimizer. En savoir plus dans la section [section conditions préalables et planification](#prerequisites-and-planning) plus loin.

Mettez en oeuvre le cas d’utilisation de la valeur client unique par rapport à la valeur de durée de vie pour stimuler l’engagement de la marque et la fidélité à la marque. Créer une expérience client connectée sur plusieurs canaux ou parcours en utilisant la puissance d’Experience Platform, augmentée par [Real-Time CDP](/help/rtcdp/home.md) et [Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/ajo-home).

Les personnes que vous ciblez sont les rares visiteurs de vos propriétés qui ont effectué des achats au cours des trois derniers mois.

Tenez compte de ces clients qui visitent vos propriétés et achètent sporadiquement les produits ou services que vous proposez. Vous pouvez créer des campagnes personnalisées pour séduire ces clients afin que votre marque leur offre une valeur à plus long terme au lieu d’une valeur ponctuelle. Découvrez comment :

* Collecte et gestion des données
* Créer des audiences
* Créez des parcours pour cibler ces audiences dans Adobe Journey Optimizer et les activer dans Real-Time CDP.

![Étape par étape Évoldez la valeur ponctuelle pour obtenir la valeur de durée de vie d’un aperçu visuel de haut niveau.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## Prérequis et planification {#prerequisites-and-planning}

En considérant que vous avez défini en interne un objectif et un objectif professionnels pour accroître la fidélité à la marque. Cela peut se traduire par l’exécution d’un cas d’utilisation afin de fidéliser les clients et leur engagement.

Pour ce faire, la technologie requise se compose des deux applications Experience Platform. [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=fr) et [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=fr). Vous trouverez ci-dessous différentes fonctionnalités et éléments d’interface utilisateur des deux applications que vous utiliserez lors de la mise en oeuvre du cas d’utilisation.

>[!TIP]
>
>Assurez-vous que vous disposez des [autorisations de contrôle d’accès basées sur des attributs](/help/access-control/abac/end-to-end-guide.md) pour toutes ces zones ou demandez à votre administrateur ou administratrice système de vous accorder les autorisations nécessaires.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html): intégrez des données à l’échelle des sources de données pour alimenter la campagne. Ces données sont ensuite utilisées pour créer les audiences de campagne et faire apparaître les éléments de données personnalisés utilisés dans l&#39;email et les mosaïques de promotion web (par exemple, le nom ou les informations liées au compte). Enfin, Real-Time CDP est également utilisé pour activer les audiences vers les destinations de médias payants.
   * [Schémas](/help/xdm/home.md)
   * [Profils](/help/profile/home.md)
   * [Jeux de données](/help/catalog/datasets/overview.md)
   * [Audiences](/help/segmentation/home.md)
   * [Destinations](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html): concevez des parcours, configurez des triggers et créez un message approprié pour s’adresser à vos visiteurs.
   * [Déclencheur d’événement ou d’audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Audiences et événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=fr)
   * [Parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

## Architecture de Real-Time CDP et Journey Optimizer

Vous trouverez ci-dessous une vue d’architecture de haut niveau des différents composants de Real-Time CDP et Journey Optimizer. Ce diagramme montre comment les données transitent par les deux applications Experience Platform, de la collecte de données jusqu’au point où elles sont activées par le biais de parcours ou de campagnes vers des destinations, afin d’atteindre le cas d’utilisation décrit sur cette page.

![Présentation visuelle de haut niveau de l’architecture.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## Comment réaliser le cas d’utilisation : vue d’ensemble de haut niveau {#achieve-the-use-case-high-level}

Vous trouverez ci-dessous un aperçu général du workflow, une combinaison d’un workflow de parcours et d’un workflow d’activation.

Dans l’exemple de workflow illustré ci-dessous, vous recherchez des clients qui répondent à certains critères et vous souhaitez les inciter à revenir sur votre site web ou votre application. Vous souhaitez les définir sur un parcours où, au lieu d’une activité limitée sur votre propriété, ils reviennent de manière plus récurrente. Vous essayez de les ramener à votre propriété, puis, une fois qu’ils sont de retour, vous leur demandez de saisir le parcours pour effectuer des achats récurrents sur votre site. La configuration de la campagne ici est limitée à un engagement avec les clients par mois.

Vous commencez par envoyer un message à votre audience de clients à forte et à faible fréquence. Vous pouvez ensuite vérifier s’ils ont reçu ce message au cours des trente derniers jours. Si ce n’est pas le cas, vous pouvez les entrer dans un parcours à propos, par exemple, d’un nouveau programme d’abonnement. Vous pouvez ensuite attendre quelques jours (sept jours dans cet exemple). Après ce délai, s’ils n’ont pas acheté l’abonnement sur lequel vous leur avez envoyé un message, vous pouvez diffuser des publicités multimédia payantes via des destinations. S’ils ont acheté l’abonnement, vous pouvez leur demander de saisir un parcours de confirmation de commande, complétant ainsi le cas pratique.

>[!IMPORTANT]
>
>Comme décrit plus loin sur cette page, en définissant une variable [groupe de champs de consentement dédié dans votre schéma](#customer-attributes-schema) et par [mise en oeuvre de stratégies de consentement](#privacy-consent), toutes les actions et tous les workflows sont implémentés d’une manière privilégiée en matière de confidentialité et de consentement.

>[!BEGINSHADEBOX]

![Étape par étape Évoldez la valeur ponctuelle pour obtenir la valeur de durée de vie d’un aperçu visuel de haut niveau.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. Vous créez des schémas et des jeux de données, puis les marquez pour [!UICONTROL Profil].
2. Les données sont collectées et intégrées dans Experience Platform par le biais du SDK Web, du SDK Mobile Edge ou de l’API. Le connecteur de données Analytics peut également être utilisé, mais peut entraîner une latence de parcours.
3. Vous chargez des profils dans Real-Time CDP et créez des stratégies de gouvernance pour garantir une utilisation responsable.
4. Vous créez des audiences ciblées à partir de la liste des profils pour rechercher des clients à forte valeur et à faible fréquence.
5. Vous créez deux parcours dans [!DNL Adobe Journey Optimizer], l’une pour envoyer un message aux utilisateurs au sujet d’un nouveau programme d’abonnement, l’autre pour leur envoyer un message pour confirmer l’achat ultérieurement.
6. Si vous le souhaitez, vous activez l’audience des clients qui n’ont pas acheté votre abonnement à des destinations de médias payants souhaitées.

>[!ENDSHADEBOX]

## Comment réaliser le cas d’utilisation {#achieve-use-case-instruction}

Pour terminer chacune des étapes de la présentation de haut niveau ci-dessus, consultez les sections ci-dessous, qui proposent des liens vers des informations supplémentaires et des instructions plus détaillées.

### Fonctionnalités et éléments de l’interface utilisateur que vous utiliserez {#ui-functionality-and-elements}

Lorsque vous aurez terminé les étapes de mise en oeuvre du cas d’utilisation, vous utiliserez la fonctionnalité Real-Time CDP, Adobe Journey Optimizer et les éléments d’IU répertoriés au début de ce document. Assurez-vous de disposer des autorisations de contrôle d’accès en fonction des attributs nécessaires pour toutes ces zones ou demandez à votre administrateur système de vous octroyer les autorisations nécessaires.

### Création d’une conception de schéma et spécification de groupes de champs {#schema-design}

Les ressources du modèle de données d’expérience (XDM) sont gérées dans le [!UICONTROL Schémas] espace de travail dans [!DNL Adobe Experience Platform]. Vous pouvez afficher et explorer les ressources de base fournies par [!DNL Adobe] (par exemple, [!UICONTROL groupes de champs]) et créez des ressources et des schémas personnalisés pour votre organisation.

Pour plus d’informations sur la création [schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr), lisez le [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md)

Il existe plusieurs conceptions de schéma que vous pouvez utiliser dans cet exemple d’implémentation pour que le cas d’utilisation évolue vers la valeur de durée de vie. Chaque schéma comprend des champs obligatoires spécifiques à configurer et certains champs suggérés.

Sur la base d’exemples de mise en oeuvre, Adobe vous suggère de créer les trois schémas suivants pour réaliser ce cas d’utilisation :

* [Schéma des attributs du client](#customer-attributes-schema) (un schéma de profil)
* [Schéma des transactions numériques client](#customer-digital-transactions-schema) (un schéma d’événement d’expérience)
* [Schéma des transactions hors ligne client](#customer-offline-transactions-schema) (un schéma d’événement d’expérience)

#### Schéma des attributs du client {#customer-attributes-schema}

Utilisez ce schéma pour structurer et référencer les données de profil qui constituent les informations sur vos clients. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via votre système CRM ou similaire. Il est nécessaire de référencer les détails du client utilisés pour la personnalisation, le consentement marketing et des fonctionnalités de segmentation améliorées.

![Schéma des attributs du client avec mise en surbrillance des groupes de champs](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

Le schéma des attributs du client est représenté par une [!UICONTROL XDM Individual Profile] , qui inclut les groupes de champs suivants :

+++Détails démographiques (groupe de champs)

[Détails démographiques](/help/xdm/field-groups/profile/demographic-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile. Le groupe de champs fournit un objet person de niveau racine, dont les sous-champs décrivent les informations sur une personne.

+++

+++Détails du contact personnel (groupe de champs)

[Détails du contact personnel](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile, qui décrit les informations de contact pour une personne individuelle.

+++

+++Détails de l’audit du système source externe (groupe de champs)

[Attributs d’audit du système de source externe](/help/xdm/data-types/external-source-system-audit-attributes.md) est un type de données XDM (Experience Data Model) standard qui capture les détails de l’audit sur un système source externe.

+++

+++Groupes de champs de consentement et de préférence (groupe de champs)

[Consentements et préférences](/help/xdm/field-groups/profile/consents.md) Le groupe de champs fournit un champ de type objet unique, les consentements, pour capturer les informations de consentement et de préférence.

+++

#### Schéma des transactions numériques client {#customer-digital-transactions-schema}

Ce schéma est utilisé pour structurer et référencer les données d’événement qui constituent l’activité de votre client sur votre site web ou sur d’autres plateformes numériques associées. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via [SDK Web](/help/web-sdk/home.md) et est nécessaire pour référencer les différents événements de navigation et de conversion utilisés pour le déclenchement des parcours, l’analyse client détaillée en ligne et les fonctionnalités de segmentation améliorées.

![Schéma des transactions numériques client avec groupes de champs mis en surbrillance](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

Le schéma des transactions numériques client est représenté par une [!UICONTROL XDM ExperienceEvent] , qui inclut les groupes de champs suivants :

+++Adobe Experience Platform Web SDK ExperienceEvent (groupe de champs)

| Champs | Exigence |
| --- | --- |
| `device.model` | Suggérée |
| `environment.browserDetails.userAgent` | Suggérée |

+++

+++Détails web (groupe de champs)

[Détails web](/help/xdm/field-groups/event/web-details.md) est un groupe de champs de schéma standard pour la classe XDM ExperienceEvent, utilisé pour décrire les informations concernant les événements de détails web tels que l’interaction, les détails de page et le référent.

+++

+++Événement d’expérience client (groupe de champs)

Ce groupe de champs contient diverses informations sur les actions, telles que les événements d’achat ou de navigation, effectuées par les utilisateurs sur votre propriété web.

| Champ | Exigence |
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

La variable [Détails de l’identifiant utilisateur final](/help/xdm/field-groups/event/enduserids.md) Ce groupe de champs contient différentes informations sur vos utilisateurs, telles que leur authentification sur votre site lors de leur visite, ainsi que des informations sur leur identité.

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

#### Schéma des transactions hors ligne client {#customer-offline-transactions-schema}

Ce schéma est utilisé pour structurer et référencer les données d’événement qui constituent l’activité de votre client sur les plateformes en dehors de votre site web. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] d’un point de contact (ou d’un système similaire) et le plus souvent diffusé en continu dans Platform via une connexion API. En savoir plus [ingestion par lots](/help/ingestion/batch-ingestion/getting-started.md). Son objectif est de référencer les différents événements de conversion hors ligne utilisés pour le déclenchement des parcours, une analyse client en ligne et hors ligne approfondie et des fonctionnalités de segmentation améliorées.

![Schéma des transactions hors ligne client avec groupes de champs surlignés](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

Le schéma des transactions hors ligne du client est représenté par une [!UICONTROL XDM ExperienceEvent] , qui inclut les groupes de champs suivants :

+++Détails Commerce (groupe de champs)

[Détails du Commerce](/help/xdm/field-groups/event/commerce-details.md) est un groupe de champs de schéma standard pour la variable [!DNL XDM ExperienceEvent] , utilisée pour décrire les données commerciales telles que les informations sur les produits (SKU, nom, quantité) et les opérations standard sur les paniers (commande, passage en caisse, abandon).

+++

+++Détails du contact personnel (groupe de champs)

[[!UICONTROL Détails du contact personnel]](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la variable [!DNL XDM Individual Profile] qui décrit les coordonnées d’une personne.

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

#### Schéma du connecteur web Adobe {#adobe-web-connector-schema}

>[!NOTE]
>
>Il s’agit d’une implémentation facultative si vous utilisez le [!DNL Adobe Analytics Data Connector].

Ce schéma est utilisé pour structurer et référencer les données d’événement qui constituent l’activité de votre client sur votre site web ou sur d’autres plateformes numériques associées. Ce schéma est similaire au schéma des transactions numériques client, mais il est différent dans la mesure où il peut être utilisé lorsque le SDK Web n’est pas une option de collecte de données. Par conséquent, vous pouvez utiliser ce schéma lorsque vous utilisez le [!DNL Adobe Analytics Data Connector] pour envoyer vos données en ligne dans [!DNL Adobe Experience Platform] en tant que flux de données principal ou secondaire.

![Schéma du connecteur web Adobe avec les groupes de champs mis en évidence](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

La variable [!DNL Adobe] le schéma du connecteur web est représenté par une [!UICONTROL XDM ExperienceEvent] , qui inclut les groupes de champs suivants :

+++Modèle ExperienceEvent Adobe Analytics (groupe de champs)

[[!UICONTROL Extension complète Adobe Analytics ExperienceEvent]](/help/xdm/field-groups/event/analytics-full-extension.md) est un groupe de champs de schéma standard qui capture les mesures courantes collectées par Adobe Analytics.

+++

### Création d’un jeu de données à partir d’un schéma {#dataset-from-schema}

Un jeu de données est une structure de stockage et de gestion pour un groupe de données. Chaque schéma utilisé pour réaliser cet exemple d’implémentation comporte un jeu de données unique.

Pour plus d’informations sur la création d’un [dataset](/help/catalog/datasets/overview.md) à partir d’un schéma, lisez la [Guide de l’interface utilisateur des jeux de données](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Tout comme l’étape de création d’un schéma, vous devez activer l’inclusion du jeu de données dans le profil client en temps réel. Pour plus d’informations sur l’activation du jeu de données à utiliser dans Real-Time Customer Profile, consultez la section [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Confidentialité, consentement et gouvernance des données {#privacy-consent}

#### Politiques de consentement

>[!IMPORTANT]
>
>Disposer aux clients de la possibilité de se désabonner de la réception des communications d’une marque et veiller au respect de ce choix est une obligation légale. En savoir plus sur la législation applicable dans la section [Présentation des réglementations sur la confidentialité](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Envisagez de mettre en oeuvre les [stratégies de consentement](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) et demander le consentement de vos visiteurs avant de les contacter :

* If `consents.marketing.email.val = "Y"` alors peut envoyer un courrier électronique
* If `consents.marketing.sms.val = "Y"` alors peut envoyer des SMS
* If `consents.marketing.push.val = "Y"` Push
* If `consents.share.val = "Y"` puis peuvent faire la publicité

#### Libellé de gouvernance des données et application

Envisagez d’ajouter et d’appliquer les éléments suivants : [étiquettes de gouvernance des données](/help/data-governance/labels/overview.md):

* Les adresses électroniques personnelles sont utilisées comme données d’identification directe utilisées pour identifier ou contacter une personne spécifique plutôt qu’un appareil.
   * `personalEmail.address = I1`

#### Stratégies marketing

Il n’y a pas de [stratégies marketing](/help/data-governance/policies/overview.md) requis pour les parcours que vous créez dans le cadre de ce cas pratique. Cependant, vous pouvez tenir compte des stratégies suivantes selon vos besoins :

* Limitation des données sensibles
* Limitation de la publicité Onsite
* Limitation du ciblage des emails
* Limitation du ciblage intersite
* Restreindre la combinaison de données directement identifiables avec des données anonymes

### Créer des audiences {#create-audiences}

Ce cas d’utilisation nécessite la création de deux audiences pour définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de personnes pouvant faire l’objet d’un marketing. Les audiences peuvent être créées de plusieurs façons dans Adobe Experience Platform :

* Pour plus d’informations sur la création d’une audience, lisez le [Guide de l’interface utilisateur d’Audience Service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).
* Pour plus d’informations sur la composition [audiences](/help/segmentation/home.md), lisez le [Guide de l’interface utilisateur de composition d’audience](/help/segmentation/ui/audience-composition.md).
* Pour plus d’informations sur la création d’audiences par le biais de définitions de segment dérivées de Platform, lisez la section [Guide de l’interface utilisateur d’Audience Builder](/help/segmentation/ui/segment-builder.md).

Plus précisément, vous devez créer et utiliser deux audiences à différentes étapes du cas d’utilisation, comme illustré dans l’image ci-dessous.

![Audiences surlignées.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Audience Adobe Journey Optimizer admissible]

Cette audience haute valeur et basse fréquence comprend les profils auxquels vous souhaitez accéder via un parcours, afin de leur faire part d&#39;un nouveau programme d&#39;abonnement. Les détails de l’audience sont les suivants :

* Description : Profils ayant dépensé plus de 250 $ dans l’ensemble au cours des 3 derniers mois
* Champs et conditions nécessaires dans l’audience :
   * Événement : `commerce.order.payments.paymentamount`
* Somme agrégée : >= 250 $
   * EventType : `commerce.purchases`
* Horodatage : moins de 3 mois avant maintenant


>[!TAB Audience de médias payants]

Cette audience est créée pour inclure les profils qui ont dépensé plus de 250 euros dans l’ensemble au cours des trois derniers mois et qui n’ont pas effectué d’achat au cours des 7 derniers jours. Les détails de l’audience sont les suivants :

* Description : profils ayant dépensé plus de 250 $ dans l’ensemble au cours des 3 derniers mois et n’ayant pas effectué d’achat au cours des 7 derniers jours.
* Champs et conditions nécessaires :
   * EventType : `journey.feedback`
      * Operand : = true
   * Événement : `experience.journeyOrchestration.stepEvents.nodeName`
      * Operand : = JourneyStepEventTracker - Abonnement non acheté
      * Horodatage : au cours des 7 derniers jours
   * EventType n’est pas : `commerce.purchases`
      * Horodatage : &lt;= 7 jours avant maintenant
   * Événement : SKU
      * Valeur : = `subscription`

>[!ENDTABS]

### Configuration des parcours dans Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] n’englobe pas tout ce qui est affiché dans les diagrammes. Tous [publicités médias payantes](/help/destinations/catalog/social/overview.md) sont créées dans la variable [!UICONTROL destinations] [workspace](/help/destinations/ui/destinations-workspace.md).

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) vous aide à offrir à vos clients des expériences connectées, contextuelles et personnalisées. Le parcours client correspond à l’ensemble du processus des interactions d’un client avec la marque. Chaque parcours de cas d’utilisation nécessite des informations spécifiques.

Pour réaliser ce cas pratique, vous devez créer deux parcours distincts :

* Parcours de durée de vie, qui inclut le message que vous envoyez à vos clients à forte valeur ajoutée et à faible fréquence
* Le parcours de confirmation de commande pour les utilisateurs qui répondent à votre appel et qui achètent un abonnement.

![Parcours surlignés.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

Vous trouverez ci-dessous les données précises nécessaires à chaque branche de Parcours.

>[!BEGINTABS]

>[!TAB Parcours de durée de vie]

Le parcours de durée de vie s’adresse à l’audience des clients à forte valeur et à faible fréquence qui n’ont pas été ciblés au cours des 30 derniers jours. Un message s’affiche à ces clients et, si au bout de 7 jours ils n’effectuent toujours pas d’achat, vous pouvez inclure les non-acheteurs dans une audience à laquelle vous pouvez afficher des publicités multimédia payantes. S&#39;ils effectuent un achat, vous pouvez définir les acheteurs sur un parcours de confirmation de commande, détaillé dans l&#39;onglet distinct.

![Présentation visuelle de haut niveau du parcours de vie.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "Valeur unique à durée de vie parcours un aperçu visuel de haut niveau."){zoomable="yes"}

+++Logique de Parcours détaillée

Le parcours illustré ci-dessus suit la logique suivante.

1. Lecture d’audience : utilisez une [lecture de l’activité d’audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=en) pour la première audience créée dans la section audiences ci-dessus.

2. Condition - Canal préféré : utilisez un [activité de condition](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html) pour déterminer comment atteindre les clients, que ce soit par courrier électronique, SMS ou notifications push. Utilisez trois activités d’action pour créer les trois branches.

3. Attente : utilisez une [activité d’attente](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html) d’attendre que vous écoutiez les achats.

4. Condition - Abonnement acheté au cours des 7 derniers jours ? : utilisez une activité de condition pour écouter les achats de produits au cours des sept derniers jours.

5. JourneyStepEventTracker - Abonnement non acheté : utilisez un [action personnalisée](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html) pour les visiteurs qui n’ont pas encore acheté votre abonnement, même s’ils ont reçu votre message. Dans le cadre de la condition personnalisée à la fin du parcours, créez une `journey.feedback` et l’ajouter à un jeu de données en fonction de la variable [!UICONTROL Événement d’étape de parcours] schéma. Vous utiliserez cet événement pour segmenter l’audience qui n’a pas acheté l’abonnement et que vous pouvez cibler par le biais de publicités multimédia payantes.

+++

>[!TAB Parcours de confirmation de commande]

Le parcours de confirmation de commande se concentre sur la question de savoir si un achat a été effectué via le site web ou l’application mobile. Une fois qu’un client a acheté, par exemple, un abonnement auprès de votre société, vous pouvez le définir sur un parcours de confirmation de commande.

![Présentation visuelle de haut niveau du parcours de confirmation de commande du client.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "Présentation visuelle de haut niveau du parcours de confirmation de commande du client."){zoomable="yes"}

Logique du Parcours +++

Utilisez les événements, champs et actions suggérés ci-dessous dans votre parcours de confirmation :

* Le parcours est déclenché par un événement d’achat en ligne.
   * Schéma : transactions numériques client
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

+++Logique du Parcours clé

* Logique d’entrée de parcours
   * Événement de commande

* Conditions
   * Sélectionnez Canal cible (vous pouvez sélectionner un ou plusieurs canaux pour une portée plus large).
      * La confirmation de commande est considérée comme étant de nature à servir. La vérification du consentement est donc généralement inutile.
      * E-mail
      * Notification push
      * SMS

   * Personnalisation du contenu du canal
      * Affichez les informations sur les commandes et affichez une liste de produits au format tabulaire.

+++

>[!ENDTABS]

Pour plus d’informations sur la création de parcours dans [!DNL Adobe Journey Optimizer], lisez le [Prise en main de parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) guide.

### Configuration d’une destination pour l’affichage de publicités multimédia payantes {#paid-media-ads}

Certains utilisateurs n’ont peut-être pas acheté votre abonnement, même après leur avoir envoyé un message à propos du nouveau programme. Après avoir attendu un certain nombre de jours (sept dans cet exemple d’utilisation), vous pouvez décider d’afficher des publicités multimédia payantes à ces utilisateurs, afin de les encourager à acheter votre abonnement.

Utilisez la structure de destinations dans Real-Time CDP pour les publicités multimédia payantes. Sélectionnez l’une des nombreuses destinations publicitaires disponibles pour afficher des publicités multimédia payantes à vos clients et activer l’audience de médias payants que vous [créé précédemment](#create-audiences) vers une destination de votre choix. Consultez un aperçu des [publicité](/help/destinations/catalog/advertising/overview.md) et [social](/help/destinations/catalog/social/overview.md) destinations.

Pour savoir comment activer des données vers des destinations (par exemple [Le bureau de commerce](/help/destinations/catalog/advertising/tradedesk.md) ou [Correspondance client Google](/help/destinations/catalog/advertising/google-customer-match.md)), lisez la documentation ci-dessous :

* [Créer une connexion à une destination](/help/destinations/ui/connect-destination.md)
* [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md)

## Étapes suivantes {#next-steps}

En définissant vos utilisateurs à faible fréquence et à forte valeur ajoutée sur un parcours et en affichant des publicités multimédia payantes sur un sous-ensemble d’entre eux, vous avez, je l’espère, fait de certains d’entre eux une valeur unique à des clients à valeur ajoutée tout au long de leur vie, améliorant ainsi vos mesures de fidélité à la marque et d’engagement des clients.

Vous pouvez ensuite explorer d’autres cas pratiques pris en charge par Real-Time CDP, tels que [réengager intelligemment les clients](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) ou [affichage de contenu personnalisé pour les utilisateurs non authentifiés](/help/rtcdp/partner-data/onsite-personalization.md) sur vos propriétés web.
