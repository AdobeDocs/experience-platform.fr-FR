---
title: Réengagement intelligent
description: Proposez des expériences attrayantes et connectées au cours des moments de conversion clés pour réengager intelligemment la clientèle moins fréquente.
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: d47ddc474fcaf19eaff8ddcd67139dec5c417720
workflow-type: tm+mt
source-wordcount: '3594'
ht-degree: 6%

---

# Réengager intelligemment vos clientes et clients pour qu’ils reviennent

>[!NOTE]
>
>Il s’agit d’un exemple de mise en oeuvre. Les exemples de cette page, tels que la syntaxe de segment, ne sont que des exemples. Utilisez les exemples comme guide, car votre mise en oeuvre peut différer.

Réengager les clients qui ont abandonné une conversion de manière intelligente et responsable. Contactez les clients obsolètes avec des expériences afin d’augmenter la conversion et d’augmenter la valeur de durée de vie du client.

Utilisez des considérations en temps réel, prenez en compte toutes les qualités et comportements des consommateurs et proposez une réqualification rapide basée sur des événements en ligne et hors ligne.

![Présentation visuelle de haut niveau du réengagement intelligent.](../intelligent-re-engagement/images/step-by-step.png)

## Présentation du cas d’utilisation {#overview}

Vous allez créer des schémas, des jeux de données et des audiences à mesure que vous examinez les exemples de scénarios de réengagement. Vous découvrirez également les fonctionnalités nécessaires à la configuration d’exemples de parcours dans [!DNL Adobe Journey Optimizer] et ceux nécessaires pour créer des publicités médiatiques payantes dans les destinations. Ce guide utilise des exemples de réengagement des clients dans les parcours de cas d’utilisation décrits ci-dessous :

* **Scénario de navigation des produits abandonné** - Ciblez les clients qui ont abandonné la navigation sur le site web et dans l’application mobile.
* **Scénario de panier abandonné** - Ciblez les clients qui ont placé des produits dans le panier mais qui n’ont pas encore été achetés sur le site web et l’application mobile.
* **Scénario de confirmation de commande** - Concentrez-vous sur les achats de produits effectués par le biais du site web et de l’application mobile.

## Prérequis et planification {#prerequisites-and-planning}

Lorsque vous terminez les étapes de mise en oeuvre du cas d’utilisation, vous utiliserez les fonctionnalités Real-Time CDP et Adobe Journey Optimizer suivantes (répertoriées dans l’ordre dans lequel vous les utiliserez). Assurez-vous que vous disposez des [autorisations de contrôle d’accès basées sur des attributs](/help/access-control/home.md) pour toutes ces zones ou demandez à votre administrateur ou administratrice système de vous accorder les autorisations nécessaires.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) : intègre des données à l’échelle des sources de données pour alimenter la campagne. Ces données sont ensuite utilisées pour créer les audiences de campagne et faire apparaître les éléments de données personnalisés utilisés dans l&#39;email et les mosaïques de promotion web (par exemple, le nom ou les informations liées au compte). La plateforme de données clients (CDP) est également utilisée pour activer les audiences par courrier électronique et sur le web (via [!DNL Adobe Target]).
   * [Schémas](/help/xdm/home.md)
   * [Profils](/help/profile/home.md)
   * [Jeux de données](/help/catalog/datasets/overview.md)
   * [Audiences](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr)
   * [Destinations](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=fr) - Vous aide à offrir à vos clients des expériences connectées, contextuelles et personnalisées.
   * [Déclencheur d’événement ou d’audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Audiences/Événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=fr)
   * [Actions de parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr)

## Comment réaliser le cas d’utilisation {#achieve-use-case-instruction}

Vous trouverez ci-dessous un aperçu général des trois exemples de scénarios de réengagement.

>[!BEGINTABS]

>[!TAB Scénario de navigation des produits abandonné]

Le scénario de navigation du produit abandonné cible la navigation du produit abandonné sur le site web et dans l’application mobile. Ce scénario est déclenché lorsqu’un produit a été consulté, mais n’a pas été acheté ni ajouté au panier. Dans cet exemple, l’engagement de la marque est déclenché au bout de trois jours s’il n’y a pas d’ajouts de liste au cours des dernières 24 heures.<p>![Présentation visuelle de haut niveau du scénario de navigation des produits abandonnés par l’intelligence client.](../intelligent-re-engagement/images/re-engagement-journey.png "Présentation visuelle de haut niveau du scénario de navigation des produits abandonnés par l’intelligence client."){width="1920" zoomable="yes"}</p>

1. Vous créez des schémas et des jeux de données, puis vous activez pour [!UICONTROL Profil].
2. Vous ingérez des données dans Experience Platform via le SDK Web, le SDK Mobile ou l’API. Le connecteur de données Analytics peut également être utilisé, mais peut entraîner une latence de parcours.
3. Vous ingérez des données de profil supplémentaires, qui peuvent être liées aux visiteurs de l’application web et/ou mobile authentifiés par le biais de graphiques d’identités.
4. Vous créez des audiences ciblées à partir de la liste des profils pour vérifier si un **client** a fait un engagement au cours des trois derniers jours.
5. Vous créez un parcours de navigation de produit abandonné dans [!DNL Adobe Journey Optimizer].
6. Si nécessaire, travaillez avec la fonction **partenaire de données** pour activer les audiences vers les destinations de médias payants souhaitées.
7. [!DNL Adobe Journey Optimizer] recherche le consentement et envoie les différentes actions configurées.

>[!TAB Scénario de panier abandonné]

Le scénario de panier abandonné s’applique lorsque des produits ont été placés dans le panier mais n’ont pas encore été achetés sur le site web et sur l’application mobile. En outre, les campagnes de médias payants sont lancées et arrêtées à l’aide de cette méthode.<p>![Présentation visuelle de haut niveau du scénario Panier abandonné par le client.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Présentation visuelle de haut niveau du scénario Panier abandonné par le client."){width="1920" zoomable="yes"}</p>

1. Vous créez des schémas et des jeux de données, l’option activer pour [!UICONTROL Profil].
2. Vous ingérez des données dans Experience Platform via le SDK Web, le SDK Mobile ou l’API. Le connecteur de données Analytics peut également être utilisé, mais peut entraîner une latence de parcours.
3. Vous ingérez des données de profil supplémentaires, qui peuvent être liées aux visiteurs de l’application web et/ou mobile authentifiés par le biais de graphiques d’identités.
4. Vous créez des audiences ciblées à partir de la liste des profils pour vérifier si un **client** a placé un élément dans son panier mais n’a pas terminé l’achat. La variable **[!UICONTROL Ajouter au panier]** démarre un minuteur qui attend pendant 30 minutes, puis vérifie l’achat. Si aucun achat n’a été effectué, la variable **client** est ajouté à la variable **[!UICONTROL Abandonner le panier]** audiences.
5. Vous créez un parcours de panier abandonné dans [!DNL Adobe Journey Optimizer].
6. Si nécessaire, travaillez avec la fonction **partenaire de données** pour activer les audiences vers les destinations de médias payants souhaitées.
7. [!DNL Adobe Journey Optimizer] recherche le consentement et envoie les différentes actions configurées.

>[!TAB Scénario de confirmation de commande]

Le scénario de confirmation de commande se concentre sur les achats de produits effectués par le biais du site web et de l’application mobile.<p>![Présentation visuelle de haut niveau du scénario de confirmation de commande du client.](../intelligent-re-engagement/images/order-confirmation-journey.png "Présentation visuelle de haut niveau du scénario de confirmation de commande du client."){width="1920" zoomable="yes"}</p>

1. Vous créez des schémas et des jeux de données, puis vous activez pour [!UICONTROL Profil].
2. Vous ingérez des données dans Experience Platform via le SDK Web, le SDK Mobile ou l’API. Le connecteur de données Analytics peut également être utilisé, mais peut entraîner une latence de parcours.
3. Vous ingérez des données de profil supplémentaires, qui peuvent être liées aux visiteurs de l’application web et/ou mobile authentifiés par le biais de graphiques d’identités.
4. Vous créez un parcours de confirmation dans [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] envoie un message de confirmation de commande à l’aide du canal préféré.

>[!ENDTABS]

Pour terminer chacune des étapes des présentations de haut niveau ci-dessus, consultez les sections ci-dessous, qui proposent des liens vers des informations supplémentaires et des instructions plus détaillées.

### Créer des schémas et spécifier des groupes de champs {#schema-design}

Les ressources du modèle de données d’expérience (XDM) sont gérées dans le [!UICONTROL Schémas] espace de travail dans [!DNL Adobe Experience Platform]. Vous pouvez afficher et explorer les ressources de base fournies par [!DNL Adobe] (par exemple, les groupes de champs) et créez des ressources et des schémas personnalisés pour votre organisation.

Pour plus d’informations sur la création [schémas](/help/xdm/home.md), voir [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md) et [Modèle de vos données d’expérience client avec XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html).

Quatre conceptions de schéma sont utilisées pour le cas d’utilisation du réengagement. Chaque schéma nécessite la configuration de champs spécifiques. Vous devez activer l’inclusion du schéma dans le profil client en temps réel. Pour plus d’informations sur l’activation du schéma à utiliser dans Real-Time Customer Profile, consultez [Activation d’un schéma pour Real-time Customer Profile](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### Schéma des attributs du client

Ce schéma est utilisé pour structurer et référencer les données de profil qui constituent les informations sur vos clients. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via votre système CRM ou similaire. Il est nécessaire de référencer les détails du client utilisés pour la personnalisation, le consentement marketing et des fonctionnalités d’audience améliorées.

Le schéma des attributs du client est représenté par une [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md) , qui inclut les groupes de champs suivants :

+++Détails du contact personnel (groupe de champs)

[Détails du contact personnel](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile qui décrit les coordonnées d’une personne.

| Champs | Exigence | Description |
| --- | --- | --- |
| `mobilePhone.number` | Obligatoire | Numéro de téléphone portable de la personne, qui sera utilisé pour les SMS. |
| `personalEmail.address` | Obligatoire | Adresse électronique de la personne. |

+++

+++Détails de l’audit du système source externe (groupe de champs)

[Attributs d’audit du système de source externe](/help/xdm/data-types/external-source-system-audit-attributes.md) est un type de données XDM (Experience Data Model) standard qui capture les détails de l’audit sur un système source externe.

+++

+++Groupes de champs de consentement et de préférence (groupe de champs)

La variable [Consentements et préférences](/help/xdm/field-groups//profile/consents.md) Le groupe de champs fournit un champ de type objet unique, les consentements, pour capturer les informations de consentement et de préférence.

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

Ce schéma est utilisé pour structurer et référencer les données d’événement qui constituent l’activité de votre client sur votre site web et/ou les plateformes numériques associées. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via [SDK Web](/help/edge/home.md) et est nécessaire pour référencer les différents événements de navigation et de conversion utilisés pour le déclenchement des parcours, l’analyse client détaillée en ligne et les fonctionnalités d’audience améliorées.

Le schéma des transactions numériques client est représenté par une [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) classe .

+++XDM ExperienceEvent (Classe)

| Champs | Exigence | Description |
| --- | --- | --- |
| `_id` | Obligatoire | Identifie de manière unique les événements individuels ingérés dans [!DNL Adobe Experience Platform]. |
| `timestamp` | Obligatoire | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme RFC 3339 Section 5.6. Cet horodatage doit avoir lieu dans le passé. |
| `eventType` | Obligatoire | Chaîne indiquant le type de catégorie de l’événement. |

+++

La variable [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) inclut les groupes de champs suivants :

+++Détails de l’ID utilisateur final (groupe de champs)

La variable [Détails de l’identifiant utilisateur final](/help/xdm/field-groups/event/enduserids.md) Le groupe de champs sert à décrire les informations d’identité d’une personne dans plusieurs applications Adobe.

| Champs | Exigence | Description |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Obligatoire | ID d’adresse électronique de l’utilisateur final état authentifié. |
| `endUserIDs._experience.emailid.id` | Obligatoire | ID de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.emailid.namespace.code` | Obligatoire | Code d’espace de noms de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoire | [!DNL Adobe] État d’authentification de l’ID de Marketing Cloud (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoire | [!DNL Adobe] ID de Marketing Cloud (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoire | [!DNL Adobe] Code d’espace de noms de l’identifiant de Marketing Cloud (MCID). |

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

#### Schéma des transactions hors ligne client

Ce schéma est utilisé pour structurer et référencer les données d’événement qui constituent l’activité de votre client sur les plateformes en dehors de votre site web. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] d’un point de contact (ou d’un système similaire) et le plus souvent diffusé en continu dans Platform via une connexion API. Son objectif est de référencer les différents événements de conversion hors ligne utilisés pour le déclenchement des parcours, une analyse client en ligne et hors ligne approfondie et des fonctionnalités d’audience améliorées.

Le schéma des transactions hors ligne du client est représenté par une [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) classe .

+++XDM ExperienceEvent (Classe)

| Champs | Exigence | Description |
| --- | --- | --- |
| `_id` | Obligatoire | Identifie de manière unique les événements individuels ingérés dans [!DNL Adobe Experience Platform]. |
| `timestamp` | Obligatoire | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme RFC 3339 Section 5.6. Cet horodatage doit avoir lieu dans le passé. |
| `eventType` | Obligatoire | Chaîne indiquant le type de catégorie de l’événement. |

+++

La variable [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) inclut les groupes de champs suivants :

+++Détails du commerce (groupe de champs)

La variable [Détails du commerce](/help/xdm/field-groups/event/commerce-details.md) Le groupe de champs est utilisé pour décrire les données commerciales telles que les informations sur les produits (SKU, nom, quantité) et les opérations standard sur les paniers (commande, passage en caisse, abandon).

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

[Détails du contact personnel](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile qui décrit les coordonnées d’une personne.

| Champs | Exigence | Description |
| --- | --- | --- |
| `mobilePhone.number` | Obligatoire | Numéro de téléphone portable de la personne, qui sera utilisé pour les SMS. |
| `personalEmail.address` | Obligatoire | Adresse électronique de la personne. |

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

#### Schéma du connecteur web Adobe

>[!NOTE]
>
>Il s’agit d’une implémentation facultative si vous utilisez le [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md).

Ce schéma est utilisé pour structurer et référencer les données d’événement qui constituent l’activité de votre client sur votre site web et/ou les plateformes numériques associées. Ce schéma est similaire au schéma des transactions numériques client, mais il est différent dans la mesure où il est destiné à être utilisé lors de la [SDK Web](/help/edge/home.md) n’est pas une option de collecte de données ; ce schéma est donc nécessaire lorsque vous utilisez la méthode [!DNL Adobe Analytics Source Connector] pour envoyer vos données en ligne dans [!DNL Adobe Experience Platform] en tant que flux de données principal ou secondaire.

La variable [!DNL Adobe] le schéma du connecteur web est représenté par une [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) classe .

+++XDM ExperienceEvent (Classe)

| Champs | Exigence | Description |
| --- | --- | --- |
| `_id` | Obligatoire | Identifie de manière unique les événements individuels ingérés dans [!DNL Adobe Experience Platform]. |
| `timestamp` | Obligatoire | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme RFC 3339 Section 5.6. Cet horodatage doit avoir lieu dans le passé. |
| `eventType` | Obligatoire | Chaîne indiquant le type de catégorie de l’événement. |

+++

La variable [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) inclut les groupes de champs suivants :

+++Modèle ExperienceEvent Adobe Analytics (groupe de champs)

La variable [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) groupe de champs capture les mesures courantes collectées par Adobe Analytics.

| Champs | Exigence | Description |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Obligatoire | ID d’adresse électronique de l’utilisateur final état authentifié. |
| `endUserIDs._experience.emailid.id` | Obligatoire | ID de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.emailid.namespace.code` | Obligatoire | Code d’espace de noms de l’adresse électronique de l’utilisateur final. |
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoire | [!DNL Adobe] État d’authentification de l’ID de Marketing Cloud (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoire | [!DNL Adobe] ID de Marketing Cloud (MCID). Le MCID est désormais connu sous le nom d’ID Experience Cloud (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoire | [!DNL Adobe] Code d’espace de noms de l’identifiant de Marketing Cloud (MCID). |

+++

+++Détails de l’audit du système source externe (groupe de champs)

Les attributs d’audit du système de source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système de source externe.

+++

### Création d’un jeu de données à partir d’un schéma {#create-datasets}

Un jeu de données est une structure de stockage et de gestion pour un groupe de données. Chaque schéma pour les scénarios de réengagement intelligent doit avoir son propre jeu de données.

Pour plus d’informations sur la création d’un [dataset](/help/catalog/datasets/overview.md) à partir d’un schéma, lisez la [Guide de l’interface utilisateur des jeux de données](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Tout comme l’étape de création d’un schéma, vous devez activer l’inclusion du jeu de données dans le profil client en temps réel. Pour plus d’informations sur l’activation du jeu de données à utiliser dans Real-Time Customer Profile, consultez le tutoriel sur [introduction de données dans Real-time Customer Profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=fr).

### Consentement et gouvernance des données {#privacy-consent}

>[!IMPORTANT]
>
>Disposer aux clients de la possibilité de se désabonner de la réception des communications d’une marque et veiller au respect de ce choix est une obligation légale. En savoir plus sur la législation applicable dans la section [Présentation des réglementations sur la confidentialité](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

#### Stratégies de consentement

Lors de la création d’un chemin de réengagement, pensez à ajouter les éléments suivants : [stratégies de consentement](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html):

* If `consents.marketing.email.val = "Y"` alors peut envoyer un courrier électronique
* If `consents.marketing.sms.val = "Y"` alors peut envoyer des SMS
* If `consents.marketing.push.val = "Y"` Push
* If `consents.share.val = "Y"` puis peuvent faire la publicité

#### Étiquetage et application de la gouvernance des données

Lors de la création d’un chemin de réengagement, pensez à ajouter les éléments suivants : [Étiquettes de gouvernance des données](/help/data-governance/labels/overview.md):

* Les adresses électroniques personnelles sont utilisées comme données d’identification directe utilisées pour identifier ou contacter une personne spécifique plutôt qu’un appareil.
   * `personalEmail.address = I1`

#### Politiques d’utilisation des données

Il n’y a pas de [stratégies d’utilisation des données](/help/data-governance/policies/overview.md) requis pour le scénario de navigation du produit abandonné. Toutefois, tenez compte des points suivants :

* Limitation des données sensibles
* Limitation de la publicité Onsite
* Limitation du ciblage des emails
* Limitation du ciblage intersite
* Restreindre la combinaison de données directement identifiables avec des données anonymes

### Créer des audiences {#create-audience}

Les scénarios de réengagement utilisent des audiences pour définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de clients potentiels de votre base. Les audiences peuvent être créées de plusieurs façons dans [!DNL Adobe Experience Platform].

Pour plus d’informations sur la création d’une audience, lisez le [Guide de l’interface utilisateur d’Audience Service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Pour plus d’informations sur la composition directe [Audiences](/help/segmentation/home.md), lisez le [Guide de l’interface utilisateur de composition d’audience](/help/segmentation/ui/audience-composition.md).

Pour plus d’informations sur la création d’audiences par le biais de définitions d’audiences dérivées de Platform, consultez la rubrique [Guide de l’interface utilisateur d’Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Scénario de navigation des produits abandonné]

Cette audience est créée afin d’améliorer le scénario classique &quot;Abandon de panier&quot;. Alors que l’abandon de panier se concentre généralement sur un ajout de panier sans achat ultérieur pendant une certaine période, cette audience recherche un engagement précédent, en particulier ceux qui ont pu parcourir un produit particulier mais ne l’ont pas ajouté au panier et n’ont eu aucune activité de suivi sur votre site au cours d’une certaine période. Cette audience permet de garder votre marque à l’esprit pour les clients qui répondent à ces critères d’inclusion et peut également être utilisée pour les clients dont les propriétés numériques peuvent différer d’un modèle de commerce électronique traditionnel.

+++Abandon de la consultation du produit sans engagement au cours des trois derniers jours

L’événement suivant est utilisé pour le scénario de navigation des produits abandonnés où les utilisateurs ont consulté les produits en ligne et n’ont pas interagi (visites sur le site, visites dans les applications, achat en ligne, achat hors ligne et ajout à des événements de panier) dans les 3 jours suivants.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.productViews`
* Et `THEN` (événement séquentiel) exclude `eventType: commerce.procuctListAdds` ou `application.launch` ou `web.webpagedetails.pageViews` ou `commerce.purchases` (y compris en ligne et hors ligne)
   * `Timestamp: > 3 days after productView`

+++

+++Consultation produit avec engagement au cours des trois derniers jours

L’événement suivant est utilisé pour le scénario de navigation des produits abandonnés où les utilisateurs ont consulté les produits en ligne et se sont engagés (visites du site, visites de l’application, achat en ligne, achat hors ligne et ajout aux événements du panier) dans les 3 jours suivants.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.productViews`
* Et `THEN` (événement séquentiel) inclut `eventType: commerce.procuctListAdds` ou `application.launch` ou `web.webpagedetails.pageViews` ou `commerce.purchases` (y compris en ligne et hors ligne)
   * `Timestamp: > 3 days after productView`

+++Diffusion en continu de l’engagement au cours du dernier jour

L’événement suivant est utilisé pour le scénario de navigation des produits abandonnés où les utilisateurs se sont engagés (visites du site, visites d’applications, achat en ligne, achat hors ligne et ajout à des événements de panier) au cours du dernier jour.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 1 day` (Diffusion en continu)

+++

+++Lot d’engagement dans les trois derniers jours

L’événement suivant est utilisé pour le scénario de navigation des produits abandonnés où les utilisateurs se sont engagés (visites du site, visites d’applications, achat en ligne, achat hors ligne et ajout à des événements de panier) au cours des 3 derniers jours.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `EventType: commerce.procuctListAdds or application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: in last 3 days` (Lot)

+++

>[!TAB Scénario de panier abandonné]

Cette audience est créée pour prendre en charge le scénario classique &quot;Abandon de panier&quot;. Son objectif est de trouver les clients qui ont ajouté un produit à leur panier, mais qui n’ont finalement pas effectué d’achat. Cette audience vous aidera à garder non seulement votre marque en tête de vos clients, mais aussi les produits qu’ils ont laissés sans achat ultérieur.

Les événements suivants sont utilisés pour le scénario de panier abandonné où les utilisateurs ont ajouté un produit à leur panier il y a entre 1 et 4 jours, mais n’ont pas effectué l’achat ou vidé leur panier.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

Le descripteur du scénario de panier abandonné apparaît comme suit :

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Scénario de confirmation de commande]

Ce parcours ne nécessite aucune audience à créer.

>[!ENDTABS]

### Configuration des parcours dans Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] n’englobe pas tout ce qui est affiché dans les diagrammes. Tous [publicités médias payantes](/help/destinations/catalog/social/overview.md) sont créées dans [!UICONTROL Destinations].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr) vous aide à offrir à vos clients des expériences connectées, contextuelles et personnalisées. Le parcours client correspond à l’ensemble du processus des interactions d’un client avec la marque. Chaque parcours de cas d’utilisation nécessite des informations spécifiques. Vous trouverez ci-dessous les données précises nécessaires à chaque parcours.

>[!BEGINTABS]

>[!TAB Scénario de navigation des produits abandonné]

Le scénario de navigation du produit abandonné cible la navigation du produit abandonné sur le site web et dans l’application mobile.<p>![Présentation visuelle de haut niveau du scénario de navigation du produit abandonnée par le client.](../intelligent-re-engagement/images/re-engagement-journey.png "Présentation visuelle de haut niveau du scénario de navigation du produit abandonnée par le client."){width="1920" zoomable="yes"}</p>

+++Événements

* Événement 1 : Consultations de produit
   * Schéma : transactions numériques client
   * Champs:
      * `eventType`
   * Condition:
      * `eventType = commerce.productViews`
      * Champs:
         * `commerce.productViews.id`
         * `commerce.productViews.value`
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

* Événement 2 : ajout au panier
   * Schéma : transactions numériques client
   * Champs:
      * `eventType`
   * Condition:
      * `eventType = commerce.productListAdds`
      * Champs:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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

* Événement 3 : Engagement de marque
   * Schéma : transactions numériques client
   * Champs:
      * `eventType`
   * Condition:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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
      * Schéma : transactions hors ligne client
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

>[!TAB Scénario de panier abandonné]

Le scénario de panier abandonné cible les produits qui ont été placés dans le panier mais qui n’ont pas encore été achetés sur le site web et sur l’application mobile.<p>![Présentation visuelle de haut niveau du scénario Panier abandonné par le client.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Présentation visuelle de haut niveau du scénario Panier abandonné par le client."){width="1920" zoomable="yes"}</p>

+++Événements

* Événement 2 : ajout au panier
   * Schéma : transactions numériques client
   * Champs:
      * `eventType`
   * Condition:
      * `eventType = commerce.productListAdds`
      * Champs:
         * `commerce.productListAdds.id`
         * `commerce.productListAdds.value`
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

* Événement 4 : Achats en ligne
   * Schéma : transactions numériques client
   * Champs:
      * `eventType`
   * Condition:
      * `eventType = commerce.purchases`
      * Champs:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

* Événement 3 : Engagement de marque
   * Schéma : transactions numériques client
   * Champs:
      * `eventType`
   * Condition:
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
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
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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
   * Schéma : transactions hors ligne client
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Condition : le panier est effacé depuis la dernière abandon du panier :
   * Schéma : transactions numériques client
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

>[!TAB Scénario de confirmation de commande]

Le scénario de confirmation de commande se concentre sur les achats de produits effectués par le biais du site web et de l’application mobile.<p>![Présentation visuelle de haut niveau du scénario de confirmation de commande du client.](../intelligent-re-engagement/images/order-confirmation-journey.png "Présentation visuelle de haut niveau du scénario de confirmation de commande du client."){width="1920" zoomable="yes"}</p>

+++Événements

* Événement 4 : Achats en ligne
   * Schéma : transactions numériques client
   * Champs:
      * `eventType`
   * Condition:
      * `eventType = commerce.purchases`
      * Champs:
         * `commerce.purchases.id`
         * `commerce.purchases.value`
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

Pour plus d’informations sur la création de parcours dans [!DNL Adobe Journey Optimizer], lisez le [Guide de prise en main de parcours](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr).

### Configuration des publicités multimédia payantes dans les destinations {#paid-media-ads}

La structure des destinations est utilisée pour les publicités multimédia payantes. Une fois le consentement vérifié, il est envoyé vers les différentes destinations configurées. Pour plus d’informations sur les destinations, consultez la [Présentation des destinations](/help/destinations/home.md) document.

#### Données requises pour les destinations

Les destinations d’exportation d’audiences en flux continu (telles que Facebook, Google Customer Match, Google DV360) prennent en charge diverses identités à partir des données client :

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

l’audience du panier d’abandon est évaluée en tant qu’audience en continu et peut donc être utilisée par la structure des destinations pour ce cas d’utilisation.

* Diffusion/Déclenché
   * [Publicité](/help/destinations/catalog/advertising/overview.md)/[Médias payants et réseaux sociaux](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destination de diffusion en continu](/help/destinations/catalog/streaming/http-destination.md)
   * [Destination personnalisée créée à l’aide de Destination SDK.](/help/destinations/destination-sdk/overview.md). Si vous êtes un client Real-Time CDP Ultimate, vous pouvez également créer un [destination personnalisée à l’aide de Destination SDK](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)
