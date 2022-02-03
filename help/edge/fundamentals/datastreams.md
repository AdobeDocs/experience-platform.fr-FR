---
title: Configuration du flux de données pour le SDK Web Experience Platform
description: 'Découvrez comment configurer les flux de données. '
keywords: configuration;datastreams;datastreamId;edge;datastream id;paramètres d’environnement;edgeConfigId;identité;synchronisation des identifiants activée;ID de conteneur de synchronisation;sandbox;flux de données;jeu de données d’événement;cible;code client;jeton de propriété;ID d’environnement cible;destinations de cookie;destinations d’URL;ID de suite de rapports de paramètres Analytics;ID de blocage
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: d3f1a6a5f3f10b8ccbe73ebc744dc60bbbf1bb07
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 3%

---


# Configuration d’un flux de données

La configuration du SDK Web Adobe Experience Platform est fractionnée en deux endroits. Le [configuration, commande](configuring-the-sdk.md) dans le SDK contrôle les éléments qui doivent être gérés sur le client, comme la variable `edgeDomain`. Les flux de données gèrent toutes les autres configurations pour le SDK. Lorsqu’une demande est envoyée au réseau Edge Adobe Experience Platform, la variable `edgeConfigId` sert à référencer la configuration côté serveur. Cela vous permet de mettre à jour la configuration sans avoir à apporter de modifications au code sur votre site web.

Votre entreprise doit être configurée pour cette fonctionnalité. Veuillez contacter votre responsable du succès client pour qu’il soit mis en liste autorisée.

## Création d’une configuration de flux de données

Vous pouvez créer et gérer des flux de données dans l’interface utilisateur de la collecte de données en sélectionnant **[!UICONTROL Datastreams]** dans le volet de navigation de gauche.

![navigation de l’outil datastreams](../images/datastreams/config.png)

>[!NOTE]
>
>Lorsque vous pouvez accéder à la variable [!UICONTROL Datastreams] que vous utilisiez ou non les fonctionnalités de gestion des balises de Platform, vous devez disposer des autorisations de développeur pour gérer les flux de données eux-mêmes. Voir [permissions utilisateur](../../tags/ui/administration/user-permissions.md) pour plus d’informations.

Créez un flux de données en cliquant sur **[!UICONTROL Nouvelle structure de données]** dans la zone supérieure droite de l’écran. Après avoir fourni un nom et une description, vous êtes invité à définir les paramètres par défaut de chaque environnement. Les paramètres disponibles sont présentés ci-dessous.

Lors de la création d’un flux de données, trois environnements sont automatiquement créés avec des paramètres identiques. Ces trois environnements : *dev*, *étape*, et *prod*. Ils correspondent aux trois environnements par défaut des balises. Lorsque vous créez une bibliothèque de balises dans un environnement de développement, la bibliothèque utilise automatiquement l’environnement de développement de votre configuration. Vous pouvez modifier les paramètres dans des environnements individuels autant que vous le souhaitez.

ID utilisé dans le SDK en tant que `edgeConfigId` est un identifiant composite qui spécifie la configuration et l’environnement (par exemple, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Si aucun environnement n’est présent dans l’ID composite (par exemple, `stage` dans l’exemple précédent), alors l’environnement de production est utilisé.

Vous trouverez ci-dessous les paramètres disponibles pour chaque environnement de configuration. La plupart des sections peuvent être activées ou désactivées. Lorsque cette option est désactivée, vos paramètres sont enregistrés, mais ne sont pas principaux.

## [!UICONTROL ID tiers] paramètres

La section ID tiers est la seule section toujours active. Deux paramètres sont disponibles : &quot;[!UICONTROL Synchronisation des identifiants tiers activée]&quot; et &quot;[!UICONTROL ID de conteneur de synchronisation des identifiants tiers]&quot;.

![Section Identité de l’interface utilisateur de configuration](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Synchronisation des identifiants tiers activée]

Contrôle si le SDK effectue ou non des synchronisations d’identité avec des partenaires tiers.

### [!UICONTROL ID de conteneur de synchronisation des identifiants tiers]

Les synchronisations des identifiants peuvent être regroupées en conteneurs afin de permettre l’exécution de différentes synchronisations des identifiants à différents moments. Cela contrôle le conteneur des synchronisations des identifiants exécuté pour un identifiant de configuration donné.

## Paramètres d’Adobe Experience Platform

Les paramètres répertoriés ici vous permettent d’envoyer des données à Adobe Experience Platform. N’activez cette section que si vous avez acheté Adobe Experience Platform.

![Bloc de paramètres Adobe Experience Platform](../images/datastreams/platform-config.png)

| Champ | Description |
| --- | --- |
| [!UICONTROL Environnement de test] | **(Obligatoire)** Sélectionnez l’environnement de test Platform auquel vous souhaitez envoyer des données. Les environnements de test sont des partitions virtuelles dans Adobe Experience Platform qui vous permettent d’isoler vos données et implémentations des autres membres de votre organisation. Pour plus d’informations sur leur fonctionnement, voir [documentation des environnements de test](../../sandboxes/home.md). |
| [!UICONTROL Jeu de données d’événement] | **(Obligatoire)** Sélectionnez le jeu de données Platform vers lequel les données d’événement client seront diffusées. Ce schéma doit utiliser la variable [Classe XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Jeu de données de profil] | Sélectionnez le jeu de données Platform auquel les données d’attributs du client seront envoyées. Ce schéma doit utiliser la variable [Classe XDM Individual Profile](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Cochez cette case pour activer l’Offer decisioning pour une mise en oeuvre du SDK Web Platform. Consultez le guide sur la [utilisation de l’Offer decisioning avec le SDK Web Platform](../personalization/offer-decisioning/offer-decisioning-overview.md) pour plus d’informations sur l’implémentation. Pour plus d’informations sur les fonctionnalités d’Offer decisioning, reportez-vous à la section [Documentation Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=fr). |
| [!UICONTROL Segmentation Edge] | Cochez cette case pour activer [segmentation de périphérie](../../segmentation/ui/edge-segmentation.md) pour ce flux de données. Lorsque le SDK Web Platform envoie des données par le biais d’un flux de données activé pour la segmentation Edge, toutes les adhésions de segment mises à jour pour le profil en question sont renvoyées dans la réponse.<br><br>Cette option peut être utilisée conjointement avec [!UICONTROL Destinations de personnalisation] pour [Cas d’utilisation de la personnalisation de la page suivante](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinations de personnalisation] | Utilisé en combinaison avec la propriété [!UICONTROL Segmentation Edge] , cette option permet à la banque de données de se connecter à des moteurs de personnalisation tels qu’Adobe Target. Reportez-vous à la documentation des destinations pour obtenir des instructions spécifiques sur [configuration des destinations de personnalisation](../../destinations/ui/configure-personalization-destinations.md). |

## Paramètres Adobe Target

Pour configurer Adobe Target, vous devez fournir un code client. Les autres champs sont facultatifs.

![Bloc de paramètres Adobe Target](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>L’organisation associée au code client doit correspondre à l’organisation dans laquelle l’ID de configuration est créé.

### [!UICONTROL Code client]

Identifiant unique d’un compte cible. Pour le trouver, vous pouvez accéder à [!UICONTROL Adobe Target] > [!UICONTROL Configuration]> [!UICONTROL Implémentation] > [!UICONTROL paramètres de modification] en regard de [!UICONTROL télécharger] pour [!UICONTROL at.js] ou [!UICONTROL mbox.js]

### [!UICONTROL Jeton de propriété]

[!DNL Target] permet aux clients de contrôler les autorisations par l’utilisation des propriétés. Vous trouverez des détails dans la section [Autorisations d’entreprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=fr) de la section [!DNL Target] documentation.

Le jeton de propriété se trouve dans [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Propriétés]

### [!UICONTROL Identifiant d’environnement de Target]

[Environnements](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) dans Adobe Target, vous pouvez gérer votre mise en oeuvre à toutes les étapes du développement. Ce paramètre spécifie l’environnement que vous allez utiliser avec chaque environnement.

Adobe recommande de définir cette variable différemment pour chacun de vos `dev`, `stage`, et `prod` des environnements de flux de données pour simplifier les choses. Cependant, si des environnements Adobe Target sont déjà définis, vous pouvez les utiliser.

## Paramètres Adobe Audience Manager

Pour envoyer des données à Adobe Audience Manager, il suffit d’activer cette section. Les autres paramètres sont facultatifs, mais encouragés.

![Bloc des paramètres d’Adobe Audience Manager](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Destinations de cookie activées]

Permet au SDK de partager des informations sur les segments via [Destinations de cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) de [!DNL Audience Manager].

### [!UICONTROL Destinations d’URL activées]

Permet au SDK de partager des informations sur les segments via [Destinations d’URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Ils sont configurés dans [!DNL Audience Manager].

## Paramètres Adobe Analytics

Contrôle si les données sont envoyées à Adobe Analytics. Pour plus d’informations, reportez-vous à la section [Présentation d’Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloc de paramètres Adobe Analytics](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL Identifiant de Report Suite]

La suite de rapports se trouve dans la section Admin d’Adobe Analytics sous [!UICONTROL Admin > ReportSuites]. Si plusieurs suites de rapports sont spécifiées, les données sont copiées dans chaque suite de rapports.
