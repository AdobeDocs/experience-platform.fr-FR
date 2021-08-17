---
keywords: mobile; le braquage; la messagerie;
title: Connexion de frein
description: Braze est une plateforme d’engagement client complète qui optimise les expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 2%

---

# (Version bêta) [!DNL Braze] connexion

>[!IMPORTANT]
>
>La destination du braze dans Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

La destination [!DNL Braze] vous aide à envoyer des données de profil à [!DNL Braze].

[!DNL Braze] est une plateforme d’engagement client exhaustive qui optimise les expériences pertinentes et mémorisables entre les clients et les marques qu’ils aiment.

Pour envoyer des données de profil à [!DNL Braze], vous devez d’abord vous connecter à la destination.

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques à la destination [!DNL Braze] :

* [!DNL Adobe Experience Platform] les segments sont exportés vers  [!DNL Braze] sous l’ `AdobeExperiencePlatformSegments` attribut .

>[!NOTE]
>
>Gardez à l’esprit que l’envoi d’attributs personnalisés supplémentaires à [!DNL Braze] peut entraîner une augmentation de la consommation de vos points de données [!DNL Braze]. Consultez votre gestionnaire de compte [!DNL Braze] avant d’envoyer des attributs personnalisés supplémentaires.

## Cas d&#39;utilisation {#use-cases}

En tant que marketeur, je souhaite cibler les utilisateurs dans une destination d’engagement mobile, avec des segments créés dans [!DNL Adobe Experience Platform]. En outre, je souhaite leur fournir des expériences personnalisées, en fonction des attributs de leurs profils [!DNL Adobe Experience Platform], dès que les segments et les profils sont mis à jour dans [!DNL Adobe Experience Platform].

## Identités prises en charge {#supported-identities}

[!DNL Braze] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| external_id | Identifiant [!DNL Braze] personnalisé qui prend en charge le mappage de n’importe quelle identité. | Vous pouvez envoyer n’importe quelle [identité](../../../identity-service/namespaces.md) à la destination [!DNL Braze] tant que vous la mappez à la [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

## Type d&#39;export {#export-type}

**[!DNL Profile-based]** - vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom) et/ou identités, en fonction du mappage de vos champs.
[!DNL Adobe Experience Platform] les segments sont exportés vers  [!DNL Braze] sous l’ `AdobeExperiencePlatformSegments` attribut .

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Jeton de compte de braquage]** : C&#39;est ta  [!DNL Braze] [!DNL API] clé. Vous trouverez des instructions détaillées sur la manière d’obtenir votre clé [!DNL API] ici : [Présentation de la clé API REST](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Nom]** : saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : saisissez une description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Instance]** de point d’entrée : demandez à votre  [!DNL Braze] représentant l’instance de point d’entrée que vous devez utiliser.

## Activation des segments vers cette destination {#activate}

Voir [Activation des profils et des segments vers une destination](../../ui/activate-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers des destinations.

## Considérations relatives au mappage {#mapping-considerations}

Pour envoyer correctement les données d’audience de [!DNL Adobe Experience Platform] vers la destination [!DNL Braze], vous devez passer par l’étape de mappage des champs.

Le mappage consiste à créer un lien entre vos champs de schéma [!DNL Experience Data Model] (XDM) dans votre compte [!DNL Platform] et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL Braze], procédez comme suit :

À l’étape [!UICONTROL Mapping], cliquez sur **[!UICONTROL Ajouter un nouveau mappage]**.

![Mappage de l’ajout de la destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping.png)

Dans la section [!UICONTROL Champ source] , cliquez sur la flèche en regard du champ vide.

![Mappage de la source de destination du braquage](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ source] , vous pouvez choisir entre deux catégories de champs XDM :
* [!UICONTROL Sélectionner des attributs] : utilisez cette option pour mapper un champ spécifique de votre schéma XDM à un  [!DNL Braze] attribut.

![Attribut source de mappage de destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Sélectionnez l’espace de noms] d’identité : Utilisez cette option pour mapper un espace de noms  [!DNL Platform] d’identité à un  [!DNL Braze] espace de noms.

![Espace de noms source du mapping de destination de la suppression](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Choisissez votre champ source, puis cliquez sur **[!UICONTROL Sélectionner]**.

Dans la section [!UICONTROL Champ cible] , cliquez sur l’icône de mappage située à droite du champ.

![Mappage cible de la destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ cible] , vous pouvez choisir entre trois catégories de champs cibles :
* [!UICONTROL Sélectionner des attributs] : Utilisez cette option pour mapper vos attributs XDM aux  [!DNL Braze] attributs standard.
* [!UICONTROL Sélectionnez l’espace de noms] d’identité : Utilisez cette option pour mapper les espaces de noms  [!DNL Platform] d’identité aux espaces de noms  [!DNL Braze] d’identité.
* [!UICONTROL Sélectionner des attributs] personnalisés : Utilisez cette option pour mapper les attributs XDM aux  [!DNL Braze] attributs personnalisés que vous avez définis dans votre  [!DNL Braze] compte.
* Vous pouvez également utiliser cette option pour renommer les attributs XDM existants en [!DNL Braze]. Par exemple, le mappage d’un attribut XDM `lastName` à un attribut `Last_Name` personnalisé dans [!DNL Braze] crée l’attribut `Last_Name` dans [!DNL Braze], s’il n’existe pas déjà, et lui fait correspondre l’attribut XDM `lastName`.

![Braquer les champs de mappage cible de destination](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Choisissez votre champ cible, puis cliquez sur **[!UICONTROL Sélectionner]**.

Vous devriez maintenant voir votre mappage de champ dans la liste.

![Mappage de destination du bloc terminé](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Pour ajouter d’autres mappages, répétez les étapes précédentes.

## Exemple de mappage {#mapping-example}

Supposons que votre schéma de profil XDM et votre instance [!DNL Braze] contiennent les attributs et identités suivants :

|  | Schéma de profil XDM | [!DNL Braze] Instance |
|---|---|---|
| Attributs | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identités | <ul><li>Email</code></li><li>Identifiant Google Ad (GAID)</code></li><li>Identifiant Apple Pour Les Annonceurs (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Le mappage correct se présente comme suit :

![Exemple de mappage de destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Braze], vérifiez votre compte [!DNL Braze]. [!DNL Adobe Experience Platform] les segments sont exportés vers  [!DNL Braze] sous l’ `AdobeExperiencePlatformSegments` attribut .

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](../../../data-governance/home.md).
