---
keywords: mobile; le braquage; la messagerie;
title: Connexion Braze
description: Braze est une plateforme d’engagement client complète qui optimise les expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 8%

---

# Connexion [!DNL Braze]

## Présentation {#overview}

Le [!DNL Braze] la destination vous aide à envoyer des données de profil à [!DNL Braze].

[!DNL Braze] est une plateforme d’engagement client exhaustive qui optimise les expériences pertinentes et mémorisables entre les clients et les marques qu’ils aiment.

Pour envoyer des données de profil à [!DNL Braze], vous devez d’abord vous connecter à la destination.

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques à la variable [!DNL Braze] destination :

* [!DNL Adobe Experience Platform] les segments sont exportés vers [!DNL Braze] sous le `AdobeExperiencePlatformSegments` attribut.

>[!NOTE]
>
>Gardez à l’esprit que l’envoi d’attributs personnalisés supplémentaires à [!DNL Braze] peut entraîner des augmentations de vos [!DNL Braze] consommation des points de données. Veuillez consulter votre [!DNL Braze] gestionnaire de compte avant d’envoyer des attributs personnalisés supplémentaires.

## Cas dʼutilisation {#use-cases}

En tant que marketeur, je souhaite cibler les utilisateurs dans une destination d’engagement mobile, avec des segments intégrés à [!DNL Adobe Experience Platform]. En outre, je souhaite leur proposer des expériences personnalisées, en fonction des attributs de leur [!DNL Adobe Experience Platform] profils, dès que les segments et les profils sont mis à jour dans [!DNL Adobe Experience Platform].

## Identités prises en charge {#supported-identities}

[!DNL Braze] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| external_id | Personnalisé [!DNL Braze] identifiant qui prend en charge le mappage de n’importe quelle identité. | Vous pouvez envoyer n’importe quel [identité](../../../identity-service/namespaces.md) au [!DNL Braze] tant que vous le mappez à la variable [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom) et/ou identités, en fonction du mappage de vos champs.[!DNL Adobe Experience Platform] les segments sont exportés vers [!DNL Braze] sous le `AdobeExperiencePlatformSegments` attribut. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Authentification à la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Jeton de compte de frein]**: C&#39;est votre [!DNL Braze] [!DNL API] clé. Vous trouverez des instructions détaillées sur la manière d’obtenir votre [!DNL API] clé ici : [Présentation de la clé API REST](https://www.braze.com/docs/api/api_key/).

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]**: saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: saisissez une description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Instance de point de fin]**: demandez votre [!DNL Braze] représente l’instance de point d’entrée que vous devez utiliser.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur l’état du flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur les [abonnement aux alertes de destinations à l’aide de l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de fournir des détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de segments par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

Pour envoyer correctement les données de votre audience à partir de [!DNL Adobe Experience Platform] au [!DNL Braze] destination, vous devez passer par l’étape de mappage des champs.

Le mappage consiste à créer un lien entre votre [!DNL Experience Data Model] Champs de schéma (XDM) dans votre [!DNL Platform] et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM à [!DNL Braze] champs de destination, procédez comme suit :

Dans le [!UICONTROL Mappage] étape, cliquez sur **[!UICONTROL Ajouter un nouveau mappage]**.

![Mappage de l’ajout de la destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping.png)

Dans le [!UICONTROL Champ source] , cliquez sur la flèche située en regard du champ vide.

![Mappage de la source de destination du braquage](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Dans le [!UICONTROL Sélectionner le champ source] vous pouvez choisir entre deux catégories de champs XDM :
* [!UICONTROL Sélectionner des attributs]: utilisez cette option pour mapper un champ spécifique de votre schéma XDM à un [!DNL Braze] attribut.

![Attribut source de mappage de destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Sélectionner un espace de noms d’identité]: Utilisez cette option pour mapper une [!DNL Platform] espace de noms d’identité en un [!DNL Braze] espace de noms.

![Espace de noms source du mapping de destination de la suppression](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Sélectionnez votre champ source, puis cliquez sur **[!UICONTROL Sélectionner]**.

Dans le [!UICONTROL Champ cible] , cliquez sur l’icône de mappage située à droite du champ.

![Mappage cible de la destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Dans le [!UICONTROL Sélectionner le champ cible] , vous pouvez choisir entre deux catégories de champs cibles :
* [!UICONTROL Sélectionner un espace de noms d’identité]: Utiliser cette option pour mapper [!DNL Platform] espaces de noms d’identité vers [!DNL Braze] espaces de noms d’identité.
* [!UICONTROL Sélectionner des attributs personnalisés]: Utilisez cette option pour mapper des attributs XDM à des attributs personnalisés [!DNL Braze] attributs que vous avez définis dans votre [!DNL Braze] compte . <br> Vous pouvez également utiliser cette option pour renommer les attributs XDM existants en [!DNL Braze]. Par exemple, le mappage d’un `lastName` Attribut XDM à un `Last_Name` dans [!DNL Braze], crée la variable `Last_Name` dans [!DNL Braze], s’il n’existe pas déjà, et mappez la variable `lastName` Attribut XDM à celui-ci.

![Braquer les champs de mappage cible de destination](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Sélectionnez votre champ cible, puis cliquez sur **[!UICONTROL Sélectionner]**.

Vous devriez maintenant voir votre mappage de champ dans la liste.

![Mappage de destination du bloc terminé](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Pour ajouter d’autres mappages, répétez les étapes précédentes.

## Exemple de mappage {#mapping-example}

Supposons que votre schéma de profil XDM et votre [!DNL Braze] contiennent les attributs et identités suivants :

|  | Schéma de profil XDM | [!DNL Braze] Instance |
|---|---|---|
| Attributs | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identités | <ul><li>E-mail</code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID For Advertisers (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Le mappage correct se présente comme suit :

![Exemple de mappage de destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la variable [!DNL Braze] destination, vérifiez votre [!DNL Braze] compte . [!DNL Adobe Experience Platform] les segments sont exportés vers [!DNL Braze] sous le `AdobeExperiencePlatformSegments` attribut.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](../../../data-governance/home.md).
