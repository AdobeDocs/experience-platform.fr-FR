---
title: Utilisation de la reconnaissance des visiteurs assistée par les partenaires pour personnaliser les expériences Onsite
description: Découvrez comment utiliser la reconnaissance des visiteurs avec l’aide de partenaires pour offrir des expériences personnalisées sur site à vos visiteurs.
source-git-commit: 9d7e8ef99a42e804896f5c9befcf98bb1c010606
workflow-type: tm+mt
source-wordcount: '2530'
ht-degree: 8%

---

# Utiliser la reconnaissance des visiteurs par les partenaires pour personnaliser les expériences sur site

>[!AVAILABILITY]
>
>Cette fonctionnalité est disponible pour les clientes et clients qui disposent d’une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime et Real-Time CDP Ultimate. Consultez la [description des produits](https://helpx.adobe.com/fr/legal/product-descriptions.html) pour en savoir plus sur ces packages et contactez votre représentant ou représentante Adobe pour obtenir plus d’informations.

Découvrez comment utiliser la reconnaissance assistée par les partenaires pour offrir des expériences personnalisées aux visiteurs de vos propriétés web. Utilisez ce tutoriel pour comprendre la séquence d’implémentation de divers éléments dans les solutions Experience Platform et autres solutions Experience Cloud afin d’afficher une expérience personnalisée pour les visiteurs authentifiés et non authentifiés.

![Infographie qui décrit comment utiliser les attributs fournis par les partenaires pour offrir des expériences personnalisées à vos visiteurs.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Exemple de secteur {#industry-example}

Prenons l’exemple d’une marque d’amélioration de la maison dont les taux d’authentification sont faibles. Cette marque souhaite offrir des expériences personnalisées aux nouveaux visiteurs, sans historique préalable ni authentification, et sans se reposer sur les cookies tiers.

Cette marque choisit d’exploiter la technologie de reconnaissance des partenaires pour reconnaître de manière probabiliste le visiteur et offrir une expérience plus personnalisée. Cela permet d’avancer dans la prise en compte lorsque le visiteur passe à l’entonnoir marketing. Par exemple, la marque peut utiliser des signaux démographiques fournis par le partenaire pour le contenu sur site qui séduit les personnes qui ont récemment déménagé et offre une remise sur les produits très vendus.

## Prérequis et planification {#prerequisites-and-planning}

Lorsque vous envisagez d’utiliser les attributs fournis par les partenaires pour offrir des expériences personnalisées à vos visiteurs authentifiés et non authentifiés, tenez compte des conditions préalables suivantes dans votre processus de planification :

* Quelles entrées sont attendues par la technologie de reconnaissance de votre partenaire afin qu’il puisse superposer des attributs supplémentaires ?
* Dans quelle mesure êtes-vous à l’aise avec la personnalisation sur différents canaux et pour différents cas d’utilisation basés sur des attributs dérivés probabilistes, par rapport à des attributs confirmés déterministes ?
* Comment l’expérience d’un visiteur préauthentifié mais reconnu doit-elle changer lorsqu’il s’authentifie ?

### Fonctionnalités de l’interface utilisateur, composants Platform et produits Experience Cloud que vous utiliserez {#ui-functionality-and-elements}

Pour mettre en oeuvre ce cas pratique avec succès, vous devez utiliser plusieurs zones de Real-time Customer Data Platform et d’autres solutions Experience Cloud. Assurez-vous que vous disposez des [autorisations de contrôle d’accès basées sur des attributs](/help/access-control/abac/overview.md) pour toutes ces zones ou demandez à votre administrateur système de vous accorder les autorisations nécessaires.

* Collecte de données
   * [SDK Web Adobe Experience Platform](/help/edge/home.md)
   * [Balises](/help/tags/home.md)
   * [Flux de données](/help/datastreams/overview.md)
* Gestion des données dans Real-Time CDP
   * [Identités](/help/identity-service/namespaces.md)
   * [Schémas](/help/xdm/home.md)
   * [Libellés d’utilisation des données](/help/data-governance/labels/overview.md)
   * [Jeux de données](/help/catalog/datasets/overview.md)
* Personnalisation des propriétés web
   * [Segmentation Edge](/help/segmentation/ui/edge-segmentation.md)
   * [Destinations de personnalisation Edge](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (ou une plateforme de personnalisation de votre choix. Ce tutoriel de cas d’utilisation met en évidence Adobe Target en tant que moteur de personnalisation)

## Comment réaliser le cas d’utilisation : aperçu de haut niveau {#achieve-the-use-case-high-level}

![Infographie qui décrit comment utiliser les attributs fournis par les partenaires pour offrir des expériences personnalisées à vos visiteurs.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Comme **client**, vous obtenez une licence depuis le **partenaire de données** la possibilité de récupérer des informations en temps réel sur les visiteurs anonymes d’un site web.
2. Comme **client**, vous déployez des bibliothèques côté client sur vos propriétés pour appeler **partenaire** Les API et vous configurez le SDK Web ou le SDK Mobile pour envoyer des signaux fournis par les partenaires à Real-Time CDP.
3. Lorsque vous parcourez votre site web ou votre application, la variable **visiteur** est reconnu de manière probabiliste par **partenaire**, qui renvoie des attributs avec un identifiant.
4. Real-Time CDP exécute une segmentation Edge pour évaluer les accès aux événements entrants et conserve les résultats par rapport à [Identifiant ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr).
5. Adobe Target utilise la sortie de segmentation Edge pour restituer l’expérience au **visiteur** pour la personnalisation en session.
6. L’événement est conservé dans son intégralité pour les workflows en aval tels que l’analyse et le reciblage.

## Comment réaliser le cas d’utilisation : instructions détaillées {#step-by-step-instructions}

Parcourez les sections ci-dessous, qui contiennent des liens vers d’autres documents, pour suivre chacune des étapes de la vue d’ensemble de haut niveau ci-dessus.

### Gestion des données : créez un espace de noms, un schéma et un jeu de données d’identité pour gérer les attributs de données. {#data-management}

Pour préparer le cas d’utilisation afin de personnaliser l’expérience des visiteurs non authentifiés, vous devez d’abord configurer la structure de gestion des données dans Real-Time CDP afin de recevoir les données entrantes d’événement en temps réel et de qualification des audiences.

#### Créer un espace de noms d’identité des identifiants de partenaire

Tout d’abord, vous devez créer un espace de noms d’identité d’identifiant de partenaire. Accédez à **[!UICONTROL Client]** > **[!UICONTROL Identités]** dans le rail de gauche, puis sélectionnez **[!UICONTROL Créer un espace de noms d’identité]** dans le coin supérieur droit de l’écran.

![La boîte de dialogue Créer un espace de noms d’identité avec l’identifiant de partenaire est mise en surbrillance.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

En savoir plus sur la manière de procéder [création d’un espace de noms d’identité d’identifiant de partenaire](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Création d’un schéma

Créez ensuite une [!UICONTROL Événement d’expérience] schéma destiné à contenir les données de série temporelle que vous collecterez ultérieurement à partir de vos propriétés web et à utiliser [!UICONTROL XDM ExperienceEvent] comme classe de base du schéma. Découvrez comment [création d’un schéma à l’aide de l’interface utilisateur Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![Espace de travail des schémas avec création de schéma et événement d’expérience XDM mis en surbrillance.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

Lors de la création de votre schéma et [ajouter des groupes de champs à votre schéma ;](/help/xdm/ui/resources/schemas.md#add-field-groups), pensez à ajouter la variable [Page Web Visite](/help/xdm/field-groups/event/web-details.md) et [Carte des identités](/help/xdm/field-groups/profile/identitymap.md) groupes de champs. Cela s’ajoute à d’autres groupes de champs qui s’appliquent à votre propriété numérique et à vos pratiques de collecte de données.

En outre, vous pouvez créer ou réutiliser un groupe de champs existant et l’ajouter à votre schéma, afin de capturer les informations fournies par les partenaires sur le visiteur. Lire comment [création d’un groupe de champs](/help/xdm/ui/resources/field-groups.md) et comment [ajouter des champs](/help/xdm/ui/resources/field-groups.md) au groupe de champs. Par exemple, si vous prévoyez de personnaliser les informations fournies par les partenaires comme la tranche d’âge, l’état de l’emploi, le pouvoir de dépenser mensuel ou les comportements d’achat, demandez à votre groupe de champs d’inclure les champs appropriés.

En supposant que le partenaire de données fournisse un identifiant stable pour le visiteur et que vous souhaitiez l’importer dans Real-Time CDP, veillez à disposer d’un champ nommé de manière appropriée pour l’identifiant dans votre groupe de champs personnalisé. Vous devez également marquer le champ comme identité dans l’espace de noms d’identité que vous avez créé précédemment. N’oubliez pas également de [activation de l’inclusion du schéma dans Profile](/help/xdm/ui/resources/schemas.md#profile).

#### Créer un jeu de données

Vous devez ensuite créer un jeu de données destiné à contenir les données de série temporelle que vous collectez auprès des visiteurs de vos propriétés web et que vous utiliserez pour la personnalisation sur site.

Lisez le tutoriel sur [comment créer un jeu de données](/help/catalog/datasets/user-guide.md#create) et pensez à sélectionner l’option pour créer le jeu de données à partir d’un schéma. Créez le jeu de données en fonction du schéma que vous avez créé à l’étape précédente.

Tout comme lors de la création d’un schéma, vous devez activer l’inclusion du jeu de données dans la variable [!UICONTROL Profil client en temps réel]. Pour plus d’informations sur l’activation du jeu de données à utiliser dans [!UICONTROL Profil client en temps réel], lisez le [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implémentation de la collecte de données d’événement sur votre propriété web {#implement-data-collection}

Après avoir configuré votre configuration de Data Management, vous devez maintenant mettre en oeuvre un événement en temps réel. [collecte de données](/help/collection/home.md) sur votre propriété web. Vous devez instrumenter votre propriété avec la bibliothèque de collecte de données d’Adobe - [!UICONTROL SDK Web] - pour collecter des appels d’événement en temps réel et les renvoyer à Real-Time CDP. Cet élément se compose de quelques tâches distinctes sur quelques composants de collecte de données.

>[!IMPORTANT]
>
>Pour récupérer les attributs fournis par le partenaire, vous devez également *intégrer votre propriété web avec les API des partenaires ou d’autres méthodes pour appeler et récupérer des attributs des partenaires de données en temps réel*. Veuillez discuter de cet aspect avec votre partenaire de choix, car il ne fait pas l’objet de ce tutoriel.

Tout d’abord, utilisez le sélecteur d’applications dans le coin supérieur droit de l’écran pour accéder au **[!UICONTROL Collecte de données]** .

>[!TIP]
>
>Contactez votre administrateur système pour demander l’accès si vous ne pouvez pas voir [!UICONTROL Collecte de données] dans le sélecteur d’applications.

![Sélecteur d’application pour accéder à la section Collecte de données .](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

La variable **[!UICONTROL Collecte de données]** de l’interface utilisateur ressemble à l’image ci-dessous.

![Section Collecte de données de l’interface utilisateur de Platform.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Créer un flux de données

Pour commencer, reportez-vous à la section Collecte de données : [créer un flux de données](/help/datastreams/configure.md). Le flux de données est la base de la manière dont les données sont collectées et correctement acheminées vers l’application d’Adobe appropriée, dans ce cas Experience Platform.

Lorsque vous créez le flux de données, dans la variable **[!UICONTROL Schéma d’événement]** , sélectionnez le schéma que vous avez créé précédemment.

![Sélecteur de schéma d’événement surligné lors de la configuration d’un nouveau flux de données.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Sélectionner le jeu de données d’événement](/help/datastreams/configure.md#aep) que vous avez créé précédemment dans la liste déroulante, cochez les cases en regard de **[!UICONTROL Segmentation Edge]** et **[!UICONTROL Destinations de personnalisation]**, puis sélectionnez **[!UICONTROL Enregistrer]**.

Notez que vous n’avez pas à sélectionner un jeu de données de profil dans ce scénario, car vous incorporez des données de série temporelle basées sur un événement.

#### Créer une propriété de balise

Considérez une propriété comme un conteneur que vous remplissez d’extensions, de règles, d’éléments de données et de bibliothèques lorsque vous déployez des balises sur votre site.

Accédez à **[!UICONTROL Balises]** et sélectionnez **[!UICONTROL Nouvelle propriété]**.

![Créez une propriété de balise.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Renseignez les champs obligatoires et sélectionnez **[!UICONTROL Enregistrer]**.

![Renseignez les champs requis pour votre nouvelle propriété.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Obtention d’informations complètes sur la procédure à suivre [création d’une propriété de balise](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Vous devez ensuite installer différentes extensions dans la propriété . Sélectionnez la propriété de balise et accédez au [!UICONTROL Extensions] .

![Sélectionnez la nouvelle propriété de balise.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Notez que la variable [!UICONTROL Core] l’extension est déjà installée. Vous devez installer deux autres extensions, comme indiqué dans les sections suivantes.

![Afficher les extensions installées.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installation de l’extension SDK Web

Notez que ce tutoriel indique comment instrumenter votre site web avec le SDK Web. Vous pouvez également utiliser [SDK Mobile](https://developer.adobe.com/client-sdks/documentation/) sur votre application pour personnaliser l’expérience pour les visiteurs de votre application.

![Vue de l’extension du SDK Web dans le catalogue des extensions.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Dans l’écran de configuration du SDK Web, accédez au **[!UICONTROL Datastreams]** et fournissez des informations sur l’environnement de test Experience Platform que vous utilisez. Sélectionnez l’environnement de test approprié et le flux de données créé lors des étapes précédentes dans la liste déroulante suivante. Vous pouvez choisir les mêmes valeurs sandbox et datastream pour tous les autres environnements. Laissez les autres paramètres inchangés et sélectionnez **[!UICONTROL Enregistrer]**.

Obtenir des informations complètes sur [procédure d’installation du SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Installation de l’extension du service d’ID

Utilisez la variable [Extension du service d’ID Experience Cloud](/help/tags/extensions/client/id-service/overview.md) pour créer une identité propriétaire unique basée sur les appareils pour les visiteurs dans toutes les solutions Experience Cloud. Recherchez **[!UICONTROL Service d’ID]** dans le catalogue d’extensions, puis installez-le. Conservez tous les paramètres par défaut lors de l’installation de l’extension.

![Vue de l’extension du service d’ID dans le catalogue des extensions.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Configuration des environnements

Ensuite, passez au **[!UICONTROL Environnements]** à partir du volet de navigation de gauche. Au cours de cette étape, vous devez connecter votre site web au réseau Adobe Edge pour récupérer et diffuser les informations sur les visiteurs en temps réel.

Sélectionnez l’icône de boîte à droite pour l’environnement de développement, puis copiez la version standard du fragment de code JavaScript qui apparaît dans une fenêtre modale.

![Icône de case à cocher mise en surbrillance dans la section Environnements de l’interface utilisateur de la collecte de données.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Vous devez ajouter ce fragment de code tout en haut de votre site web. Par conséquent, votre site web lancera un appel au réseau Adobe Edge pour récupérer la logique JavaScript qui sera chargée et exécutée sur la page. Cela permet le fonctionnement de fonctionnalités telles que la génération d’identifiants visiteur, la collecte de données et la personnalisation de l’expérience en temps réel.

#### Configuration des éléments de données

Les éléments de données sont les blocs de construction de votre dictionnaire de données (ou mappage de données). Un seul élément de données est une variable dont la valeur peut être mappée à des chaînes de requête, des URL, des valeurs de cookie, des variables JavaScript, etc. En savoir plus sur [éléments de données](/help/tags/ui/managing-resources/data-elements.md).

Dans ce cas pratique, vous devez configurer deux éléments de données.

Tout d’abord, configurez une `partnerData` élément . Accédez au **[!UICONTROL Éléments de données]** et sélectionnez **[!UICONTROL Créer un élément de données]**.

![Créez un élément de données.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Nommer l’élément de données `partnerData`, laissez la variable [!UICONTROL extension] value as [!UICONTROL Core], et définissez **[!UICONTROL Type d’élément de données]** as **[!UICONTROL Variable JavaScript]**. Entrée `partnerData` dans le champ intitulé **[!UICONTROL Nom de variable JavaScript]** et sélectionnez **[!UICONTROL Enregistrer]**.

![Sélections mises en surbrillance pour configurer correctement l’élément de données partnerData .](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Pour configurer le second élément de données, nommez la nouvelle variable . `pageVisit`, définissez la variable **[!UICONTROL Extension]** to **[!UICONTROL Adobe Experience Platform]** et choisissez **[!UICONTROL Objet XDM]** comme type de données.

![Sélections mises en surbrillance pour configurer correctement l’élément de données pageVisit .](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

Dans le schéma, sélectionnez les attributs tiers qui correspondent aux valeurs attendues du partenaire de données. Sélectionnez ensuite le bouton radio intitulé **[!UICONTROL Fournir un objet entier]**. Sélectionnez l&#39;icône qui ressemble à une base de données et choisissez le `partnerData` élément de données que vous avez créé précédemment.

#### Configuration de règles

Dans le **[!UICONTROL Règles]** , vous pouvez configurer votre site web pour envoyer une demande de personnalisation afin d’y Adobe avec les attributs chargés dans les éléments de données que vous venez de créer. En savoir plus sur [création de règles](/help/tags/ui/managing-resources/rules.md).

Sélectionner **[!UICONTROL Créer une règle]**. Nom de cette règle **[!UICONTROL Personnaliser]** et sélectionnez le signe + en regard de **[!UICONTROL Événements]**. Sélectionner **[!UICONTROL Bas de page]** comme événement et enregistrez.

![Sélections pour la partie type d’événement d’une règle.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Sélectionnez le signe + en regard de **[!UICONTROL Actions]**. Mettre à jour l’extension vers **[!UICONTROL SDK Web Adobe Experience Platform]** et défini **[!UICONTROL Type d’action]** to **[!UICONTROL Envoyer un événement]**.

![Sélections pour la partie de type d’action d’une règle.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Dans la **[!UICONTROL Type]** sélecteur de liste déroulante à droite, sélectionnez `web.webpagedetails.pageViews` comme type d’événement.

![Sélectionnez le type d’événement.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Sélectionnez l’icône de base de données en regard des données XDM et sélectionnez le `pageVisit` élément de données.

Faites défiler la liste des configurations d’action et assurez-vous de cocher la case intitulée **[!UICONTROL Rendu des décisions de personnalisation visuelle]**. Ceci est important pour permettre le rendu visuel des expériences diffusées via Adobe Target ou d’autres produits similaires sur la page web. Sélectionner **[!UICONTROL Conserver les modifications]**, puis **[!UICONTROL Enregistrer]** la règle.

![Cochez la case Rendre les décisions de personnalisation visuelle .](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Configuration du processus de publication

Pour déployer cette configuration sur la page web, l’étape suivante consiste à créer une bibliothèque contenant les ressources que vous venez de créer. En savoir plus sur [configuration d’un flux de publication](/help/tags/ui/publishing/publishing-flow.md).

Sélectionner **[!UICONTROL Flux de publication]** puis **[!UICONTROL Ajouter une bibliothèque]**.

Sélectionner **[!UICONTROL Ajout de toutes les ressources modifiées]**, attribuez un nom à la bibliothèque, définissez l’environnement sur **[!UICONTROL Développement]** et sélectionnez **[!UICONTROL Enregistrement et création pour le développement]**.

![Création d’une bibliothèque et déploiement dans l’environnement de développement](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Test de votre site web

À ce stade, votre site web doit être entièrement instrumenté avec le SDK web. Pour vérifier que la collecte de données fonctionne comme prévu, vous pouvez accéder à votre site web et utiliser les outils de développement de votre navigateur pour inspecter le trafic réseau.

Entrée `interact` dans la zone de recherche, actualisez la page. les appels réseau de votre site web vers le réseau Adobe Edge s’affichent.

![Affichage des événements réseau renseignés dans les outils de développement.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personnalisation {#personalization}

Vous êtes maintenant prêt à créer et activer des audiences pour la personnalisation.

#### Configuration de la segmentation Edge

Configuration [segmentation de périphérie](/help/segmentation/ui/edge-segmentation.md) ainsi, l’appartenance de l’audience de vos visiteurs est évaluée en temps réel, lorsqu’ils visitent votre propriété web.

Veillez également à configurer une [stratégie de fusion active-on-edge](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) pour les audiences Edge.

#### Intégration à Adobe Target ou à une autre destination de personnalisation personnalisée

Vous êtes maintenant prêt à intégrer avec un moteur de personnalisation pour afficher du contenu personnalisé pour les visiteurs de votre site web ou de votre application. Adobe recommande d’utiliser la variable [Destination Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) à cet effet.

>[!IMPORTANT]
>
>Lisez le tutoriel sur [activation d’audiences vers des destinations de personnalisation de périphérie](/help/destinations/ui/activate-edge-personalization-destinations.md) pour une vue complète des étapes nécessaires à l’activation de vos audiences.

## Limites et dépannage {#limitations-and-troubleshooting}

Notez que les limites suivantes s’appliquent lorsque vous utilisez le cas d’utilisation décrit sur cette page :

* Si vous utilisez des identifiants de partenaire, sachez que ces identifiants ne sont pas utilisés lors de la création de vos [graphique d’identités](/help/identity-service/ui/identity-graph-viewer.md).

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* [Complétez les profils propriétaires avec les attributs des partenaires de données de confiance pour améliorer votre base de données, obtenir de nouvelles informations sur votre base de clientes et clients et optimiser l’audience.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* Utilisation de la prise en charge de données tierces dans Real-Time CDP pour [développer votre base de profils avec des profils de prospect des partenaires de données et interagir avec eux pour acquérir ou atteindre de nouveaux clients ;](/help/rtcdp/partner-data/prospecting.md).
* [Activation étendue des profils de prospects et des audiences de prospects](/help/destinations/ui/activate-prospect-audiences.md) pour sélectionner des destinations.