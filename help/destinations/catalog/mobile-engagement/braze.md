---
keywords: mobile ; braquer; messagerie ;
title: Connexion au frein
description: Braze est une plate-forme d'engagement client complète qui permet d'offrir des expériences pertinentes et mémorables entre les clients et les marques qu'ils aiment.
translation-type: tm+mt
source-git-commit: 0759919dc458798ca4bc5f233a9cb319194ea534
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 5%

---


# (Beta) [!DNL Braze] connexion

>[!IMPORTANT]
>
>La destination du braze à Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

La destination [!DNL Braze] vous aide à envoyer des données de profil à [!DNL Braze].

[!DNL Braze] est une plate-forme d&#39;engagement client complète qui permet d&#39;offrir des expériences pertinentes et mémorables entre les clients et les marques qu&#39;ils aiment.

Pour envoyer des données de profil à [!DNL Braze], vous devez d&#39;abord vous connecter à la destination.

## Spécifications de la destination {#destination-specs}

Notez les détails suivants spécifiques à la destination [!DNL Braze] :

* [!DNL Adobe Experience Platform] sont exportés vers  [!DNL Braze] sous l’ `AdobeExperiencePlatformSegments` attribut.

>[!NOTE]
>
>N’oubliez pas que l’envoi d’attributs personnalisés supplémentaires à [!DNL Braze] peut entraîner une augmentation de la consommation de vos points de données [!DNL Braze]. Consultez votre gestionnaire de compte [!DNL Braze] avant d&#39;envoyer des attributs personnalisés supplémentaires.

## Cas d’utilisation {#use-cases}

En tant que spécialiste du marketing, je souhaite cible les utilisateurs dans une destination d’engagement mobile, avec des segments créés dans [!DNL Adobe Experience Platform]. En outre, je souhaite leur proposer des expériences personnalisées, basées sur des attributs de leurs [!DNL Adobe Experience Platform] profils, dès que les segments et les profils sont mis à jour dans [!DNL Adobe Experience Platform].

### Identités prises en charge {#supported-identities}

[!DNL Google Ad Manager] prend en charge l&#39;activation des identités décrites dans le tableau ci-dessous.

| Identité de cible | Description | Considérations |
|---|---|---|
| external_id | Identificateur [!DNL Braze] personnalisé qui prend en charge le mappage de toute identité. | Vous pouvez envoyer toute [identité](../../../identity-service/namespaces.md) à la destination [!DNL Braze], à condition de la mapper à [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

## Type d&#39;exportation {#export-type}

**[!DNL Profile-based]** - vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom) et/ou identités, selon votre mappage de champs.
[!DNL Adobe Experience Platform] sont exportés vers  [!DNL Braze] sous l’ `AdobeExperiencePlatformSegments` attribut.


## Se connecter à la destination {#connect-destination}

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Braze], puis **[!UICONTROL Configurer]**.

![Configurer la destination du braquage](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.
>
>![Activer la destination du braquage](../../assets/catalog/mobile-engagement/braze/activate.png)

À l’étape [!UICONTROL Compte], vous devez fournir votre jeton de compte [!DNL Braze]. Il s&#39;agit de votre clé [!DNL Braze] [!DNL API]. Vous trouverez des instructions détaillées sur la façon d&#39;obtenir votre clé [!DNL API] ici : [Présentation de la clé d&#39;API REST](https://www.braze.com/docs/api/api_key/). Saisissez le jeton et cliquez sur **[!UICONTROL Se connecter à destination]**.

![Étape du compte de destination du braquage](../../assets/catalog/mobile-engagement/braze/account.png)

Cliquez sur **[!UICONTROL Suivant]**. À l’étape [!UICONTROL Authentification], vous devez saisir les détails de la connexion [!DNL Braze] :
* **[!UICONTROL Nom]** : entrez un nom qui vous permettra de reconnaître cette destination à l&#39;avenir.
* **[!UICONTROL Description]** : entrez une description qui vous aidera à identifier cette destination dans le futur.
* **[!UICONTROL Instance]** de point de terminaison : demandez à votre  [!DNL Braze] représentant quelle instance de point de terminaison vous devez utiliser.
* **[!UICONTROL Action]** marketing : les actions marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, voir la page [Gouvernance des données dans Adobe Experience Platform](../../../data-governance/policies/overview.md). Pour plus d&#39;informations sur les actions marketing définies par l&#39;Adobe, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

![Étape d&#39;authentification du frein](../../assets/catalog/mobile-engagement/braze/authentication.png)

Cliquez sur **[!UICONTROL Créer une destination]**. Votre destination est maintenant créée. Vous pouvez cliquer sur **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement, ou vous pouvez sélectionner **[!UICONTROL Suivant]** pour continuer le processus et sélectionner les segments à activer. Dans les deux cas, consultez la section suivante, [Activer les segments](#activate-segments), pour le reste du flux de travail.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md#select-attributes).

## Mappage des champs {#field-mapping}

Pour envoyer correctement les données d&#39;audience de [!DNL Adobe Experience Platform] à la destination [!DNL Braze], vous devez passer par l&#39;étape de mappage des champs.

Le mappage consiste à créer un lien entre vos champs de schéma [!DNL Experience Data Model] (XDM) de votre compte [!DNL Platform] et leurs équivalents correspondants de la destination de la cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL Braze], procédez comme suit :

À l’étape [!UICONTROL Mappage], cliquez sur **[!UICONTROL Ajouter un nouveau mappage]**.

![Mappage de l&#39;Ajoute de destination du braquage](../../assets/catalog/mobile-engagement/braze/mapping.png)

Dans la section [!UICONTROL Champ source], cliquez sur la flèche en regard du champ vide.

![Mappage de la source de destination du braquage](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ source], vous pouvez choisir entre deux catégories de champs XDM :
* [!UICONTROL Sélectionner des attributs] : utilisez cette option pour mapper un champ spécifique de votre schéma XDM à un  [!DNL Braze] attribut.

![Attribut source de mappage de destination de braquage](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Sélectionner l&#39;espace de nommage] d&#39;identité : Utilisez cette option pour mapper un espace de nommage  [!DNL Platform] d&#39;identité à un  [!DNL Braze] espace de nommage.

![Espace de nommage de la source de mappage de destination du braquage](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Sélectionnez votre champ source, puis cliquez sur **[!UICONTROL Sélectionner]**.

Dans la section [!UICONTROL Champ de Cible], cliquez sur l’icône de mappage à droite du champ.

![Mapping de ciblage de destination du braquage](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ de cible], vous pouvez choisir entre trois catégories de champs de cible :
* [!UICONTROL Sélectionner des attributs] : Utilisez cette option pour mapper vos attributs XDM à  [!DNL Braze] des attributs standard.
* [!UICONTROL Sélectionner l&#39;espace de nommage] d&#39;identité : Utilisez cette option pour mapper les espaces de nommage  [!DNL Platform] d&#39;identité aux espaces de nommage  [!DNL Braze] d&#39;identité.
* [!UICONTROL Sélectionner des attributs] personnalisés : Utilisez cette option pour mapper des attributs XDM à  [!DNL Braze] des attributs personnalisés que vous avez définis dans votre  [!DNL Braze] compte.
* Vous pouvez également utiliser cette option pour renommer les attributs XDM existants en [!DNL Braze]. Par exemple, le mappage d&#39;un attribut XDM `lastName` à un attribut `Last_Name` personnalisé dans [!DNL Braze] crée l&#39;attribut `Last_Name` dans [!DNL Braze], s&#39;il n&#39;existe pas déjà, et lui associe l&#39;attribut XDM `lastName`.

![Champs du Mapping de ciblage de destination du braquage](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Choisissez votre champ de cible, puis cliquez sur **[!UICONTROL Sélectionner]**.

Vous devriez maintenant voir votre mappage de champs dans la liste.

![Mappage de destination du braquage terminé](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Pour ajouter d’autres mappages, répétez les étapes précédentes.

### Exemple {#mapping-example}

Supposons que votre schéma de profil XDM et votre instance [!DNL Braze] contiennent les attributs et identités suivants :

|  | Schéma de Profil XDM | [!DNL Braze] Instance |
|---|---|---|
| Attributs | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>Prénom</code></li><li>Nom</code></li><li>PhoneNumber</code></li></ul> |
| Identités | <ul><li>E-mail</code></li><li>Identifiant de publicité Google (GAID)</code></li><li>ID Apple pour les annonceurs (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

Le mappage correct se présenterait comme suit :

![Exemple de mappage des destinations de braquage](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Braze], vérifiez votre compte [!DNL Braze]. [!DNL Adobe Experience Platform] sont exportés vers  [!DNL Braze] sous l’ `AdobeExperiencePlatformSegments` attribut.

## Utilisation des données et gouvernance {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux règles d&#39;utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](../../../data-governance/home.md).

