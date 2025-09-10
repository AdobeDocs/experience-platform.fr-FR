---
keywords: balises airship;destination airship
title: Connexion Balises Airship
description: Transmettez facilement les données d’audience Adobe à Airship sous la forme de balises d’audience pour le ciblage dans Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 5a2f1c87381c39d6d15f569523cfb3b00d02b34b
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 32%

---

# Connexion [!DNL Airship Tags] {#airship-tags-destination}

## Présentation

[!DNL Airship] est la principale plateforme d’engagement des clients. Elle vous permet de fournir à vos utilisateurs des messages omnicanal pertinents et personnalisés à chaque étape du cycle de vie du client.

Cette intégration transmet les données d’audience Adobe Experience Platform dans des [!DNL Airship] sous la forme de [Balises](https://docs.airship.com/guides/audience/tags/) à des fins de ciblage ou de déclenchement.

Pour en savoir plus sur [!DNL Airship], consultez les [documents relatifs aux dirigeables](https://docs.airship.com).


>[!TIP]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe [!DNL Airship]. Pour toute demande ou information, contactez directement l&#39;équipe d&#39;assistance technique [support.airship.com](https://support.airship.com/).

## Conditions préalables

Avant d’envoyer vos audiences Adobe Experience Platform à [!DNL Airship], vous devez :

* Créez un groupe de balises dans votre projet [!DNL Airship].
* Générez un jeton porteur pour l’authentification.

>[!TIP]
> 
>Créez un compte [!DNL Airship] via [ce lien d’inscription](https://go.airship.eu/accounts/register/plan/starter/) si ce n’est pas déjà fait.

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
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants utilisés dans la destination Balises Airship . |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Groupes de balises

Le concept d’audiences dans Adobe Experience Platform est similaire à [Balises](https://docs.airship.com/guides/audience/tags/) dans Airship, avec de légères différences d’implémentation. Cette intégration mappe le statut de l’[appartenance d’un utilisateur à un segment Experience Platform](../../../xdm/field-groups/profile/segmentation.md) à la présence ou à la non-présence d’une balise [!DNL Airship]. Par exemple, dans une audience Experience Platform où la `xdm:status` est remplacée par `realized`, la balise est ajoutée au canal [!DNL Airship] ou à l’utilisateur nommé auquel ce profil est mappé. Si la `xdm:status` devient `exited`, la balise est supprimée.

Pour activer cette intégration, créez un *groupe de balises* dans [!DNL Airship] appelé `adobe-segments`.

>[!IMPORTANT]
>
>Lors de la création de votre groupe de balises **ne cochez pas** cliquez sur le bouton radio indiquant « [!DNL Allow these tags to be set only from your server] ». Cela entraîne l’échec de l’intégration des balises Adobe.

Voir [Gérer les groupes de balises](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) pour obtenir des instructions sur la création du groupe de balises.

## Générer un jeton du porteur

Accédez à **[!UICONTROL Paramètres]** » **[!UICONTROL API et intégrations]** dans le tableau de bord [Airship](https://go.airship.com) et sélectionnez **[!UICONTROL Jetons]** dans le menu de gauche.

Cliquez sur **[!UICONTROL Créer un jeton]**.

Attribuez un nom convivial à votre jeton, par exemple « Destination Adobe Tags », et sélectionnez « Tous les accès » pour le rôle.

Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les détails comme confidentiels.

## Cas d’utilisation

Pour mieux comprendre quand et comment utiliser la destination [!DNL Airship Tags], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1

Les détaillants ou les plateformes de divertissement peuvent créer des profils d’utilisateurs sur leurs clients fidèles et transmettre ces audiences dans des [!DNL Airship] pour le ciblage des messages sur les campagnes mobiles.

### Cas d’utilisation #2

Déclenchez des messages un-à-un en temps réel lorsque les utilisateurs appartiennent ou non à des audiences spécifiques dans Adobe Experience Platform.

Par exemple, un retailer configure une audience spécifique à la marque Jeans dans Experience Platform. Ce retailer peut désormais déclencher un message mobile dès que quelqu’un définit sa préférence de jeans sur une marque spécifique.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Jeton porteur]** : jeton porteur que vous avez généré depuis le tableau de bord de la [!DNL Airship].

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : saisissez une description pour cette destination.
* **[!UICONTROL Domaine]** : sélectionnez un centre de données des États-Unis ou de l’UE, selon le centre de données [!DNL Airship] qui s’applique à cette destination.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

[!DNL Airship] balises peuvent être définies sur un canal, qui représente une instance d’appareil, par exemple iPhone, ou sur un utilisateur nommé, qui mappe tous les appareils d’un utilisateur à un identifiant commun, tel qu’un identifiant client. Si votre schéma comporte des adresses e-mail en texte brut (non hachées) comme identité principale, sélectionnez le champ e-mail dans vos **[!UICONTROL Attributs Source]** et mappez-les à l’utilisateur [!DNL Airship] nommé dans la colonne de droite sous **[!UICONTROL Identités cibles]**, comme illustré ci-dessous.

![Mappage d’utilisateurs nommés](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire un appareil, mappez-le au canal approprié en fonction de la source. Les images suivantes montrent comment mapper un identifiant Advertising Google à un canal Android [!DNL Airship].

![Se connecter aux balises Airship](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Se connecter aux balises Airship](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mappage de canal](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez [présentation de la gouvernance des données](../../../data-governance/home.md).
