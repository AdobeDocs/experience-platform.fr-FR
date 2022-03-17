---
keywords: mobile; le braquage; la messagerie;
title: Connexion de frein
description: Braze est une plateforme d’engagement client complète qui optimise les expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---

# [!DNL Braze] connection

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
| Type d&#39;export | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom) et/ou identités, en fonction du mappage de vos champs.[!DNL Adobe Experience Platform] les segments sont exportés vers [!DNL Braze] sous le `AdobeExperiencePlatformSegments` attribut. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Jeton de compte de frein]**: C&#39;est votre [!DNL Braze] [!DNL API] clé. Vous trouverez des instructions détaillées sur la manière d’obtenir votre [!DNL API] clé ici : [Présentation de la clé API REST](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Nom]**: saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: saisissez une description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Instance de point de fin]**: demandez votre [!DNL Braze] représente l’instance de point d’entrée que vous devez utiliser.

## Activation des segments vers cette destination {#activate}

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
| Identités | <ul><li>Email</code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID For Advertisers (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Le mappage correct se présente comme suit :

![Exemple de mappage de destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la variable [!DNL Braze] destination, vérifiez votre [!DNL Braze] compte . [!DNL Adobe Experience Platform] les segments sont exportés vers [!DNL Braze] sous le `AdobeExperiencePlatformSegments` attribut.

## Utilisation et gouvernance des données {#data-usage-governance}

Tous [!DNL Adobe Experience Platform] Les destinations sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](../../../data-governance/home.md).
