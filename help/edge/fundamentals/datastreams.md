---
title: Configuration du flux de données pour le SDK Web Experience Platform
description: 'Découvrez comment configurer les flux de données. '
keywords: configuration;datastreams;datastreamId;edge;datastream id;paramètres d’environnement;edgeConfigId;identité;synchronisation des identifiants activée;ID de conteneur de synchronisation;sandbox;flux de données;jeu de données d’événement;cible;code client;jeton de propriété;ID d’environnement cible;destinations de cookie;destinations d’URL;ID de suite de rapports de paramètres Analytics;ID de blocage
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 1%

---


# Configuration d’un flux de données

La configuration du SDK Web Adobe Experience Platform est fractionnée en deux endroits. La [commande configure](configuring-the-sdk.md) du SDK contrôle les éléments qui doivent être gérés sur le client, comme la balise `edgeDomain`. Les flux de données gèrent toutes les autres configurations pour le SDK. Lorsqu’une demande est envoyée au réseau Adobe Experience Platform Edge, la valeur `edgeConfigId` est utilisée pour référencer la configuration côté serveur. Cela vous permet de mettre à jour la configuration sans avoir à apporter de modifications au code sur votre site web.

Votre entreprise doit être configurée pour cette fonctionnalité. Veuillez contacter votre responsable du succès client pour qu’il soit mis en liste autorisée.

## Création d’une configuration de flux de données

Les flux de données peuvent être créés dans Adobe [!DNL Experience Platform Launch] à l’aide de l’outil de configuration Datastream .

![navigation de l’outil datastreams](../images/datastreams/config.png)

>[!NOTE]
>
>L’outil de configuration des flux de données est disponible pour les clients de la liste autorisée, qu’ils utilisent [!DNL Experience Platform Launch] comme gestionnaire de balises. En outre, les utilisateurs ont besoin des autorisations Développer dans [!DNL Experience Platform Launch]. Pour plus d’informations, reportez-vous à l’article [Autorisations utilisateur](../../tags/ui/administration/user-permissions.md) de la documentation [!DNL Experience Platform Launch] .

Créez un flux de données en cliquant sur **[!UICONTROL Nouvelle flux de données]** dans la zone supérieure droite de l’écran. Après avoir fourni un nom et une description, vous êtes invité à définir les paramètres par défaut de chaque environnement. Les paramètres disponibles sont présentés ci-dessous.

Lors de la création d’un flux de données, trois environnements sont automatiquement créés avec des paramètres identiques. Ces trois environnements sont *dev*, *stage* et *prod*. Ils correspondent aux trois environnements par défaut dans [!DNL Experience Platform Launch]. Lorsque vous créez une bibliothèque [!DNL Experience Platform Launch] dans un environnement de développement, la bibliothèque utilise automatiquement l’environnement de développement de votre configuration. Vous pouvez modifier les paramètres dans des environnements individuels autant que vous le souhaitez.

L’ID utilisé dans le SDK comme `edgeConfigId` est un ID composite qui spécifie la configuration et l’environnement (par exemple, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Si aucun environnement n’est présent dans l’ID composite (par exemple, `stage` dans l’exemple précédent), l’environnement de production est utilisé.

Vous trouverez ci-dessous les paramètres disponibles pour chaque environnement de configuration. La plupart des sections peuvent être activées ou désactivées. Lorsque cette option est désactivée, vos paramètres sont enregistrés, mais ne sont pas principaux.

## [!UICONTROL Paramètres ] IDSettings tiers

La section ID tiers est la seule section toujours active. Deux paramètres sont disponibles : &quot;[!UICONTROL Synchronisation des identifiants tiers activée]&quot; et &quot;[!UICONTROL ID de conteneur de synchronisation des identifiants tiers]&quot;.

![Section Identité de l’interface utilisateur de configuration](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Synchronisation des identifiants tiers activée]

Contrôle si le SDK effectue ou non des synchronisations d’identité avec des partenaires tiers.

### [!UICONTROL ID de conteneur de synchronisation des identifiants tiers]

Les synchronisations des identifiants peuvent être regroupées en conteneurs afin de permettre l’exécution de différentes synchronisations des identifiants à différents moments. Cela contrôle le conteneur des synchronisations des identifiants exécuté pour un identifiant de configuration donné.

## Paramètres Adobe Experience Platform

Les paramètres répertoriés ici vous permettent d’envoyer des données à Adobe Experience Platform. N’activez cette section que si vous avez acheté Adobe Experience Platform.

![Bloc de paramètres Adobe Experience Platform](../images/datastreams/edge_configuration_aep.png)

### [!UICONTROL Environnement de test]

Les environnements de test sont des emplacements dans Adobe Experience Platform qui permettent aux clients d’isoler leurs données et implémentations les uns des autres. Pour plus d’informations sur leur fonctionnement, consultez la [documentation des environnements de test](../../sandboxes/home.md).

### [!UICONTROL Inlet de diffusion en continu]

Un inlet de flux est une source HTTP dans Adobe Experience Platform. Elles sont créées sous l’onglet &quot;[!UICONTROL Sources]&quot; dans Adobe Experience Platform en tant qu’API HTTP.

### [!UICONTROL Jeu de données d’événement]

Les flux de données prennent en charge l’envoi de données à des jeux de données qui ont un schéma de classe [!UICONTROL Événement d’expérience].

## Paramètres Adobe Target

Pour configurer Adobe Target, vous devez fournir un code client. Les autres champs sont facultatifs.

![Bloc de paramètres Adobe Target](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>L’organisation associée au code client doit correspondre à l’organisation dans laquelle l’ID de configuration est créé.

### [!UICONTROL Code client]

Identifiant unique d’un compte cible. Pour le trouver, vous pouvez accéder à [!UICONTROL Adobe Target] > [!UICONTROL Configuration] [!UICONTROL Mise en oeuvre] > [!UICONTROL modifier les paramètres] en regard du bouton [!UICONTROL télécharger] pour [!UICONTROL at.js] ou &lt;a11 2/>mbox.js][!UICONTROL 

### [!UICONTROL Jeton de propriété]

[!DNL Target] permet aux clients de contrôler les autorisations par l’utilisation des propriétés. Vous trouverez des détails dans la section [Autorisations d’entreprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=fr) de la documentation [!DNL Target].

Le jeton de propriété se trouve dans [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Propriétés]

### [!UICONTROL Identifiant d’environnement de Target]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Les environnements d’Adobe Target vous aident à gérer votre mise en oeuvre à toutes les étapes de développement. Ce paramètre spécifie l’environnement que vous allez utiliser avec chaque environnement.

Adobe recommande de définir cela différemment pour chacun de vos environnements de flux de données `dev`, `stage` et `prod` afin de garder les choses simples. Cependant, si des environnements Adobe Target sont déjà définis, vous pouvez les utiliser.

## Paramètres Adobe Audience Manager

Pour envoyer des données à Adobe Audience Manager, il suffit d’activer cette section. Les autres paramètres sont facultatifs, mais encouragés.

![Bloc des paramètres d’Adobe Audience Manager](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Destinations de cookie activées]

Permet au SDK de partager des informations sur les segments via [les destinations de cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) à partir de [!DNL Audience Manager].

### [!UICONTROL Destinations d’URL activées]

Permet au SDK de partager les informations sur les segments via [les destinations d’URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Ils sont configurés dans [!DNL Audience Manager].

## Paramètres Adobe Analytics

Contrôle si les données sont envoyées à Adobe Analytics. Pour plus d’informations, reportez-vous à la section [Présentation d’Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloc de paramètres Adobe Analytics](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL Identifiant de Report Suite]

La suite de rapports se trouve dans la section Admin d’Adobe Analytics sous [!UICONTROL Admin > ReportSuites]. Si plusieurs suites de rapports sont spécifiées, les données sont copiées dans chaque suite de rapports.
