---
title: Réengagement intelligent
description: Proposez des expériences attrayantes et connectées au cours des moments de conversion clés pour réengager intelligemment la clientèle irrégulière.
feature: Use Cases
exl-id: 13f6dbc9-7471-40bf-824d-27922be0d879
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3896'
ht-degree: 4%

---

# Réengager intelligemment le retour de vos clientes et clients

>[!NOTE]
>
>Il s’agit d’un exemple d’implémentation. Les exemples de cette page, tels que la syntaxe du segment, ne sont que des exemples. Vous devez utiliser ces exemples comme guide, car votre implémentation peut différer.

Réengagez les clients qui ont abandonné une conversion de manière intelligente et responsable. Faites participer les clients obsolètes avec des expériences pour augmenter la conversion et la valeur de durée de vie du client.

Tenez compte des considérations en temps réel, prenez en compte toutes les qualités et tous les comportements des consommateurs et offrez une requalification rapide en fonction des événements en ligne et hors ligne.

Vous trouverez ci-dessous une vue d’ensemble de l’architecture des différents composants de Real-Time CDP et Journey Optimizer. Ce diagramme montre le flux de données entre les deux applications Experience Platform, de la collecte de données jusqu’au point d’activation par le biais de parcours ou de campagnes vers les destinations, afin d’atteindre le cas d’utilisation décrit sur cette page.

![Présentation visuelle de haut niveau du réengagement intelligent.](../intelligent-re-engagement/images/step-by-step.png)

## Présentation du cas d’utilisation {#overview}

Vous allez créer des schémas, des jeux de données et des audiences à mesure que vous examinerez des exemples de scénarios de réengagement. Vous découvrirez également les fonctionnalités nécessaires à la configuration des exemples de parcours dans [!DNL Adobe Journey Optimizer] et celles nécessaires à la création de publicités multimédias payantes dans les destinations. Ce guide utilise des exemples de réengagement des clients dans les parcours de cas d’utilisation décrits ci-dessous :

* **Scénario de navigation de produit abandonné** - Ciblez les clients qui ont abandonné la navigation sur le site web et l’application mobile.
* **Scénario de panier abandonné** - Ciblez les clients et clientes qui ont placé des produits dans le panier, mais qui n’ont pas encore été achetés sur le site web et l’application mobile.
* **Scénario de confirmation de commande** - Concentrez-vous sur les achats de produits effectués par le biais du site web et de l’application mobile.

## Prérequis et planification {#prerequisites-and-planning}

Au fur et à mesure que vous exécuterez les étapes de mise en œuvre du cas d’utilisation, vous utiliserez les fonctionnalités Real-Time CDP et Adobe Journey Optimizer suivantes (répertoriées dans l’ordre dans lequel vous les utiliserez). Assurez-vous que vous disposez des [autorisations de contrôle d’accès basées sur des attributs](/help/access-control/home.md) pour toutes ces zones ou demandez à votre administrateur ou administratrice système de vous accorder les autorisations nécessaires.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=fr) : intègre des données entre les sources de données pour alimenter la campagne. Ces données sont ensuite utilisées pour créer les audiences de la campagne et les éléments de données personnalisés de la surface utilisés dans l’e-mail et les vignettes de promotion web (par exemple, les informations relatives au nom ou au compte). Le CDP est également utilisé pour activer les audiences dans les e-mails et sur le web (via [!DNL Adobe Target]).
   * [Schémas](/help/xdm/home.md)
   * [Profils](/help/profile/home.md)
   * [Jeux de données](/help/catalog/datasets/overview.md)
   * [Audiences](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr)
   * [Destinations](/help/destinations/home.md)

* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/introduction-to-journey-optimizer/introduction.html?lang=fr) - Vous permet de proposer des expériences connectées, contextuelles et personnalisées à vos clients.
   * [Déclencheur d’événement ou d’audience](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html?lang=fr)
   * [Audiences/Événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=fr)
   * [Actions de Parcours ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr)

## Comment réaliser le cas d’utilisation {#achieve-use-case-instruction}

Vous trouverez ci-dessous un aperçu général des trois exemples de scénarios de réengagement.

>[!BEGINTABS]

>[!TAB Scénario de navigation de produit abandonné]

Le scénario de navigation de produits abandonnés cible la navigation de produits abandonnés sur le site web et l’application mobile. Ce scénario est déclenché lorsqu’un produit a été consulté, mais n’a pas été acheté ou ajouté au panier. Dans cet exemple, l’engagement de la marque est déclenché après trois jours s’il n’y a aucun ajout à la liste au cours des dernières 24 heures.<p>![Présentation visuelle générale du scénario de navigation de produit abandonné intelligent du client.](../intelligent-re-engagement/images/re-engagement-journey.png "Présentation visuelle de haut niveau du scénario de navigation de produit abandonné intelligent du client."){width="1920" zoomable="yes"}</p>

1. Créez des schémas et des jeux de données, puis activez pour [!UICONTROL Profil].
2. Vous ingérez des données dans Experience Platform par le biais de Web SDK, de Mobile SDK ou d’une API. Le connecteur Source d’Analytics peut également être utilisé, mais peut entraîner une latence du parcours.
3. Vous ingérez des données supplémentaires activées pour le profil, qui peuvent être liées au visiteur d’applications web et mobiles authentifié via des graphiques d’identités.
4. Vous créez des audiences ciblées à partir de la liste des profils pour vérifier si un **client** a effectué un engagement au cours des trois derniers jours.
5. Vous créez un parcours de navigation de produit abandonné dans [!DNL Adobe Journey Optimizer].
6. Si nécessaire, collaborez avec le **partenaire de données** pour l’activation des audiences vers les destinations de médias achetés souhaitées.
7. [!DNL Adobe Journey Optimizer] vérifie le consentement et envoie les différentes actions configurées.

>[!TAB Scénario de panier abandonné]

Le scénario de panier abandonné s’applique lorsque des produits ont été placés dans le panier, mais n’ont pas encore été achetés sur le site web et l’application mobile. En outre, les campagnes de médias payants sont démarrées et arrêtées à l’aide de cette méthode.<p>![Présentation visuelle de haut niveau du scénario de panier abandonné par le client.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Présentation visuelle de haut niveau du scénario de panier abandonné par le client."){width="1920" zoomable="yes"}</p>

1. Vous créez des schémas et des jeux de données, puis activez pour [!UICONTROL Profil].
2. Vous ingérez des données dans Experience Platform par le biais de Web SDK, de Mobile SDK ou d’une API. Le connecteur Source d’Analytics peut également être utilisé, mais peut entraîner une latence du parcours.
3. Vous ingérez des données supplémentaires activées pour le profil, qui peuvent être liées au visiteur d’applications web et mobiles authentifié via des graphiques d’identités.
4. Vous créez des audiences ciblées à partir de la liste des profils pour vérifier si un **client** a placé un article dans son panier mais n’a pas effectué l’achat. L’événement **[!UICONTROL Ajouter au panier]** déclenche un minuteur qui attend pendant 30 minutes, puis vérifie l’achat. Si aucun achat n’a été effectué, le **client** est ajouté aux audiences **[!UICONTROL Abandonner le panier]**.
5. Vous créez un parcours de panier abandonné dans [!DNL Adobe Journey Optimizer].
6. Si nécessaire, collaborez avec le **partenaire de données** pour l’activation des audiences vers les destinations de médias achetés souhaitées.
7. [!DNL Adobe Journey Optimizer] vérifie le consentement et envoie les différentes actions configurées.

>[!TAB Scénario de confirmation de commande]

Le scénario de confirmation de commande se concentre sur les achats de produits effectués par le biais du site web et de l’application mobile.<p>![Présentation visuelle générale du scénario de confirmation de commande client.](../intelligent-re-engagement/images/order-confirmation-journey.png "Présentation visuelle générale du scénario de confirmation de commande client."){width="1920" zoomable="yes"}</p>

1. Créez des schémas et des jeux de données, puis activez pour [!UICONTROL Profil].
2. Vous ingérez des données dans Experience Platform par le biais de Web SDK, de Mobile SDK ou d’une API. Le connecteur Source d’Analytics peut également être utilisé, mais peut entraîner une latence du parcours.
3. Vous ingérez des données supplémentaires activées pour le profil, qui peuvent être liées au visiteur d’applications web et mobiles authentifié via des graphiques d’identités.
4. Vous créez un parcours de confirmation dans [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] envoie un message de confirmation de commande par le biais du canal préféré.

>[!ENDTABS]

Pour réaliser chacune des étapes des présentations de haut niveau ci-dessus, lisez les sections ci-dessous qui contiennent des liens vers des informations supplémentaires et des instructions plus détaillées.

### Création de schémas et spécification de groupes de champs {#schema-design}

Les ressources du modèle de données d’expérience (XDM) sont gérées dans l’espace de travail [!UICONTROL Schémas] de [!DNL Adobe Experience Platform]. Vous pouvez afficher et explorer les ressources de base fournies par [!DNL Adobe] (par exemple, les groupes de champs) et créer des ressources et des schémas personnalisés pour votre organisation.

Pour plus d’informations sur la création de [schémas](/help/xdm/home.md), consultez le tutoriel [créer un schéma .](/help/xdm/tutorials/create-schema-ui.md) et [modéliser vos données d’expérience client avec XDM](https://experienceleague.adobe.com/docs/courses/using/experienceplatform-d-1-2021-1-xdm.html?lang=fr).

Quatre conceptions de schéma sont utilisées dans le cas d’utilisation de réengagement. Chaque schéma nécessite la configuration de champs spécifiques. Vous devez activer l’inclusion du schéma dans le profil client en temps réel. Pour plus d’informations sur l’activation du schéma à utiliser dans le profil client en temps réel, lisez [activer un schéma pour le profil client en temps réel](/help/xdm/ui/resources/schemas.md#enable-a-schema-for-real-time-customer-profile).

#### Schéma des attributs du client

Ce schéma est utilisé pour structurer et référencer les données de profil qui constituent vos informations client. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via votre CRM ou un système similaire et sont nécessaires pour référencer les détails des clients utilisés pour la personnalisation, le consentement marketing et les fonctionnalités améliorées d’audience.

Le schéma des attributs du client est représenté par une classe [[!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md) qui comprend les groupes de champs suivants :

+++Coordonnées personnelles (groupe de champs)

[Coordonnées personnelles](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile qui décrit les informations de contact d’une personne individuelle.

| Champs | Description |
| --- | --- |
| `mobilePhone.number` | Numéro de téléphone mobile de la personne, qui sera utilisé pour les SMS. |
| `personalEmail.address` | Adresse e-mail de la personne. |

+++

+++Détails de l’audit du système Source externe (groupe de champs)

[Attributs d’audit du système Source externe](/help/xdm/data-types/external-source-system-audit-attributes.md) est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails d’audit d’un système source externe.

+++

+++Groupes de champs de consentement et de préférence (groupe de champs)

Le groupe de champs [Consentements et préférences](/help/xdm/field-groups//profile/consents.md) fournit un seul champ de type objet, consentements, pour capturer les informations de consentement et de préférence.

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

Ce groupe de champs vous permet de tester votre parcours avant sa publication à l’aide de profils de test. Pour plus d’informations sur la création de profils de test, consultez les tutoriels [créer des profils de test](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles.html?lang=fr) et [tester le parcours ](https://experienceleague.adobe.com/docs/journeys/using/building-journeys/testing-the-journey.html?lang=fr).

+++

#### Schéma des transactions numériques client

Ce schéma est utilisé pour structurer et référencer les données d’événement qui composent l’activité de votre client qui se produit sur votre site web ou les plateformes numériques associées. Ces données sont généralement ingérées dans [!DNL Adobe Experience Platform] via [Web SDK](/help/web-sdk/home.md) et sont nécessaires pour référencer les différents événements de navigation et de conversion utilisés pour le déclenchement de parcours, l’analyse détaillée des clients en ligne, les fonctionnalités améliorées d’audience et la messagerie personnalisée.

Le schéma des transactions numériques client est représenté par une classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++XDM ExperienceEvent (classe)

La classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) comprend les groupes de champs suivants :

| Champs | Description |
| --- | --- |
| `_id` | Identifie de manière unique les événements individuels qui sont ingérés dans [!DNL Adobe Experience Platform]. |
| `timestamp` | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme RFC 3339 (section 5.6). Cet horodatage doit se produire dans le passé. |
| `eventType` | Chaîne indiquant le type de catégorie de l’événement. |

+++

+++Détails de l’ID de l’utilisateur final (groupe de champs)

Le groupe de champs [Détails de l’ID de l’utilisateur final](/help/xdm/field-groups/event/enduserids.md) est utilisé pour décrire les informations d’identité d’un individu dans plusieurs applications Adobe.

| Champs | Description |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | État d’authentification de l’adresse e-mail de l’utilisateur final. |
| `endUserIDs._experience.emailid.id` | ID d’adresse e-mail de l’utilisateur final. |
| `endUserIDs._experience.emailid.namespace.code` | Code d’espace de noms d’identifiant d’adresse e-mail de l’utilisateur final. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] état d’authentification de l’ID Marketing Cloud (MCID). Le MCID est désormais appelé Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud ID (MCID). Le MCID est désormais appelé Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] code d’espace de noms de l’identifiant Marketing Cloud ID (MCID). |

+++

Détails du Commerce (groupe de champs)

Le groupe de champs [Détails Commerce](/help/xdm/field-groups/event/commerce-details.md) est utilisé pour décrire des données commerciales telles que des informations sur le produit (SKU, nom, quantité) et des opérations standard du panier (commande, passage en caisse, abandon).

| Champs | Description |
| --- | --- |
| `commerce.cart.cartID` | Identifiant du panier. |
| `commerce.order.orderType` | Objet décrivant le type de commande de produit. |
| `commerce.order.payments.paymentAmount` | Objet décrivant le montant du paiement de la commande de produit. |
| `commerce.order.payments.paymentType` | Objet décrivant le type de paiement de la commande de produit. |
| `commerce.order.payments.transactionID` | ID de transaction de commande de produit objet. |
| `commerce.order.purchaseID` | Identifiant d&#39;achat de commande de produit d&#39;objet. |
| `productListItems.name` | Liste de noms d’éléments représentant le ou les produits sélectionnés par un client. |
| `productListItems.priceTotal` | Prix total de la liste d’articles représentant le ou les produits sélectionnés par un client. |
| `productListItems.product` | Le ou les produits sélectionnés. |
| `productListItems.quantity` | Quantité de la liste d’articles représentant le ou les produits sélectionnés par un client. |

+++

+++Détails de l’audit du système Source externe (groupe de champs)

Attributs d’audit du système Source externe est un type de données standard des modèles de données d’expérience (XDM) qui capture les détails d’audit d’un système source externe.

+++

#### Schéma des transactions client hors ligne

Ce schéma est utilisé pour structurer et référencer les données d’événement qui composent l’activité de votre client ou cliente qui se produit sur des plateformes en dehors de votre site web. Ces données sont généralement ingérées dans des [!DNL Adobe Experience Platform] à partir d’un point de vente (ou d’un système similaire) et le plus souvent diffusées en continu dans Experience Platform via une connexion API. Son objectif est de référencer les différents événements de conversion hors ligne utilisés pour le déclenchement de parcours, l’analyse approfondie des clients en ligne et hors ligne, les fonctionnalités améliorées d’audience et la messagerie personnalisée.

Le schéma des transactions hors ligne du client est représenté par une classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++XDM ExperienceEvent (classe)

La classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) comprend les groupes de champs suivants :

| Champs | Description |
| --- | --- |
| `_id` | Identifie de manière unique les événements individuels qui sont ingérés dans [!DNL Adobe Experience Platform]. |
| `timestamp` | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme RFC 3339 (section 5.6). Cet horodatage doit se produire dans le passé. |
| `eventType` | Chaîne indiquant le type de catégorie de l’événement. |

+++

Détails du Commerce (groupe de champs)

Le groupe de champs [Détails Commerce](/help/xdm/field-groups/event/commerce-details.md) est utilisé pour décrire des données commerciales telles que des informations sur le produit (SKU, nom, quantité) et des opérations standard du panier (commande, passage en caisse, abandon).

| Champs | Description |
| --- | --- |
| `commerce.cart.cartID` | Identifiant du panier. |
| `commerce.order.orderType` | Objet décrivant le type de commande de produit. |
| `commerce.order.payments.paymentAmount` | Objet décrivant le montant du paiement de la commande de produit. |
| `commerce.order.payments.paymentType` | Objet décrivant le type de paiement de la commande de produit. |
| `commerce.order.payments.transactionID` | ID de transaction de commande de produit objet. |
| `commerce.order.purchaseID` | Identifiant d&#39;achat de commande de produit d&#39;objet. |
| `productListItems.name` | Liste de noms d’éléments représentant le ou les produits sélectionnés par un client. |
| `productListItems.priceTotal` | Prix total de la liste d’articles représentant le ou les produits sélectionnés par un client. |
| `productListItems.product` | Le ou les produits sélectionnés. |
| `productListItems.quantity` | Quantité de la liste d’articles représentant le ou les produits sélectionnés par un client. |

+++

+++Coordonnées personnelles (groupe de champs)

[Coordonnées personnelles](/help/xdm/field-groups/profile/personal-contact-details.md) est un groupe de champs de schéma standard pour la classe XDM Individual Profile qui décrit les informations de contact d’une personne individuelle.

| Champs | Description |
| --- | --- |
| `mobilePhone.number` | Numéro de téléphone mobile de la personne, qui sera utilisé pour les SMS. |
| `personalEmail.address` | Adresse e-mail de la personne. |

+++

+++Détails de l’audit du système Source externe (groupe de champs)

Attributs d’audit du système Source externe est un type de données standard des modèles de données d’expérience (XDM) qui capture les détails d’audit d’un système source externe.

+++

#### Schéma du connecteur web Adobe

>[!NOTE]
>
>Il s’agit d’une implémentation facultative si vous utilisez le [[!DNL Adobe Analytics Source Connector]](/help/sources/connectors/adobe-applications/analytics.md) .

Ce schéma est utilisé pour structurer et référencer les données d’événement qui composent l’activité de votre client qui se produit sur votre site web ou les plateformes numériques associées. Ce schéma est similaire au schéma Transactions numériques client, mais il diffère en ce qu’il est destiné à être utilisé lorsque [Web SDK](/help/web-sdk/home.md) n’est pas une option de collecte de données. Par conséquent, ce schéma est nécessaire lorsque vous utilisez le [!DNL Adobe Analytics Source Connector] pour envoyer vos données en ligne dans [!DNL Adobe Experience Platform] en tant que flux de données principal ou secondaire.

Le schéma de connecteur web [!DNL Adobe] est représenté par une classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md).

+++XDM ExperienceEvent (classe)

La classe [[!UICONTROL XDM ExperienceEvent]](/help/xdm/classes/experienceevent.md) comprend les groupes de champs suivants :

| Champs | Description |
| --- | --- |
| `_id` | Identifie de manière unique les événements individuels qui sont ingérés dans [!DNL Adobe Experience Platform]. |
| `timestamp` | Horodatage ISO 8601 du moment où l’événement s’est produit, formaté selon la norme RFC 3339 (section 5.6). Cet horodatage doit se produire dans le passé. |
| `eventType` | Chaîne indiquant le type de catégorie de l’événement. |

+++

Modèle ExperienceEvent Adobe Analytics (groupe de champs)

Le groupe de champs [Adobe Analytics ExperienceEvent](/help/xdm/field-groups/event/analytics-full-extension.md) capture les mesures courantes collectées par Adobe Analytics.

| Champs | Description |
| --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | État d’authentification de l’adresse e-mail de l’utilisateur final. |
| `endUserIDs._experience.emailid.id` | ID d’adresse e-mail de l’utilisateur final. |
| `endUserIDs._experience.emailid.namespace.code` | Code d’espace de noms d’identifiant d’adresse e-mail de l’utilisateur final. |
| `endUserIDs._experience.mcid.authenticatedState` | [!DNL Adobe] état d’authentification de l’ID Marketing Cloud (MCID). Le MCID est désormais appelé Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.id` | [!DNL Adobe] Marketing Cloud ID (MCID). Le MCID est désormais appelé Experience Cloud ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | [!DNL Adobe] code d’espace de noms de l’identifiant Marketing Cloud ID (MCID). |

+++

+++Détails de l’audit du système Source externe (groupe de champs)

Attributs d’audit du système Source externe est un type de données standard des modèles de données d’expérience (XDM) qui capture les détails d’audit d’un système source externe.

+++

### Création d’un jeu de données à partir d’un schéma {#create-datasets}

Un jeu de données est une structure de stockage et de gestion pour un groupe de données. Chaque schéma pour les scénarios de réengagement intelligents doit avoir son propre jeu de données.

Pour plus d’informations sur la création d’un [jeu de données](/help/catalog/datasets/overview.md) à partir d’un schéma, consultez le [guide de l’interface utilisateur des jeux de données](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>Comme pour l’étape de création d’un schéma, vous devez activer l’inclusion du jeu de données dans le profil client en temps réel. Pour plus d’informations sur l’activation du jeu de données en vue de son utilisation dans le profil client en temps réel, consultez le tutoriel sur [l’importation de données dans le profil client en temps réel](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=fr).

### Consentement et gouvernance des données {#privacy-consent}

>[!IMPORTANT]
>
>La possibilité pour les clients de se désabonner de la réception des communications d’une marque, ainsi que le respect de ce choix, sont des exigences légales. Pour en savoir plus sur la législation applicable, consultez la [présentation des réglementations relatives à la confidentialité](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html?lang=fr).

#### Politiques de consentement

Lors de la création d’un chemin de réengagement, pensez à ajouter les [politiques de consentement](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html?lang=fr) suivantes :

* Si `consents.marketing.email.val = "Y"`, peut envoyer un e-mail à
* Si `consents.marketing.sms.val = "Y"`, peut envoyer des SMS.
* Si `consents.marketing.push.val = "Y"`, peut envoyer une notification push.
* Si `consents.share.val = "Y"`, peut publier

#### Étiquetage et application de la gouvernance des données

Lors de la création d’un chemin de réengagement, pensez à ajouter les étiquettes [gouvernance des données](/help/data-governance/labels/overview.md) suivantes :

* Les adresses e-mail personnelles sont utilisées comme données d’identification directe utilisées pour identifier ou contacter une personne spécifique plutôt qu’un appareil.
   * `personalEmail.address = I1`

#### Politiques d’utilisation des données

Aucune [politique d’utilisation des données](/help/data-governance/policies/overview.md) n’est requise pour le scénario de navigation de produit abandonné. Toutefois, tenez compte des points suivants :

* Limitation Des Données Sensibles
* Restreindre l’Advertising sur site
* Restreindre le ciblage par e-mail
* Limiter le ciblage intersite
* Limiter la combinaison de données directement identifiables avec des données anonymes

### Créer des audiences {#create-audience}

Les scénarios de réengagement utilisent les audiences pour définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de clients potentiels de votre base de clients. Les audiences peuvent être créées de plusieurs manières dans [!DNL Adobe Experience Platform].

Pour plus d’informations sur la création d’une audience, consultez le [guide de l’interface utilisateur du service d’audience](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=fr#create-audience).

Pour plus d’informations sur la composition directe d’[audiences](/help/segmentation/home.md), consultez le [guide de l’interface utilisateur sur la composition d’audiences](/help/segmentation/ui/audience-composition.md).

Pour plus d’informations sur la création d’audiences par le biais de définitions d’audience dérivées d’Experience Platform, consultez le [ guide de l’interface utilisateur du créateur d’audience](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Scénario de navigation de produit abandonné]

Cette audience est créée en tant qu’amélioration du scénario classique « Abandon de panier ». Alors que l’abandon de panier se concentre généralement sur un ajout au panier sans achat ultérieur pendant une certaine période de temps, cette audience recherche un engagement antérieur, en particulier ceux qui ont peut-être parcouru un produit particulier mais ne l’ont pas ajouté à leur panier et n’ont pas eu d’activité de suivi sur votre site au cours d’une certaine période. Cette audience permet de garder votre marque « à l’esprit » pour les clients qui répondent à ces critères d’inclusion et peut également être utilisée pour les clients dont les propriétés numériques peuvent différer d’un modèle d’e-commerce traditionnel.

+++consultation de produit abandonnée sans engagement au cours des trois derniers jours

L’événement suivant est utilisé pour le scénario de navigation de produit abandonné dans lequel les utilisateurs ont consulté des produits en ligne et ne les ont pas engagés (visites de site, visites d’applications, achat en ligne, achat hors ligne et événements d’ajout au panier) dans les 3 jours suivants.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.productViews`
* Et `THEN` (événement séquentiel) excluent `eventType: commerce.productListAdds` ET `application.launch` ET `web.webpagedetails.pageViews` ET `commerce.purchases` (cela inclut en ligne et hors ligne)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`

+++

+++Consultation du produit avec engagement au cours des trois derniers jours

L’événement suivant est utilisé pour le scénario de navigation de produit abandonné dans lequel les utilisateurs ont consulté des produits en ligne et ont participé (visites de site, visites d’applications, achat en ligne, achat hors ligne et événements d’ajout au panier) dans les 3 jours suivants.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.productViews`
* Les `THEN` (événements séquentiels) incluent `eventType: commerce.productListAdds` OU `application.launch` OU `web.webpagedetails.pageViews` OU `commerce.purchases` (cela inclut en ligne et hors ligne)
   * `Timestamp: > 3 days after productView`
* `Timestamp: > 4 days`
+++

+++Diffusion en continu de l’engagement au cours de la dernière journée

L’événement suivant est utilisé pour le scénario de navigation de produit abandonné dans lequel les utilisateurs ont effectué (visites de site, visites d’application, achat en ligne, achat hors ligne et événements d’ajout au panier) au cours de la dernière journée.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 1 day` (streaming)

+++

+++Lot d’engagements au cours des trois derniers jours

L’événement suivant est utilisé pour le scénario de navigation de produit abandonné dans lequel les utilisateurs ont effectué (visites de site, visites d’application, achat en ligne, achat hors ligne et événements d’ajout au panier) au cours des 3 derniers jours.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `EventType: commerce.productListAdds OR application.launch OR web.webpagedetails.pageViews OR commerce.purchases`
   * `Timestamp: in last 3 days` (lot)

+++

>[!TAB Scénario de panier abandonné]

Cette audience est créée pour prendre en charge le scénario classique « Abandon de panier ». Son objectif est de trouver les clients qui ont ajouté un produit à leur panier, mais qui n’ont pas effectué d’achat. Cette audience vous aidera à garder votre marque « à l&#39;esprit » pour vos clients, mais aussi pour les produits qu&#39;ils ont laissés derrière eux sans achat ultérieur.

Les événements suivants sont utilisés pour le scénario de panier abandonné dans lequel les utilisateurs ont ajouté un produit à leur panier il y a entre 1 et 4 jours, mais n’ont pas effectué l’achat ou effacé leur panier.

Les champs et conditions suivants sont requis lors de la configuration de cette audience :

* `eventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now AND <= 4 days before now `
* `eventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `eventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

Le descripteur du scénario de panier abandonné s’affiche comme suit :

`Include eventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude eventType = commerce.purchases 30 minutes before now OR eventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Scénario de confirmation de commande]

Ce parcours ne nécessite la création d’aucune audience.

>[!ENDTABS]

### Configuration du parcours dans Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] n’englobe pas tout ce qui est indiqué dans les diagrammes. Toutes les [annonces médias payantes](/help/destinations/catalog/social/overview.md) sont créées dans [!UICONTROL Destinations].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr) vous permet de proposer des expériences connectées, contextuelles et personnalisées à vos clients. Le parcours client est l’ensemble du processus d’interaction d’un client avec la marque. Chaque parcours de cas d’utilisation nécessite des informations spécifiques. Vous trouverez ci-dessous les données précises nécessaires pour chaque parcours.

>[!BEGINTABS]

>[!TAB Scénario de navigation de produit abandonné]

Le scénario de navigation de produits abandonnés cible la navigation de produits abandonnés sur le site web et l’application mobile.<p>![Présentation visuelle générale du scénario de navigation de produit abandonné par le client.](../intelligent-re-engagement/images/re-engagement-journey.png "Présentation visuelle générale du scénario de navigation de produit abandonné par le client."){width="1920" zoomable="yes"}</p>

+++Événements

Les événements vous permettent de déclencher vos parcours de manière unitaire pour envoyer des messages, en temps réel, à l’individu progressant dans le parcours. Pour plus d’informations sur les événements, consultez le [guide général des événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=fr).

* Événement 1 : Consultations de produits
   * Schéma : Transactions numériques client
   * Champs :
      * `eventType`
   * Condition :
      * `eventType = commerce.productViews`
      * Champs :
         * `eventType`
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

* Événement 2 : Ajouter au panier
   * Schéma : Transactions numériques client
   * Champs :
      * `eventType`
   * Condition :
      * `eventType = commerce.productListAdds`
      * Champs :
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

* Événement 3 : Engagement de la marque
   * Schéma : Transactions numériques client
   * Champs :
      * `eventType`
   * Condition :
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Champs :
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

Logique de clé de la zone de travail de Parcours

La logique de clé de la zone de travail de parcours nécessite que vous identifiiez des événements spécifiques et configuriez les actions à effectuer une fois que l’événement se produit.

* Logique d&#39;entrée de parcours
   * Événement de vue du produit

* Conditions
   * Recherchez au moins un événement d’achat en ligne ou hors ligne depuis la dernière consultation du produit.
      * Schéma : Transactions numériques client
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Recherchez au moins un achat hors ligne depuis la dernière consultation du produit :
      * Schéma : Transactions hors ligne du client
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Conditions - Sélection du canal cible
      * E-mail
         * `consents.marketing.email.val = y`
      * Notification push
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Personalization du canal
      * Contenu de canal personnalisé basé sur la consultation du produit.

+++

>[!TAB Scénario de panier abandonné]

Le scénario de panier abandonné cible les produits qui ont été placés dans le panier, mais qui n’ont pas encore été achetés sur le site web et l’application mobile.<p>![Présentation visuelle de haut niveau du scénario de panier abandonné par le client.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Présentation visuelle de haut niveau du scénario de panier abandonné par le client."){width="1920" zoomable="yes"}</p>

+++Événements

Les événements vous permettent de déclencher vos parcours de manière unitaire pour envoyer des messages, en temps réel, à l’individu progressant dans le parcours. Pour plus d’informations sur les événements, consultez le [guide général des événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=fr).

* Événement 2 : Ajouter au panier
   * Schéma : Transactions numériques client
   * Champs :
      * `eventType`
   * Condition :
      * `eventType = commerce.productListAdds`
      * Champs :
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
   * Schéma : Transactions numériques client
   * Champs :
      * `eventType`
   * Condition :
      * `eventType = commerce.purchases`
      * Champs :
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

* Événement 3 : Engagement de la marque
   * Schéma : Transactions numériques client
   * Champs :
      * `eventType`
   * Condition :
      * `eventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Champs :
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

Logique de clé de la zone de travail de Parcours

La logique de clé de la zone de travail de parcours nécessite que vous identifiiez des événements spécifiques et configuriez les actions à effectuer une fois que l’événement se produit.

* Logique d&#39;entrée de parcours
   * Événement `AddToCart`

* AuthenticatedState dans l’authentifié

* Condition : achats hors ligne depuis le dernier abandon du panier :
   * Schéma : Transactions hors ligne du client
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Condition : panier effacé depuis le dernier abandon du panier :
   * Schéma : Transactions numériques client
   * `eventType = commerce.cartCleared`
   * `cartID` (ID du panier)
   * `timestamp > timestamp of cart was last abandoned`

* Sélectionner le canal cible (sélectionner un ou plusieurs canaux pour élargir la portée)
   * E-mail
      * `consents.marketing.email.val = y`
   * Notification push
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Personalization du canal
      * Affichez les informations détaillées du panier et pouvez afficher plusieurs produits sous la forme d’un tableau.

+++

>[!TAB Scénario de confirmation de commande]

Le scénario de confirmation de commande se concentre sur les achats de produits effectués par le biais du site web et de l’application mobile.<p>![Présentation visuelle générale du scénario de confirmation de commande client.](../intelligent-re-engagement/images/order-confirmation-journey.png "Présentation visuelle générale du scénario de confirmation de commande client."){width="1920" zoomable="yes"}</p>

+++Événements

Les événements vous permettent de déclencher vos parcours de manière unitaire pour envoyer des messages, en temps réel, à l’individu progressant dans le parcours. Pour plus d’informations sur les événements, consultez le [guide général des événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events.html?lang=fr).

* Événement 4 : Achats en ligne
   * Schéma : Transactions numériques client
   * Champs :
      * `eventType`
   * Condition :
      * `eventType = commerce.purchases`
      * Champs :
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

Logique de clé de la zone de travail de Parcours

La logique de clé de la zone de travail de parcours nécessite que vous identifiiez des événements spécifiques et configuriez les actions à effectuer une fois que l’événement se produit.

* Logique d&#39;entrée de parcours
   * Événement de commande

* Conditions
   * Sélectionnez Canal cible (sélectionnez un ou plusieurs canaux pour une portée plus large).
      * La confirmation de commande étant considérée comme une diffusion par nature, la vérification du consentement est généralement inutile.
      * E-mail
      * Notification push
      * SMS

   * Personalization de contenu de canal
      * Affichez les informations détaillées sur la commande et pouvez afficher une liste de produits au format tableau.

+++

>[!ENDTABS]

Pour plus d’informations sur la création de parcours dans [!DNL Adobe Journey Optimizer], consultez le guide [Prise en main des parcours ](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=fr).

### Configuration de publicités multimédias payantes dans les destinations {#paid-media-ads}

La structure des destinations est utilisée pour les annonces publicitaires médias payantes. Une fois le consentement vérifié, il est envoyé aux différentes destinations configurées. Pour plus d’informations sur les destinations, consultez le document [Présentation des destinations](/help/destinations/home.md).

#### Données requises pour les destinations

Les destinations d’exportation d’audiences en flux continu (telles que Facebook, le ciblage par liste de clients de Google, Google DV360) prennent en charge différentes identités à partir des données client :

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Vous pouvez activer les audiences de navigation de produit abandonnées et abandonner les audiences de panier pour les publicités médias payantes.

* Flux/Déclenché
   * [Advertising](/help/destinations/catalog/advertising/overview.md)/[Médias payants et médias sociaux](/help/destinations/catalog/social/overview.md)
   * [Mobile](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Destination de diffusion en continu](/help/destinations/catalog/streaming/http-destination.md)
   * [Destination personnalisée créée à l’aide de Destination SDK.](/help/destinations/destination-sdk/overview.md). Si vous êtes un client Real-Time CDP Ultimate, vous pouvez également créer une destination privée [personnalisée à l’aide de Destination SDK](/help/destinations/destination-sdk/overview.md#productized-and-custom-integrations)

## Étapes suivantes {#next-steps}

En réengageant vos clients qui ont abandonné une conversion de manière intelligente et responsable, vous avez, espérons-le, augmenté les conversions et la valeur de la durée de vie du client.

[ Ensuite, vous pouvez explorer d’autres cas d’utilisation pris en charge par Real-Time CDP, tels que l’affichage de contenu personnalisé pour les utilisateurs non authentifiés](/help/rtcdp/partner-data/onsite-personalization.md) sur vos propriétés web.
