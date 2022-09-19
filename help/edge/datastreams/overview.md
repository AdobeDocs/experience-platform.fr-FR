---
title: Présentation des flux de données
description: Connectez votre intégration SDK Experience Platform côté client à des produits Adobe et à des destinations tierces.
keywords: configuration;flux de données;datastreamId;edge;identifiant de flux de données;Paramètres d’environnement;edgeConfigId;identité;synchronisation des identifiants activée;Identifiant de conteneur de synchronisation d’identifiant;Sandbox;Diffusion d’entrée;Jeu de données d’événement;cible;code client;Jeton de propriété;Identifiant d’environnement cible;Destinations de cookie;Destinations d’url;identifiant de suite de rapports de blocs de paramètres Analytics;Préparation des données pour la collecte de données;Préparation des données;Mappeur;Mappeur XDM;Mappeur sur Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 3690a32f32c6cfa25120e9af44fe559122e779a0
workflow-type: tm+mt
source-wordcount: '1729'
ht-degree: 100%

---

# Présentation des flux de données

Un flux de données représente la configuration côté serveur lors de la mise en œuvre des SDK web et mobile d’Adobe Experience Platform. Lorsque la [commande de configuration](../fundamentals/configuring-the-sdk.md) dans le SDK contrôle les éléments qui doivent être gérés sur le client (comme `edgeDomain`), les flux de données gèrent toutes les autres configurations pour le SDK. Lorsqu’une requête est envoyée à Adobe Experience Platform Edge Network, `edgeConfigId` est utilisé pour référencer le flux de données. Cela vous permet de mettre à jour la configuration côté serveur sans devoir modifier le code du site web.

Ce document décrit les étapes de configuration d’un flux de données dans l’interface utilisateur de collecte de données.

## Accéder à l’espace de travail [!UICONTROL Flux de données]

Vous pouvez créer et gérer des flux de données dans l’interface utilisateur de collecte de données en sélectionnant **[!UICONTROL Flux de données]** dans le volet de navigation de gauche.

![Onglet Flux de données dans l’interface utilisateur de collecte de données](../images/datastreams/overview/datastreams-tab.png)

L’onglet [!UICONTROL Flux de données] affiche une liste des flux de données existants, y compris leur nom convivial, leur identifiant et leur date de dernière modification. Sélectionnez le nom d’un flux de données pour [afficher les détails et configurer des services](#view-details).

Sélectionnez l’icône « plus » (**…**) d’un flux de données spécifique afin d’afficher plus d’options. Sélectionnez **[!UICONTROL Modifier]** pour mettre à jour la [configuration de base](#configure) du flux de données ou sélectionnez **[!UICONTROL Supprimer]** pour supprimer le flux de données.

![Options de modification ou de suppression d’un flux de données existant](../images/datastreams/overview/edit-datastream.png)

## Créer un flux de données {#create}

Pour créer un flux de données, commencez par sélectionner **[!UICONTROL Nouveau flux de données]**.

![Sélectionner un nouveau flux de données](../images/datastreams/overview/new-datastream-button.png)

Le processus de création du flux de données s’affiche, en commençant à l’étape de configuration. Ensuite, vous devez fournir un nom et une description facultative pour le flux de données.

Si vous configurez ce flux de données pour l’utiliser dans Experience Platform et que vous utilisez le SDK web de Platform, vous devez également sélectionner un [schéma de modèle de données d’expérience (XDM) basé sur un événement](../../xdm/classes/experienceevent.md) pour représenter les données que vous prévoyez d’ingérer.

![Configuration de base d’un flux de données](../images/datastreams/overview/configure.png)

Sélectionnez **[!UICONTROL Options avancées]** pour afficher des commandes supplémentaires permettant de configurer le flux de données.

![Options de configuration avancées](../images/datastreams/overview/advanced-options.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Géolocalisation] | Détermine si les recherches GPS sont effectuées en fonction de l’adresse IP de l’utilisateur. Le paramètre par défaut **[!UICONTROL Aucun]** désactive les recherches GPS, tandis que le paramètre **[!UICONTROL Ville]** fournit les coordonnées GPS à deux décimales. |
| [!UICONTROL Cookie interne d’identifiant] | Lorsqu’il est activé, ce paramètre indique à Edge Network de se référer à un cookie spécifié lors de la recherche d’un [identifiant d’appareil interne](../identity/first-party-device-ids.md), plutôt que de rechercher cette valeur dans le mappage d’identité.<br><br>Lors de l’activation de ce paramètre, vous devez indiquer le nom du cookie dans lequel l’identifiant doit être stocké. |
| [!UICONTROL Synchronisation des identifiants tiers] | Les synchronisations des identifiants peuvent être regroupées en conteneurs afin de permettre l’exécution de différentes synchronisations d’identifiant à différents moments. Lorsqu’il est activé, ce paramètre vous permet de spécifier le conteneur des synchronisations d’identifiant à exécuter pour ce flux de données. |
| [!UICONTROL Type d’accès] | Définit le type d’authentification que le [!DNL Edge Network] accepte pour le train de données. <ul><li>**[!UICONTROL Authentification mixte]** : lorsque cette option est activée, Edge Network accepte les demandes authentifiées et non authentifiées. Sélectionnez cette option lorsque vous prévoyez d’utiliser le SDK web ou le [SDK mobile](https://aep-sdks.gitbook.io/docs/), ainsi que l’[API Server](../../server-api/overview.md). </li><li>**[!UICONTROL Authentifié uniquement]** : lorsque cette option est activée, Edge Network accepte uniquement les demandes authentifiées. Sélectionnez cette option lorsque vous prévoyez d’utiliser uniquement l’API Server et que vous souhaitez empêcher le traitement des demandes non authentifiées par le [!DNL Edge Network]. </li></ul> |

Ensuite, si vous configurez le flux de données d’Experience Platform, suivez le tutoriel sur la [Préparation des données pour la collecte de données](./data-prep.md) afin de mapper les données à un schéma d’événement de Platform avant de revenir à ce guide. Sinon, sélectionnez **[!UICONTROL Enregistrer]** et passez à la section suivante.

## Afficher les détails d’un flux de données {#view-details}

Après avoir configuré un nouveau flux de données ou sélectionné un flux de données existant à afficher, sa page de détails s’affiche. Vous y trouverez des informations supplémentaires sur le flux de données, y compris son identifiant.

![Page de détails d’un flux de données créé](../images/datastreams/overview/view-details.png)

À partir de l’écran de détails du flux de données, vous pouvez [ajouter des services](#add-services) pour activer les fonctionnalités des produits Adobe Experience Cloud auxquels vous avez accès. Vous pouvez également modifier la [configuration de base](#create) du flux de données, mettre à jour ses [règles de mappage](./data-prep.md), [copier le flux de données](#copy) ou le supprimer entièrement.

## Ajouter des services à un flux de données {#add-services}

Sur la page de détails d’un flux de données, sélectionnez **[!UICONTROL Ajouter un service]** pour commencer à ajouter les services disponibles à ce flux de données.

![Sélectionner Ajouter un service pour continuer](../images/datastreams/overview/add-service.png)

Sur l’écran suivant, utilisez le menu déroulant pour sélectionner un service à configurer pour ce flux de données. Seuls les services auxquels vous avez accès apparaissent dans cette liste.

![Sélectionner un service dans la liste](../images/datastreams/overview/service-selection.png)

Sélectionnez le service souhaité, renseignez les options de configuration qui s’affichent, puis sélectionnez **[!UICONTROL Enregistrer]** pour ajouter le service au flux de données. Tous les services ajoutés s’affichent dans la vue des détails du flux de données.

![Services ajoutés à un flux de données](../images/datastreams/overview/services-added.png)

Les sous-sections ci-dessous décrivent les options de configuration de chaque service.

>[!NOTE]
>
>Chaque configuration de service contient un bouton **[!UICONTROL Activer]** qui est automatiquement activé lorsque le service est sélectionné. Pour désactiver le service sélectionné de ce flux de données, sélectionnez à nouveau le bouton **[!UICONTROL Activer]**.

### Paramètres d’Adobe Analytics {#analytics}

Ce service contrôle si et comment les données sont envoyées à Adobe Analytics. Vous trouverez des informations supplémentaires dans le guide sur l’[envoi de données à Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Bloc de paramètres d’Adobe Analytics](../images/datastreams/overview/analytics-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Identifiant de suite de rapports] | **(Obligatoire)** L’identifiant de la suite de rapports Analytics à laquelle vous souhaitez envoyer des données. Cet identifiant se trouve dans l’interface utilisateur d’Adobe Analytics sous [!UICONTROL Administration] > [!UICONTROL Suites de rapports]. Si plusieurs suites de rapports sont spécifiées, les données sont copiées dans chaque suite de rapports. |

### Paramètres d’Adobe Audience Manager {#audience-manager}

Ce service contrôle si et comment les données sont envoyées à Adobe Audience Manager. Il suffit d’activer cette section pour envoyer des données à Audience Manager. Les autres paramètres sont facultatifs, mais recommandés.

![Bloc de paramètres d’Adobe Audience Manager](../images/datastreams/overview/audience-manager-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Destinations de cookie activées] | Permet au SDK de partager des informations sur les segments via les [destinations de cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html?lang=fr) d’[!DNL Audience Manager]. |
| [!UICONTROL Destinations d’URL activées] | Permet au SDK de partager des informations sur les segments via les [destinations d’URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html?lang=fr) d’[!DNL Audience Manager]. |

### Paramètres d’Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Lors de l’activation d’un flux de données pour Platform, notez le sandbox de Platform que vous utilisez actuellement, tel qu’affiché dans le ruban supérieur de l’interface utilisateur de collecte de données.
>
>![Sandbox sélectionné](../images/datastreams/overview/platform-sandbox.png)
>
>Les sandbox sont des partitions virtuelles dans Adobe Experience Platform qui vous permettent d’isoler les données et mises en œuvre des autres membres de l’organisation. Une fois un flux de données créé, le sandbox ne peut plus être modifié. Pour plus d’informations sur le rôle des sandbox dans Experience Platform, consultez la [documentation sur les sandbox](../../sandboxes/home.md).

Ce service contrôle si et comment les données sont envoyées à Adobe Experience Platform.

![Bloc de paramètres d’Adobe Experience Platform](../images/datastreams/overview/platform-config.png)

| Paramètre | Description |
|---| --- |
| [!UICONTROL Jeu de données d’événement] | **(Obligatoire)** Sélectionnez le jeu de données de Platform vers lequel les données d’événement client seront diffusées. Ce schéma doit utiliser la [classe XDM ExperienceEvent](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Jeu de données de profil] | Sélectionnez le jeu de données de Platform auquel les données d’attribut du client seront envoyées. Ce schéma doit utiliser la [classe XDM Individual Profile](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Cochez cette case pour activer Offer Decisioning pour une mise en œuvre du SDK web de Platform. Consultez le guide sur l’[utilisation d’Offer Decisioning avec le SDK web de Platform](../personalization/offer-decisioning/offer-decisioning-overview.md) pour plus d’informations sur la mise en œuvre. Pour plus d’informations sur les fonctionnalités d’Offer Decisioning, consultez la [Documentation d’Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=fr). |
| [!UICONTROL Segmentation Edge] | Cochez cette case pour activer la [segmentation Edge](../../segmentation/ui/edge-segmentation.md) de ce flux de données. Lorsque le SDK envoie des données par le biais d’un flux de données compatible avec la segmentation Edge, toutes les adhésions au segment mises à jour pour le profil en question sont renvoyées dans la réponse.<br><br>Cette option peut être utilisée conjointement avec [!UICONTROL Destinations de personnalisation] pour les [cas d’utilisation de la personnalisation de page suivante](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinations de personnalisation] | Lorsque vous activez cette fonction après avoir activé la case à cocher [!UICONTROL Segmentation Edge], cette option permet au flux de données de se connecter aux destinations de personnalisation, telles que [Personnalisation personnalisée](../../destinations/catalog/personalization/custom-personalization.md). Consultez la documentation des destinations pour obtenir des instructions spécifiques sur la [configuration des destinations de personnalisation](../../destinations/ui/configure-personalization-destinations.md). |

### Paramètres d’Adobe Target {#target}

Ce service contrôle si et comment les données sont envoyées à Adobe Target.

![Bloc de paramètres d’Adobe Target](../images/datastreams/overview/target-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Jeton de propriété] | [!DNL Target] permet aux clients de contrôler les autorisations par l’utilisation des propriétés. Pour plus d’informations sur les propriétés, consultez le guide sur la [configuration des autorisations d’entreprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=fr) dans la documentation de [!DNL Target].<br><br>Le jeton de propriété se trouve dans l’interface utilisateur d’Adobe Target sous [!UICONTROL Configuration] > [!UICONTROL Propriétés]. |
| [!UICONTROL Identifiant d’environnement Target] | Les [environnements dans Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=fr) vous permettent de gérer la mise en œuvre à toutes les étapes de développement. Ce paramètre spécifie l’environnement que vous allez utiliser avec ce flux de données.<br><br>Une bonne pratique consiste à définir ce paramètre différemment pour chacun des environnements de flux de données `dev`, `stage` et `prod` afin de simplifier le processus. Cependant, si des environnements Adobe Target sont déjà définis, vous pouvez les utiliser. |
| [!UICONTROL Espace de noms d’identifiant tiers de Target] | L’espace de noms d’identité du `mbox3rdPartyId` que vous souhaitez utiliser pour ce flux de données. Pour plus d’informations, consultez le guide sur la [mise en œuvre de `mbox3rdPartyId` avec le SDK web](../personalization/adobe-target/using-mbox-3rdpartyid.md). |

### Paramètres [!UICONTROL Transfert d’événement]

Ce service contrôle si et comment les données sont envoyées au [transfert d’événement](../../tags/ui/event-forwarding/overview.md).

![Section Transfert d’événement de l’interface utilisateur de configuration](../images/datastreams/overview/event-forwarding-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Propriété de Launch] | **(Obligatoire)** La propriété de transfert d’événement à laquelle vous souhaitez envoyer des données. |
| [!UICONTROL Environnement Launch] | **(Obligatoire)** L’environnement au sein de la propriété sélectionnée auquel vous souhaitez envoyer des données. |

>[!NOTE]
>
>Vous pouvez sélectionner **[!UICONTROL Saisie manuelle des identifiants]** pour saisir les noms des propriétés et des environnements au lieu d’utiliser les menus déroulants.

## Copier un flux de données {#copy}

Vous pouvez créer une copie d’un flux de données existant et en modifier les détails si nécessaire.

>[!NOTE]
>
>Les flux de données peuvent uniquement être copiés dans le même [sandbox](../../sandboxes/home.md). En d’autres termes, vous ne pouvez pas copier un flux de données d’un sandbox vers un autre.

À partir de la page principale de l’espace de travail [!UICONTROL Flux de données], sélectionnez les points de suspension (**....**) pour le flux de données en question, puis sélectionnez **[!UICONTROL Copier]**.

![Image illustrant l’option [!UICONTROL Copier] sélectionnée dans la vue de liste du flux de données](../images/datastreams/overview/copy-datastream-list.png).

Vous pouvez également sélectionner **[!UICONTROL Copier le flux de données]** dans la vue des détails d’un flux de données particulier.

![Image illustrant l’option [!UICONTROL Copier] sélectionnée dans la vue des détails du flux de données](../images/datastreams/overview/copy-datastream-details.png).

Une boîte de dialogue de confirmation s’affiche, vous invitant à fournir un nom unique pour la création du flux de données, ainsi que des détails sur les options de configuration qui seront copiées. Une fois prêt, sélectionnez **[!UICONTROL Copier]**.

![Image de la boîte de dialogue de confirmation pour la copie d’un flux de données](../images/datastreams/overview/copy-datastream-confirm.png)

La page principale de l’espace de travail [!UICONTROL Flux de données] réapparaît avec le nouveau flux de données répertorié.

## Étapes suivantes

Ce guide explique comment gérer les flux de données dans l’interface utilisateur de collecte de données. Pour plus d’informations sur l’installation et la configuration du SDK web après la configuration d’un flux de données, consultez le [Guide E2E de collecte de données](../../collection/e2e.md#install).
