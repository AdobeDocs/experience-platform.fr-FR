---
title: Personnaliser des expériences sur site pour les visiteurs inconnus à l’aide de la reconnaissance des visiteurs assistée par des partenaires
description: Découvrez comment utiliser la reconnaissance des visiteurs et visiteuses par les partenaires pour personnaliser les expériences sur site de vos visiteurs et visiteuses.
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: 02f2082e695d157415c9e0c59ca5d371c94bb991
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 89%

---

# Personnaliser des expériences sur site pour les visiteurs inconnus à l’aide de la reconnaissance des visiteurs assistée par des partenaires

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clients qui disposent d’une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Consultez la [description des produits](https://helpx.adobe.com/fr/legal/product-descriptions.html) pour en savoir plus sur ces packages et contactez votre représentant ou représentante Adobe pour obtenir plus d’informations.

Découvrez comment utiliser la reconnaissance par les partenaires pour offrir des expériences personnalisées aux visiteurs et visiteuses de vos propriétés web. Utilisez ce tutoriel pour comprendre la séquence d’implémentation de divers éléments dans les solutions Experience Platform et autres solutions Experience Cloud, afin d’afficher une expérience personnalisée pour les visiteurs et visiteuses authentifiés et non authentifiés.

![Infographie décrivant comment utiliser les attributs fournis par les partenaires pour offrir des expériences personnalisées à vos visiteurs et visiteuses.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## Pourquoi envisager ce cas d’utilisation {#why-this-use-case}

La fragmentation des expériences digitales, à mesure que les consommateurs interagissent avec les marques de multiples manières, est très réelle et devient de plus en plus difficile à résoudre. La reconnaissance des utilisateurs et utilisatrices limite les meilleures stratégies d’engagement client pour offrir des expériences cohérentes, des recommandations ciblées et des interactions personnalisées.

C’est là que la reconnaissance en temps réel assistée par un partenaire peut faire une différence significative. Adobe permet aux partenaires d’identité de se connecter à nos offres sophistiquées de collecte de données côté client et d’optimisation de l’expérience de pointe, afin de relever efficacement la barre en matière de diffusion d’expérience à partir de la première visite, sans historique ni authentification préalable.

Cela s’avère particulièrement utile pour les marchés verticaux présentant de faibles taux d’authentification, tels que les biens de consommation emballés, la vente au détail en ligne, etc.

## Exemple de secteur {#industry-example}

Prenons l’exemple d’une marque proposant des articles d’aménagement intérieur dont les taux d’authentification sont faibles. Cette marque souhaite offrir des expériences personnalisées aux visiteurs et visiteuses qui se connectent pour la première fois, sans historique préalable ni authentification, et sans avoir recours à des cookies tiers.

Cette marque choisit d’exploiter la technologie de reconnaissance des partenaires pour reconnaître de manière probabiliste la personne visiteuse et lui offrir ainsi une expérience davantage personnalisée. La façon de considérer la personne visiteuse est d’autant plus précise qu’elle progresse dans l’entonnoir marketing. Par exemple, la marque peut utiliser des signaux démographiques fournis par le partenaire pour un contenu sur site qui séduit les personnes ayant récemment déménagé et offrir ainsi une remise sur les produits de bricolage populaires.

## Prérequis et planification {#prerequisites-and-planning}

Lorsque vous envisagez d’utiliser des attributs fournis par les partenaires pour offrir des expériences personnalisées à vos visiteurs et visiteuses authentifiés et non authentifiés, tenez compte des conditions préalables suivantes dans votre processus de planification :

* Quelles entrées sont attendues par la technologie de reconnaissance de votre partenaire afin de pouvoir superposer des attributs supplémentaires ?
* Dans quelle mesure seriez-vous à l’aise de fournir une personnalisation dans différents canaux et pour différents cas d’utilisation basés sur des jeux de données dérivés de manière probabiliste, par rapport aux attributs confirmés de manière déterministe ?
* Comment l’expérience d’une personne visiteuse préauthentifiée mais reconnue doit-elle changer lorsqu’elle s’authentifie ?

### Fonctionnalités de l’interface utilisateur, composants Platform et produits Experience Cloud que vous allez utiliser {#ui-functionality-and-elements}

Pour mettre en œuvre ce cas d’utilisation avec succès, vous devez utiliser plusieurs zones de Real-time Customer Data Platform et d’autres solutions Experience Cloud. Assurez-vous que vous disposez des [autorisations de contrôle d’accès basées sur des attributs](/help/access-control/abac/overview.md) pour toutes ces zones ou demandez à votre administrateur ou administratrice système de vous accorder les autorisations nécessaires.

* Collecte de données
   * [SDK Web Adobe Experience Platform](/help/web-sdk/home.md)
   * [Balises](/help/tags/home.md)
   * [Flux de données](/help/datastreams/overview.md)
* Gestion des données sur Real-Time CDP
   * [Identités](/help/identity-service/features/namespaces.md)
   * [Schémas](/help/xdm/home.md)
   * [Libellés d’utilisation des données](/help/data-governance/labels/overview.md)
   * [Jeux de données](/help/catalog/datasets/overview.md)
* Personnalisation des propriétés web
   * [Segmentation Edge](/help/segmentation/methods/edge-segmentation.md)
   * [Destinations de personnalisation Edge](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (ou une plateforme de personnalisation de votre choix. Ce tutoriel de cas d’utilisation met en évidence Adobe Target en tant que moteur de personnalisation)

## Présentation vidéo {#video-walkthrough}

Regardez le tutoriel vidéo ci-dessous pour une présentation détaillée de la personnalisation des expériences sur site pour les visiteurs inconnus :

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Comment réaliser le cas d’utilisation : vue d’ensemble de haut niveau {#achieve-the-use-case-high-level}

![Infographie décrivant comment utiliser les attributs fournis par les partenaires pour offrir des expériences personnalisées à vos visiteurs et visiteuses.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. En tant que **client ou cliente**, vous obtenez du **partenaire de données** la possibilité de récupérer des informations en temps réel sur les visiteurs et visiteuses anonymes d’un site web.
2. En tant que **client ou cliente**, vous déployez des bibliothèques côté client sur vos propriétés pour appeler les API **partenaires** et vous configurez le SDK Web ou le SDK Mobile pour envoyer des signaux fournis par les partenaires à Real-Time CDP.
3. Lorsque vous parcourez votre site web ou votre application, **la personne visiteuse** est reconnue de manière probabiliste par le **partenaire**, qui renvoie des attributs avec un ID.
4. Real-Time CDP exécute une segmentation Edge pour évaluer les accès aux événements entrants et conserve les résultats par rapport à l’[identifiant ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).
5. Adobe Target utilise la sortie de segmentation Edge pour restituer l’expérience **au visiteur ou à la visiteuse** dans le cadre de la personnalisation en session.
6. L’événement est conservé dans son intégralité pour les workflows en aval, tels que l’analyse et le reciblage.

## Comment réaliser le cas d’utilisation : instructions détaillées {#step-by-step-instructions}

Parcourez les sections ci-dessous, qui contiennent des liens vers d’autres documents, pour suivre chacune des étapes de la vue d’ensemble de haut niveau ci-dessus.

### Gestion des données : créer un espace de noms, un schéma et un jeu de données d’identité pour gérer les attributs de données {#data-management}

Pour préparer le cas d’utilisation et personnaliser l’expérience des visiteurs et visiteuses non authentifiés, vous devez d’abord configurer la structure de gestion des données dans Real-Time CDP afin de recevoir les données entrantes d’événement en temps réel et de qualification des audiences.

#### Créer un espace de noms d’identité de l’ID du partenaire

Tout d’abord, vous devez créer un espace de noms d’identité de l’ID du partenaire. Accédez à **[!UICONTROL Client]** > **[!UICONTROL Identités]** dans le rail de gauche, puis sélectionnez **[!UICONTROL Créer un espace de noms d’identité]** dans le coin supérieur droit de l’écran.

![La boîte de dialogue Créer un espace de noms d’identité s’affiche avec l’ID du partenaire en surbrillance.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

En savoir plus sur la manière de [créer un espace de noms d’identité de l’ID du partenaire](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Créer un schéma

Créez ensuite un schéma d’[!UICONTROL Événement d’expérience] destiné à contenir les données de série temporelle que vous collecterez ultérieurement à partir de vos propriétés web. Assurez-vous d’utiliser [!UICONTROL XDM ExperienceEvent] comme classe de base du schéma. Découvrez comment [créer un schéma dans l’interface utilisateur d’Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![Espace de travail Schémas avec le menu de création de schéma qui s’affiche et l’événement d’expérience XDM mis en surbrillance.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Lors de la création du schéma et de l’[ajout de groupes de champs au schéma](/help/xdm/ui/resources/schemas.md#add-field-groups), pensez à ajouter les groupes de champs [Visite de page web](/help/xdm/field-groups/event/web-details.md) et [Mappage d’identités](/help/xdm/field-groups/profile/identitymap.md). Outre ces deux groupes, ajoutez les autres groupes de champs applicables à votre propriété numérique et à vos pratiques de collecte de données.

Vous pouvez également créer ou réutiliser un groupe de champs existant et l’ajouter à votre schéma, afin de capturer les informations fournies par les partenaires sur le visiteur ou la visiteuse. Découvrez comment [créer un groupe de champs](/help/xdm/ui/resources/field-groups.md) et [ajouter des champs](/help/xdm/ui/resources/field-groups.md) au groupe de champs. Par exemple, si vous prévoyez de personnaliser vos données en fonction des informations fournies par le partenaire, comme la tranche d’âge, le statut professionnel, le pouvoir d’achat mensuel ou les comportements d’achat, votre groupe de champs doit comporter les champs appropriés.

Si le partenaire de données fournit un identifiant stable pour le visiteur ou la visiteuse et que vous souhaitez l’importer dans Real-Time CDP, assurez-vous de disposer d’un champ au nom approprié pour l’identifiant dans votre groupe de champs personnalisés. Vous devez également marquer le champ comme identité dans l’espace de noms d’identité que vous avez créé précédemment. Veillez également à [inclure le schéma dans le profil](/help/xdm/ui/resources/schemas.md#profile).

#### Créer un jeu de données

Vous devez ensuite créer un jeu de données destiné à contenir les données de série temporelle que vous collectez auprès des visiteurs et visiteuses de vos propriétés web et que vous utiliserez pour la personnalisation sur site.

Suivez le tutoriel sur la [création d’un jeu de données](/help/catalog/datasets/user-guide.md#create) et veillez à sélectionner l’option permettant de créer le jeu de données à partir d’un schéma. Créez le jeu de données à partir du schéma que vous avez créé à l’étape précédente.

Tout comme lors de la création d’un schéma, vous devez activer l’inclusion du jeu de données dans le [!UICONTROL Profil client en temps réel]. Pour plus d’informations sur l’inclusion du jeu de données dans le [!UICONTROL Profil client en temps réel], consultez le [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implémenter la collecte de données d’événement sur votre propriété web {#implement-data-collection}

Une fois que vous avez terminé la configuration de la gestion des données, vous devez mettre en œuvre une [collecte de données](/help/collection/home.md) d’événement en temps réel sur votre propriété web. Votre propriété doit utiliser la bibliothèque de collecte de données Adobe ([!UICONTROL SDK Web]) pour collecter des appels d’événement en temps réel et les renvoyer à Real-Time CDP. Cet élément se compose de quelques tâches distinctes sur quelques composants de collecte de données.

>[!IMPORTANT]
>
>Pour récupérer les attributs fournis par le partenaire, vous devez également *intégrer votre propriété web aux API du partenaire ou à d’autres méthodes pour appeler et récupérer des attributs des partenaires de données en temps réel*. Consultez votre partenaire pour connaître la procédure à suivre, car ce n’est pas l’objet de ce tutoriel.

Tout d’abord, utilisez le sélecteur d’applications dans le coin supérieur droit de l’écran pour accéder à la section **[!UICONTROL Collecte de données]**.

>[!TIP]
>
>Contactez l’administrateur ou l’administratrice système pour demander l’accès si la [!UICONTROL Collecte de données] n’apparaît pas dans le sélecteur d’applications.

![Le sélecteur d’application permet d’accéder à la section Collecte de données.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

La section **[!UICONTROL Collecte de données]** de l’interface utilisateur ressemble à l’image ci-dessous.

![Section Collecte de données de l’interface utilisateur de Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Créer un train de données

Pour commencer dans la section Collecte de données, nous allons apprendre à [créer un train de données](/help/datastreams/configure.md). Le train de données définit la manière dont les données sont collectées et correctement acheminées vers l’application d’Adobe appropriée, en l’occurrence Experience Platform.

Lorsque vous créez le train de données, dans le champ **[!UICONTROL Schéma d’événement]**, sélectionnez le schéma que vous avez créé précédemment.

![Le sélecteur de schéma d’événement est mis en surbrillance lors de la configuration d’un nouveau train de données.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Sélectionnez le jeu de données d’événement](/help/datastreams/configure.md#aep) créé précédemment dans la liste déroulante, cochez les cases en regard de **[!UICONTROL Segmentation Edge]** et **[!UICONTROL Destinations de personnalisation]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

Notez que vous n’avez pas besoin de sélectionner un jeu de données de profil dans ce scénario, car vous incorporez des données de série temporelle basées sur un événement.

#### Créer une propriété de balise

Une propriété est un conteneur que vous remplissez d’extensions, de règles, d’éléments de données et de bibliothèques lorsque vous déployez des balises sur votre site.

Accédez à **[!UICONTROL Balises]** et sélectionnez **[!UICONTROL Nouvelle propriété]**.

![Création d’une propriété de balise.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Renseignez les champs obligatoires et cliquez sur **[!UICONTROL Enregistrer]**.

![Renseignement des champs requis pour votre nouvelle propriété.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Prenez connaissance des tenants et aboutissants de la [création d’une propriété de balise](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=fr).

Vous devez ensuite installer plusieurs extensions dans la propriété. Sélectionnez la propriété de balise et accédez à la section [!UICONTROL Extensions].

![Sélection de la nouvelle propriété de balise.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Notez que l’extension [!UICONTROL Core] est déjà installée. Vous devez installer deux autres extensions, comme indiqué dans les sections suivantes.

![Affichage des extensions installées.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installer l’extension SDK Web

Notez que ce tutoriel indique comment manipuler votre site web avec le SDK Web. Vous pouvez également utiliser le [SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) sur votre application pour personnaliser l’expérience des visiteurs et visiteuses de votre application.

![Vue de l’extension du SDK Web dans le catalogue des extensions.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Dans l’écran de configuration du SDK Web, accédez à la section **[!UICONTROL Trains de données]** et fournissez des informations sur la sandbox Experience Platform que vous utilisez. Sélectionnez la sandbox appropriée et le train de données créé lors des étapes précédentes dans la liste déroulante suivante. Vous pouvez choisir les mêmes valeurs de sandbox et de train de données pour tous les autres environnements. Laissez les autres paramètres inchangés et sélectionnez **[!UICONTROL Enregistrer]**.

Obtenez des informations complètes sur la [procédure d’installation du SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html?lang=fr).

#### Installer l’extension du service d’ID

Utilisez l’[Extension du service Experience Cloud ID](/help/tags/extensions/client/id-service/overview.md) pour créer une identité propriétaire unique basée sur les appareils pour les visiteurs et visiteuses de toutes les solutions Experience Cloud. Recherchez le **[!UICONTROL Service d’ID]** dans le catalogue d’extensions, puis installez-le. Conservez tous les paramètres par défaut lors de l’installation de l’extension.

![Vue de l’extension du service d’ID dans le catalogue d’extensions.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configurer les environnements

Ensuite, passez à la section **[!UICONTROL Environnements]** à partir du volet de navigation de gauche. Au cours de cette étape, vous devez connecter votre site web au réseau Adobe Edge pour récupérer et diffuser les informations sur les visiteurs et les visiteuses en temps réel.

Sélectionnez l’icône de case à cocher à droite pour l’environnement de développement, puis copiez la version standard du fragment de code JavaScript qui s’affiche dans une fenêtre modale.

![Icône de case à cocher mise en surbrillance dans la section Environnements de l’interface utilisateur de la collecte de données.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Vous devez ajouter ce fragment de code tout en haut de votre site web. Par conséquent, votre site web lancera un appel au réseau Adobe Edge pour récupérer la logique JavaScript qui sera chargée et exécutée sur la page. Vous aurez ainsi accès aux fonctionnalités telles que la génération d’identifiants visiteur, la collecte de données et la personnalisation de l’expérience en temps réel.

#### Configurer les éléments de données

Les éléments de données sont les blocs de construction de votre dictionnaire de données (ou mappage de données). Un seul élément de données est une variable dont la valeur peut être mappée à des chaînes de requête, des URL, des valeurs de cookie, des variables JavaScript, etc. En savoir plus sur les [éléments de données](/help/tags/ui/managing-resources/data-elements.md).

Dans ce cas d’utilisation, vous devez configurer deux éléments de données.

Tout d’abord, configurez un élément `partnerData`. Accédez à la section **[!UICONTROL Éléments de données]** et sélectionnez **[!UICONTROL Créer un élément de données]**.

![Création d’un élément de données.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Nommez l’élément de données `partnerData`, laissez la valeur d’[!UICONTROL extension] sur [!UICONTROL Core] et définissez le **[!UICONTROL type d’élément de données]** sur **[!UICONTROL Variable JavaScript]**. Entrez `partnerData` dans le champ intitulé **[!UICONTROL Nom de variable JavaScript]** et sélectionnez **[!UICONTROL Enregistrer]**.

![Sélections mises en surbrillance permettant de configurer correctement l’élément de données partnerData.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Pour configurer le deuxième élément de données, nommez la nouvelle variable `pageVisit`, définissez l’**[!UICONTROL extension]** sur **[!UICONTROL Adobe Experience Platform]** et choisissez **[!UICONTROL Objet XDM]** comme type de données.

![Sélections mises en surbrillance pour configurer correctement l’élément de données pageVisit.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Dans le schéma, sélectionnez les attributs tiers qui correspondent aux valeurs attendues du partenaire de données. Sélectionnez ensuite le bouton radio intitulé **[!UICONTROL Fournir un objet entier]**. Sélectionnez l’icône qui ressemble à une base de données et choisissez l’élément de données `partnerData` que vous avez créé précédemment.

#### Configurer les règles

Dans la section **[!UICONTROL Règles]**, vous pouvez configurer votre site web de sorte à envoyer une requête de personnalisation à Adobe avec les attributs chargés dans les éléments de données que vous venez de créer. En savoir plus sur la [création de règles](/help/tags/ui/managing-resources/rules.md).

Sélectionnez **[!UICONTROL Créer une règle]**. Nommez cette règle **[!UICONTROL Personnaliser]** et sélectionnez le signe + en regard d’**[!UICONTROL Événements]**. Sélectionnez **[!UICONTROL Bas de page]** comme événement et enregistrez.

![Sélections de la partie de type d’événement d’une règle.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Sélectionnez le signe + en regard d’**[!UICONTROL Actions]**. Mettez à jour l’extension sur **[!UICONTROL SDK Web d’Adobe Experience Platform]** et définissez **[!UICONTROL Type d’action]** sur **[!UICONTROL Envoyer un événement]**.

![Sélections pour la partie de type d’action d’une règle.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Dans le sélecteur de liste déroulante **[!UICONTROL Type]**, sélectionnez `web.webpagedetails.pageViews` comme type d’événement.

![Sélection du type d’événement.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Sélectionnez l’icône de base de données en regard des données XDM et sélectionnez l’élément de données `pageVisit`.

Faites défiler la liste des configurations d’action et assurez-vous de cocher la case intitulée **[!UICONTROL Rendu des décisions de personnalisation visuelle]**. Ceci est important pour permettre le rendu visuel des expériences diffusées via Adobe Target ou d’autres produits similaires sur la page web. Sélectionnez **[!UICONTROL Conserver les modifications]**, puis **[!UICONTROL enregistrez]** la règle.

![Sélection de la case Rendu des décisions de personnalisation visuelle.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Configurer le processus de publication

Pour déployer cette configuration sur la page web, l’étape suivante consiste à créer une bibliothèque contenant les ressources que vous venez de créer. En savoir plus sur la [configuration d’un flux de publication](/help/tags/ui/publishing/publishing-flow.md).

Sélectionnez **[!UICONTROL Flux de publication]**, puis **[!UICONTROL Ajouter une bibliothèque]**.

Sélectionnez **[!UICONTROL Ajouter toutes les ressources modifiées]**, attribuez un nom à la bibliothèque, définissez l’environnement sur **[!UICONTROL Développement]** et sélectionnez **[!UICONTROL Enregistrer et créer pour le développement]**.

![Création d’une bibliothèque et déploiement dans l’environnement de développement](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Tester votre site web

À ce stade, votre site web doit être entièrement instrumenté avec le SDK Web. Pour vérifier que la collecte de données fonctionne comme prévu, vous pouvez accéder à votre site web et utiliser les outils de développement de votre navigateur pour inspecter le trafic réseau.

Entrez `interact` dans la zone de recherche et actualisez la page. Les appels réseau de votre site web vers le réseau Adobe Edge doivent s’afficher.

![Affichage des événements réseau renseignés dans les outils de développement.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personnalisation {#personalization}

Vous pouvez à présent créer et activer des audiences pour la personnalisation.

#### Créer une audience et configurer la segmentation Edge

Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Client]** > **[!UICONTROL Audiences]** et créez une audience pour capturer les visiteurs de votre site web.

![Vue sur la navigation vers les audiences.](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

Vous devez configurer votre audience avec la [segmentation Edge](/help/segmentation/methods/edge-segmentation.md) afin que l’appartenance à l’audience de vos visiteurs soit évaluée en temps réel, lorsqu’ils visitent votre propriété web.

Veillez également à configurer une [politique de fusion Active-On-Edge](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) pour les audiences Edge.

#### Intégrer Adobe Target ou une autre destination de personnalisation personnalisée

Vous pouvez maintenant intégrer un moteur de personnalisation pour afficher du contenu personnalisé pour les visiteurs et visiteuses de votre site web ou de votre application. Adobe recommande d’utiliser la [Destination Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) à cet effet.

>[!IMPORTANT]
>
>Lisez le tutoriel sur l’[activation d’audiences vers des destinations de personnalisation Edge](/help/destinations/ui/activate-edge-personalization-destinations.md) pour une vue complète des étapes nécessaires à l’activation de vos audiences.

## Limites et dépannage {#limitations-and-troubleshooting}

Notez que les limites suivantes s’appliquent lorsque vous utilisez le cas d’utilisation décrit sur cette page :

* Si vous utilisez des ID de partenaire, sachez que ceux-ci ne sont pas utilisés lors de la création de votre [graphique d’identité](/help/identity-service/features/identity-graph-viewer.md).

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* [Complétez les profils propriétaires avec les attributs des partenaires de données de confiance pour améliorer votre base de données, obtenir de nouvelles informations sur votre base de clientèle et optimiser l’audience.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilisez la prise en charge de données tierces dans Real-Time CDP pour [développer votre base de profils avec les profils de prospects des partenaires de données et interagissez avec eux pour acquérir ou atteindre une nouvelle clientèle](/help/rtcdp/partner-data/prospecting.md).
* [Activation étendue des profils et des audiences de prospects](/help/destinations/ui/activate-prospect-audiences.md) pour sélectionner des destinations.
