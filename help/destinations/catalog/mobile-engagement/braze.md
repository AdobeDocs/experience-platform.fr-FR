---
keywords: mobile, braser, messagerie;
title: Connexion Braze
description: Braze est une plateforme d’engagement client complète qui optimise les expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 31%

---

# Connexion [!DNL Braze]

## Présentation {#overview}

La destination [!DNL Braze] vous aide à envoyer des données de profil à [!DNL Braze].

[!DNL Braze] est une plateforme d’engagement client complète qui offre des expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment.

Pour envoyer des données de profil à [!DNL Braze], vous devez d’abord vous connecter à la destination.

## Spécificités de la destination {#specifics}

Notez les détails suivants spécifiques à la destination [!DNL Braze] :

* Les audiences [!DNL Adobe Experience Platform] sont exportées vers [!DNL Braze] sous l’attribut `AdobeExperiencePlatformSegments` .

>[!NOTE]
>
>Gardez à l’esprit que l’envoi d’attributs personnalisés supplémentaires à [!DNL Braze] peut entraîner une augmentation de la consommation de votre point de données [!DNL Braze]. Contactez votre gestionnaire de compte [!DNL Braze] avant d’envoyer des attributs personnalisés supplémentaires.

## Cas d’utilisation {#use-cases}

En tant que marketeur, je souhaite cibler les utilisateurs dans une destination d’engagement mobile, avec des audiences intégrées à [!DNL Adobe Experience Platform]. En outre, je souhaite leur fournir des expériences personnalisées, en fonction des attributs de leurs profils [!DNL Adobe Experience Platform], dès que les audiences et les profils sont mis à jour dans [!DNL Adobe Experience Platform].

## Identités prises en charge {#supported-identities}

[!DNL Braze] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| external_id | Identifiant [!DNL Braze] personnalisé qui prend en charge le mappage de n’importe quelle identité. | Vous pouvez envoyer n&#39;importe quelle [identité](../../../identity-service/features/namespaces.md) à la destination [!DNL Braze] tant que vous la mappez à la [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse email, numéro de téléphone, nom) et/ou les identités, en fonction du mapping de vos champs.Les audiences [!DNL Adobe Experience Platform] sont exportées vers [!DNL Braze] sous l’attribut `AdobeExperiencePlatformSegments` . |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Jeton de compte de braze]** : il s’agit de votre clé [!DNL Braze] [!DNL API]. Vous trouverez des instructions détaillées sur la manière d’obtenir votre clé [!DNL API] ici : [Présentation de la clé API REST](https://www.braze.com/docs/api/api_key/).

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : saisissez un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : saisissez une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Instance de point d’entrée]** : demandez à votre représentant [!DNL Braze] quelle instance de point d’entrée vous devez utiliser.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

Pour envoyer correctement les données d’audience de [!DNL Adobe Experience Platform] vers la destination [!DNL Braze], vous devez passer par l’étape de mappage des champs.

Le mappage consiste à créer un lien entre vos champs de schéma [!DNL Experience Data Model] (XDM) dans votre compte [!DNL Platform] et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL Braze], procédez comme suit :

À l’étape [!UICONTROL Mapping], cliquez sur **[!UICONTROL Ajouter un nouveau mapping]**.

![Braze Destination Add Mapping](../../assets/catalog/mobile-engagement/braze/mapping.png)

Dans la section [!UICONTROL Champ Source] , cliquez sur la flèche en regard du champ vide.

![Braze Destination Source Mapping](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ source] , vous pouvez choisir entre deux catégories de champs XDM :
* [!UICONTROL Sélectionner des attributs] : utilisez cette option pour mapper un champ spécifique de votre schéma XDM à un attribut [!DNL Braze].

![Attribut Source de mappage de destination de braze](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Sélectionner un espace de noms d’identité] : utilisez cette option pour mapper un espace de noms d’identité [!DNL Platform] à un espace de noms [!DNL Braze].

![Braze Destination Mapping Espace de noms Source](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Sélectionnez votre champ source, puis cliquez sur **[!UICONTROL Sélectionner]**.

Dans la section [!UICONTROL Champ cible] , cliquez sur l’icône de mappage située à droite du champ.

![Braze Destination Mapping](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Dans la fenêtre [!UICONTROL Sélectionner le champ cible] , vous pouvez choisir entre deux catégories de champs cibles :
* [!UICONTROL Sélectionner l’espace de noms d’identité] : utilisez cette option pour mapper les espaces de noms d’identité [!DNL Platform] aux espaces de noms d’identité [!DNL Braze].
* [!UICONTROL Sélectionner des attributs personnalisés] : utilisez cette option pour mapper des attributs XDM aux attributs [!DNL Braze] personnalisés que vous avez définis dans votre compte [!DNL Braze]. <br> Vous pouvez également utiliser cette option pour renommer les attributs XDM existants en [!DNL Braze]. Par exemple, le mappage d’un attribut XDM `lastName` à un attribut `Last_Name` personnalisé dans [!DNL Braze], créera l’attribut `Last_Name` dans [!DNL Braze], s’il n’existe pas déjà, et lui mappera l’attribut XDM `lastName`.

![Braze Destination Mapping Fields](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Sélectionnez votre champ cible, puis cliquez sur **[!UICONTROL Sélectionner]**.

Vous devriez maintenant voir votre mappage de champ dans la liste.

![Braze Destination Mapping Complete](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Pour ajouter d’autres mappages, répétez les étapes précédentes.

## Exemple de mappage {#mapping-example}

Supposons que votre schéma de profil XDM et votre instance [!DNL Braze] contiennent les attributs et identités suivants :

|  | Schéma de profil XDM | [!DNL Braze] Instance |
|---|---|---|
| Attributs | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>FirstName</code></li><li><code>LastName</code></li><li><code>PhoneNumber</code></li></ul> |
| Identités | <ul><li><code> Email</code></li><li><code>Google Ad ID (GAID)</code></li><li><code>Apple ID For Advertisers (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

Le mappage correct se présente comme suit :

![Exemple de mappage de destination de braze](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Braze], vérifiez votre compte [!DNL Braze]. Les audiences [!DNL Adobe Experience Platform] sont exportées vers [!DNL Braze] sous l’attribut `AdobeExperiencePlatformSegments` .

## Dépannage {#troubleshooting}

**J’ai reçu une erreur de délai d’expiration lors de l’activation de mes audiences vers cette destination. Que dois-je faire ?**

L’activation de l’audience vers cette destination peut parfois entraîner une erreur de délai d’expiration. Cette erreur n’indique pas un problème d’activation.

Si vous recevez une erreur de délai d’expiration, vérifiez la taille de l’audience dans la plateforme de destination. Si la taille de l’audience est correcte, l’intégration fonctionne comme prévu.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour plus d’informations sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [présentation de la gouvernance des données](../../../data-governance/home.md).
