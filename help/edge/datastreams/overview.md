---
title: Présentation des flux de données
description: Connectez votre intégration SDK Experience Platform côté client à des produits Adobe et à des destinations tierces.
keywords: configuration;jeux de données;datastreamId;edge;datastream id;paramètres d’environnement;edgeConfigId;identité;synchronisation des identifiants activée;ID de conteneur de synchronisation;sandbox;flux de données;jeu de données d’événement;cible;code client;jeton de propriété;ID d’environnement cible;destinations de cookie;destinations d’URL;ID de suite de rapports de paramètres Analytics;prépréparation des données p;Mapper;XDM Mapper;Mapper sur Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: fe66cbd61d546da8fb6621ef78b3565126cb193d
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 3%

---

# Présentation des flux de données

Un flux de données représente la configuration côté serveur lors de l’implémentation des SDK Web et Mobile Adobe Experience Platform. Lorsque la variable [configuration, commande](../fundamentals/configuring-the-sdk.md) dans le SDK contrôle les éléments qui doivent être gérés sur le client (comme la variable `edgeDomain`), les flux de données gèrent toutes les autres configurations pour le SDK. Lorsqu’une demande est envoyée au réseau Edge Adobe Experience Platform, la variable `edgeConfigId` est utilisé pour référencer le flux de données. Cela vous permet de mettre à jour la configuration côté serveur sans avoir à modifier le code de votre site web.

Ce document décrit les étapes de configuration d’un flux de données dans l’interface utilisateur de la collecte de données.

>[!NOTE]
>
>Votre entreprise doit être configurée pour cette fonctionnalité afin d’y accéder dans l’interface utilisateur. Veuillez remplir les champs suivants : [formulaire](https://adobe.ly/websdkaccess) pour demander l’accès nécessaire. Pour gérer les flux de données, votre compte utilisateur doit être ajouté à un profil de produit pour les balises dans [!DNL Adobe Experience Platform].

## Accédez au [!UICONTROL Datastreams] workspace

Vous pouvez créer et gérer des flux de données dans l’interface utilisateur de la collecte de données en sélectionnant **[!UICONTROL Datastreams]** dans le volet de navigation de gauche.

![Onglet Flux de données dans l’interface utilisateur de la collecte de données](../images/datastreams/overview/datastreams-tab.png)

Le [!UICONTROL Datastreams] affiche une liste des flux de données existants, y compris leur nom convivial, leur identifiant et leur date de dernière modification. Sélectionnez le nom d’un flux de données sur [afficher ses détails et configurer des services ;](#view-details).

Sélectionnez l’icône &quot;plus&quot; (**...**) pour un flux de données spécifique afin d’afficher plus d’options. Sélectionner **[!UICONTROL Modifier]** pour mettre à jour la variable [configuration de base](#configure) pour le flux de données, ou sélectionnez **[!UICONTROL Supprimer]** pour supprimer le flux de données.

![Options de modification ou de suppression et flux de données existant](../images/datastreams/overview/edit-datastream.png)

## Création d’un flux de données {#create}

Pour créer un flux de données, commencez par sélectionner **[!UICONTROL Nouvelle structure de données]**.

![Sélectionner un nouveau flux de données](../images/datastreams/overview/new-datastream-button.png)

Le workflow de création de la chaîne de données s’affiche, en commençant à l’étape de configuration. À partir de là, vous devez fournir un nom et une description facultative pour le flux de données.

Si vous configurez ce flux de données à utiliser dans Experience Platform et que vous utilisez le SDK Web Platform, vous devez également sélectionner une [schéma XDM (Experience Data Model) basé sur un événement](../../xdm/classes/experienceevent.md) pour représenter les données que vous prévoyez d’ingérer.

![Configuration de base pour un flux de données](../images/datastreams/overview/configure.png)

Sélectionner **[!UICONTROL Options avancées]** pour afficher des contrôles supplémentaires pour configurer le flux de données.

![Options de configuration avancées](../images/datastreams/overview/advanced-options.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Emplacement géographique] | Détermine si des recherches GPS se produisent en fonction de l’adresse IP de l’utilisateur. Le paramètre par défaut **[!UICONTROL Aucun]** désactive les recherches GPS, tandis que la variable **[!UICONTROL Ville]** fournit les coordonnées GPS à deux décimales. |
| [!UICONTROL Cookie d’identifiant propriétaire] | Lorsqu’il est activé, ce paramètre indique au réseau Edge de faire référence à un cookie spécifié lors de la recherche d’un [identifiant d’appareil propriétaire](../identity/first-party-device-ids.md), plutôt que de rechercher cette valeur dans la carte des identités.<br><br>Lors de l’activation de ce paramètre, vous devez indiquer le nom du cookie dans lequel l’ID doit être stocké. |
| [!UICONTROL Synchronisation des identifiants tiers] | Les synchronisations des identifiants peuvent être regroupées en conteneurs afin de permettre l’exécution de différentes synchronisations des identifiants à différents moments. Lorsqu’il est activé, ce paramètre vous permet de spécifier le conteneur des synchronisations des identifiants à exécuter pour ce flux de données. |

À partir de là, si vous configurez votre flux de données pour Experience Platform, suivez le tutoriel sur [Préparation de données pour la collecte de données](./data-prep.md) pour mapper vos données à un schéma d’événement Platform avant de revenir à ce guide. Sinon, sélectionnez **[!UICONTROL Enregistrer]** et passez à la section suivante.

## Affichage des détails d’un flux de données {#view-details}

Après avoir configuré un nouveau flux de données ou sélectionné un flux existant à afficher, la page de détails de ce flux de données s’affiche. Vous trouverez ici des informations supplémentaires sur la banque de données, y compris son identifiant.

![Page de détails d’un flux de données créé](../images/datastreams/overview/view-details.png)

À partir de l’écran des détails de la chaîne de données, vous pouvez [ajouter des services](#add-services) pour activer les fonctionnalités des produits Adobe Experience Cloud auxquels vous avez accès. Vous pouvez également modifier le [configuration de base](#create), mettre à jour ses [règles de mappage](./data-prep.md), [copier le flux de données](#copy)ou supprimez-le entièrement.

## Ajout de services à un flux de données {#add-services}

Sur la page de détails d’une banque de données, sélectionnez **[!UICONTROL Ajouter un service]** pour commencer à ajouter les services disponibles pour ce flux de données.

![Sélectionnez Ajouter un service pour continuer](../images/datastreams/overview/add-service.png)

Sur l’écran suivant, utilisez le menu déroulant pour sélectionner un service à configurer pour cette banque de données. Seuls les services auxquels vous avez accès apparaîtront dans cette liste.

![Sélectionner un service dans la liste](../images/datastreams/overview/service-selection.png)

Sélectionnez le service souhaité, renseignez les options de configuration qui s’affichent, puis sélectionnez **[!UICONTROL Enregistrer]** pour ajouter le service au flux de données. Tous les services ajoutés s’affichent dans la vue Détails de la banque de données.

![Services ajoutés à un flux de données](../images/datastreams/overview/services-added.png)

Les sous-sections ci-dessous décrivent les options de configuration de chaque service.

>[!NOTE]
>
>Chaque configuration de service contient une **[!UICONTROL Activé]** bascule qui est automatiquement activé lorsque le service est sélectionné. Pour désactiver le service sélectionné pour ce flux de données, sélectionnez l’option **[!UICONTROL Activé]** basculez à nouveau.

### Paramètres Adobe Analytics

Ce service contrôle si et comment les données sont envoyées à Adobe Analytics. Vous trouverez des informations supplémentaires dans le guide sur la [envoi de données à Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloc de paramètres Adobe Analytics](../images/datastreams/overview/analytics-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Identifiant de Report Suite] | **(Obligatoire)** Identifiant de la suite de rapports Analytics à laquelle vous souhaitez envoyer des données. Cet identifiant se trouve dans l’interface utilisateur d’Adobe Analytics sous [!UICONTROL Administration] > [!UICONTROL ReportSuites]. Si plusieurs suites de rapports sont spécifiées, les données sont copiées dans chaque suite de rapports. |

### Paramètres Adobe Audience Manager

Ce service contrôle si et comment les données sont envoyées à Adobe Audience Manager. Pour envoyer des données à Audience Manager, il suffit d’activer cette section. Les autres paramètres sont facultatifs, mais encouragés.

![Bloc des paramètres d’Adobe Audience Manager](../images/datastreams/overview/audience-manager-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Destinations de cookie activées] | Permet au SDK de partager des informations sur les segments via [destinations de cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) de [!DNL Audience Manager]. |
| [!UICONTROL Destinations d’URL activées] | Permet au SDK de partager des informations sur les segments via [Destinations d’URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) de [!DNL Audience Manager]. |

### Paramètres d’Adobe Experience Platform

>[!IMPORTANT]
>
>Lors de l’activation d’un flux de données pour Platform, prenez note de l’environnement de test Platform que vous utilisez actuellement, tel qu’affiché dans le ruban supérieur de l’interface utilisateur de la collecte de données.
>
>![Environnement de test sélectionné](../images/datastreams/overview/platform-sandbox.png)
>
>Les environnements de test sont des partitions virtuelles dans Adobe Experience Platform qui vous permettent d’isoler vos données et implémentations des autres membres de votre organisation. Une fois un flux de données créé, son environnement de test ne peut plus être modifié. Pour plus d’informations sur le rôle des environnements de test dans Experience Platform, voir [documentation des environnements de test](../../sandboxes/home.md).

Ce service contrôle si et comment les données sont envoyées à Adobe Experience Platform.

![Bloc de paramètres Adobe Experience Platform](../images/datastreams/overview/platform-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Jeu de données d’événement] | **(Obligatoire)** Sélectionnez le jeu de données Platform vers lequel les données d’événement client seront diffusées. Ce schéma doit utiliser la variable [Classe XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Jeu de données de profil] | Sélectionnez le jeu de données Platform auquel les données d’attributs du client seront envoyées. Ce schéma doit utiliser la variable [Classe XDM Individual Profile](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Cochez cette case pour activer l’Offer decisioning pour une mise en oeuvre du SDK Web Platform. Consultez le guide sur la [utilisation de l’Offer decisioning avec le SDK Web Platform](../personalization/offer-decisioning/offer-decisioning-overview.md) pour plus d’informations sur l’implémentation. Pour plus d’informations sur les fonctionnalités d’Offer decisioning, reportez-vous à la section [Documentation Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=fr). |
| [!UICONTROL Segmentation Edge] | Cochez cette case pour activer [segmentation de périphérie](../../segmentation/ui/edge-segmentation.md) pour ce flux de données. Lorsque le SDK envoie des données par le biais d’un flux de données activé pour la segmentation Edge, toutes les adhésions de segment mises à jour pour le profil en question sont renvoyées dans la réponse.<br><br>Cette option peut être utilisée conjointement avec [!UICONTROL Destinations de personnalisation] pour [Cas d’utilisation de la personnalisation de la page suivante](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinations de personnalisation] | Utilisé en combinaison avec la propriété [!UICONTROL Segmentation Edge] , cette option permet à la banque de données de se connecter à des moteurs de personnalisation tels qu’Adobe Target. Reportez-vous à la documentation des destinations pour obtenir des instructions spécifiques sur [configuration des destinations de personnalisation](../../destinations/ui/configure-personalization-destinations.md). |

### Paramètres Adobe Target {#target}

Ce service contrôle si et comment les données sont envoyées à Adobe Target.

![Bloc de paramètres Adobe Target](../images/datastreams/overview/target-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Jeton de propriété] | [!DNL Target] permet aux clients de contrôler les autorisations par l’utilisation des propriétés. Pour plus d’informations sur les propriétés, consultez le guide sur [configuration des autorisations d’entreprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=fr) dans le [!DNL Target] documentation.<br><br>Le jeton de propriété se trouve dans l’interface utilisateur d’Adobe Target sous [!UICONTROL Configuration] > [!UICONTROL Propriétés]. |
| [!UICONTROL Identifiant d’environnement de Target] | [Environnements dans Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) vous aider à gérer votre mise en oeuvre à toutes les étapes de développement. Ce paramètre spécifie l’environnement que vous allez utiliser avec ce flux de données.<br><br>La bonne pratique consiste à définir cela différemment pour chacun de vos `dev`, `stage`, et `prod` des environnements de flux de données pour simplifier les choses. Cependant, si des environnements Adobe Target sont déjà définis, vous pouvez les utiliser. |
| [!UICONTROL Espace de noms d’ID tiers de Target] | L’espace de noms d’identité pour la variable `mbox3rdPartyId` vous souhaitez utiliser pour ce flux de données. Consultez le guide sur la [implémentation `mbox3rdPartyId` avec le SDK Web](../personalization/adobe-target/using-mbox-3rdpartyid.md) pour plus d’informations. |

### [!UICONTROL Transfert d’événement] paramètres

Ce service contrôle si et comment les données sont envoyées à [transfert d’événement](../../tags/ui/event-forwarding/overview.md).

![Section Transfert d’événement de l’interface utilisateur de configuration](../images/datastreams/overview/event-forwarding-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Propriété Launch] | **(Obligatoire)** La propriété de transfert d’événement à laquelle vous souhaitez envoyer des données. |
| [!UICONTROL Environnement de lancement] | **(Obligatoire)** Environnement au sein de la propriété sélectionnée auquel vous souhaitez envoyer des données. |

>[!NOTE]
>
>Vous pouvez sélectionner **[!UICONTROL Saisie manuelle des identifiants]** pour saisir les noms des propriétés et des environnements au lieu d’utiliser les menus déroulants.

## Copie d’un flux de données {#copy}

Vous pouvez créer une copie d’un flux de données existant et en modifier les détails si nécessaire.

>[!NOTE]
>
>Les flux de données ne peuvent être copiés que dans le même [sandbox](../../sandboxes/home.md). En d’autres termes, vous ne pouvez pas copier un flux de données d’un environnement de test vers un autre.

À partir de la page principale de la [!UICONTROL Datastreams] espace de travail, sélectionnez les points de suspension (**....**) pour le flux de données en question, puis sélectionnez **[!UICONTROL Copier]**.

![Image montrant le [!UICONTROL Copier] l’option sélectionnée dans la vue de liste du flux de données](../images/datastreams/overview/copy-datastream-list.png)

Vous pouvez également sélectionner **[!UICONTROL Copier le flux de données]** dans la vue détails d’un flux de données donné.

![Image montrant le [!UICONTROL Copier] l’option étant sélectionnée dans la vue détails de la chaîne de données](../images/datastreams/overview/copy-datastream-details.png)

Une boîte de dialogue de confirmation s’affiche, vous invitant à fournir un nom unique pour la création de la nouvelle banque de données, ainsi que des détails sur les options de configuration qui seront copiées. Une fois prêt, sélectionnez **[!UICONTROL Copier]**.

![Image de la boîte de dialogue de confirmation pour la copie d’un flux de données](../images/datastreams/overview/copy-datastream-confirm.png)

La page principale de [!UICONTROL Datastreams] workspace réapparaît avec le nouveau flux de données répertorié.

## Étapes suivantes

Ce guide explique comment gérer les flux de données dans l’interface utilisateur de la collecte de données. Pour plus d’informations sur l’installation et la configuration du SDK Web après la configuration d’un flux de données, reportez-vous à la section [Guide de collecte de données E2E](../../collection/e2e.md#install).
