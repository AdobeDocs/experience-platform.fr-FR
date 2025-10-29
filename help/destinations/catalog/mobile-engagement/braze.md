---
keywords: mobile ; brasage ; messagerie ;
title: Connexion Braze
description: Braze est une plateforme d’engagement client complète qui alimente des expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 30%

---

# Connexion [!DNL Braze]

## Présentation {#overview}

La destination [!DNL Braze] vous permet d’envoyer des données de profil à [!DNL Braze].

[!DNL Braze] est une plateforme d’engagement client complète qui permet d’offrir des expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment.

Pour envoyer des données de profil à [!DNL Braze], vous devez d’abord vous connecter à la destination .

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques à la destination [!DNL Braze] :

* [!DNL Adobe Experience Platform] audiences sont exportées vers [!DNL Braze] sous l’attribut `AdobeExperiencePlatformSegments` .

>[!NOTE]
>
>Gardez à l’esprit que l’envoi d’attributs personnalisés supplémentaires à [!DNL Braze] peut entraîner des augmentations de la consommation de points de données [!DNL Braze]. Veuillez consulter votre gestionnaire de compte [!DNL Braze] avant d’envoyer des attributs personnalisés supplémentaires.

## Cas d’utilisation {#use-cases}

En tant que spécialiste marketing, je souhaite cibler les utilisateurs et utilisatrices dans une destination d’engagement mobile, avec des audiences intégrées dans [!DNL Adobe Experience Platform]. En outre, je souhaite leur proposer des expériences personnalisées, en fonction des attributs de leurs profils [!DNL Adobe Experience Platform], dès que les audiences et les profils seront mis à jour dans [!DNL Adobe Experience Platform].

## Identités prises en charge {#supported-identities}

[!DNL Braze] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| external_id | Identifiant de [!DNL Braze] personnalisé qui prend en charge le mappage de n’importe quelle identité. | Vous pouvez envoyer n’importe quelle [identité](../../../identity-service/features/namespaces.md) à la destination [!DNL Braze], à condition de la mapper à la [!DNL Braze][`external_id` &#x200B;](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Profile-based]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse e-mail, numéro de téléphone, nom) et/ou les identités, en fonction de votre mappage de champs.[!DNL Adobe Experience Platform] audiences sont exportées vers [!DNL Braze] sous l’attribut `AdobeExperiencePlatformSegments` . |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Braze account token]** : il s’agit de votre clé de [!DNL Braze] [!DNL API]. Vous trouverez des instructions détaillées sur la manière d’obtenir votre clé [!DNL API] ici : [Présentation de la clé API REST](https://www.braze.com/docs/api/api_key/).

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : saisissez une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Endpoint Instance]** : demandez à votre représentant [!DNL Braze] quelle instance de point d’entrée vous devez utiliser.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

Pour envoyer correctement vos données d’audience de [!DNL Adobe Experience Platform] vers la destination [!DNL Braze], vous devez passer par l’étape de mappage des champs.

Le mappage consiste à créer un lien entre vos champs de schéma [!DNL Experience Data Model] (XDM) dans votre compte [!DNL Experience Platform] et leurs équivalents provenant de la destination cible.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL Braze], procédez comme suit :

À l’étape [!UICONTROL Mapping], cliquez sur **[!UICONTROL Add new mapping]**.

![Braze Destination Ajouter Un Mappage](../../assets/catalog/mobile-engagement/braze/mapping.png)

Dans la section [!UICONTROL Source Field] , cliquez sur le bouton fléché en regard du champ vide.

![Mappage Braze Destination Source](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Dans la fenêtre [!UICONTROL Select source field] , vous pouvez choisir entre deux catégories de champs XDM :

* [!UICONTROL Select attributes] : utilisez cette option pour mapper un champ spécifique de votre schéma XDM à un attribut [!DNL Braze].

![Attribut Source de mappage de destination Braze](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace] : utilisez cette option pour mapper un espace de noms d’identité [!DNL Experience Platform] à un espace de noms [!DNL Braze].

![Espace de noms Source du mappage de destination Braze](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Choisissez votre champ source, puis cliquez sur **[!UICONTROL Select]**.

Dans la section [!UICONTROL Target Field] , cliquez sur l’icône de mappage à droite du champ.

![Mapping de ciblage de destination Braze](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Dans la fenêtre [!UICONTROL Select target field] , vous pouvez choisir entre deux catégories de champs cibles :

* [!UICONTROL Select identity namespace] : utilisez cette option pour mapper les espaces de noms d’identité [!DNL Experience Platform] aux espaces de noms d’identité [!DNL Braze].
* [!UICONTROL Select custom attributes] : utilisez cette option pour mapper les attributs XDM aux attributs [!DNL Braze] personnalisés que vous avez définis dans votre compte [!DNL Braze]. <br> Vous pouvez également utiliser cette option pour renommer les attributs XDM existants en [!DNL Braze]. Par exemple, le mappage d’un attribut XDM `lastName` à un attribut `Last_Name` personnalisé dans [!DNL Braze] crée l’attribut `Last_Name` dans [!DNL Braze], s’il n’existe pas déjà, et lui associe l’attribut XDM `lastName`.

![Braze Champs De Mapping De Destination](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Choisissez votre champ cible, puis cliquez sur **[!UICONTROL Select]**.

Votre mappage de champs doit maintenant s’afficher dans la liste.

![Mappage de destination Braze terminé](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Pour ajouter d’autres mappages, répétez les étapes précédentes.

## Exemple de mappage {#mapping-example}

Supposons que votre schéma de profil XDM et votre instance [!DNL Braze] contiennent les attributs et identités suivants :

|  | Schéma de profil XDM | Instance [!DNL Braze] |
|---|---|---|
| Attributs | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>Prénom</code></li><li><code>NomDeFamille</code></li><li><code>PhoneNumber</code></li></ul> |
| Identités | <ul><li><code>E-mail</code></li><li><code>Google Ad ID (GAID)</code></li><li><code>Apple ID pour les annonceurs (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

Le mappage correct se présente comme suit :

![Exemple de mappage de destination Braze](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Braze], vérifiez votre compte [!DNL Braze]. [!DNL Adobe Experience Platform] audiences sont exportées vers [!DNL Braze] sous l’attribut `AdobeExperiencePlatformSegments` .

## Résolution des problèmes {#troubleshooting}

**J’ai reçu une erreur de temporisation lors de l’activation de mes audiences vers cette destination. Que dois-je faire ?**

L’activation de l’audience vers cette destination peut parfois entraîner une erreur de délai d’expiration. Cette erreur n’indique pas toujours un problème d’activation.

Si vous recevez une erreur de temporisation, vérifiez la taille de l’audience dans la plateforme de destination. Si la taille de l’audience est correcte, l’intégration fonctionne comme prévu.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez [présentation de la gouvernance des données](../../../data-governance/home.md).
