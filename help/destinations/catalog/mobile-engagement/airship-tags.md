---
keywords: balises d’avion;destination du navire d’aviation
title: Connexion à Airship Tags
description: Transmettez en toute transparence les données d’audience Adobe à Airship en tant que balises d’audience pour le ciblage dans Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# [!DNL Airship Tags] connection {#airship-tags-destination}

## Présentation

[!DNL Airship] est la principale plateforme d’engagement client, qui vous aide à diffuser des messages omnicanaux personnalisés et pertinents à vos utilisateurs à chaque étape du cycle de vie des clients.

Cette intégration transmet les données de segment Adobe Experience Platform dans [!DNL Airship] sous la forme [Balises](https://docs.airship.com/guides/audience/tags/) pour le ciblage ou le déclenchement.

Pour en savoir plus sur [!DNL Airship], voir [Documents de navigation ](https://docs.airship.com).


>[!TIP]
>
>Cette page de documentation a été créée par l’équipe [!DNL Airship]. Pour toute demande de mise à jour ou de mise à jour, contactez-les directement à l’adresse [support.airship.com](https://support.airship.com/).

## Conditions préalables

Avant d’envoyer vos segments Adobe Experience Platform à [!DNL Airship], vous devez :

* Créez un groupe de balises dans votre projet [!DNL Airship].
* Générez un jeton porteur pour l’authentification.

>[!TIP]
> 
>Créez un compte [!DNL Airship] via [ce lien d’inscription](https://go.airship.eu/accounts/register/plan/starter/) si ce n’est déjà fait.

## Groupes de balises

Le concept de segments dans Adobe Experience Platform est similaire aux [balises](https://docs.airship.com/guides/audience/tags/) dans Airship, avec de légères différences de mise en oeuvre. Cette intégration mappe l’état de l’appartenance d’un utilisateur à un segment Experience Platform](../../../xdm/field-groups/profile/segmentation.md) à la présence ou non d’une balise [!DNL Airship]. [ Par exemple, dans un segment Platform où `xdm:status` se transforme en `realized`, la balise est ajoutée au canal [!DNL Airship] ou nommée utilisateur auquel ce profil est mappé. Si la balise `xdm:status` est remplacée par `exited`, elle est supprimée.

Pour activer cette intégration, créez un *groupe de balises* dans [!DNL Airship] nommé `adobe-segments`.

>[!IMPORTANT]
>
>Lors de la création de votre nouveau groupe de balises **Ne cochez pas** le bouton radio qui indique &quot;[!DNL Allow these tags to be set only from your server]&quot;. Ce faisant, l’intégration des balises d’Adobe échouera.

Voir [Gestion des groupes de balises](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) pour obtenir des instructions sur la création du groupe de balises.

## Générer un jeton porteur

Accédez à **[!UICONTROL Paramètres]**&quot; **[!UICONTROL API et intégrations]** dans le [Tableau de bord de la navigation](https://go.airship.com) et sélectionnez **[!UICONTROL Jetons]** dans le menu de gauche.

Cliquez sur **[!UICONTROL Créer un jeton]**.

Attribuez un nom convivial à votre jeton, par exemple &quot;Destination des balises d’Adobe&quot;, puis sélectionnez &quot;Accès complet&quot; pour le rôle.

Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les détails comme confidentiels.

## Cas d&#39;utilisation

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Airship Tags], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1

Les clients au détail ou les plateformes de divertissement peuvent créer des profils utilisateur sur leurs clients fidèles et transmettre ces segments dans [!DNL Airship] pour le ciblage des messages sur les campagnes mobiles.

### Cas d’utilisation #2

Déclenchez des messages un-à-un en temps réel lorsque les utilisateurs entrent ou sortent de segments spécifiques dans Adobe Experience Platform.

Par exemple, un détaillant configure un segment spécifique à la marque jeans dans Platform. Ce détaillant peut désormais déclencher un message mobile dès que quelqu’un définit la préférence de son jean sur une marque spécifique.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Jeton]** porteur : le jeton porteur que vous avez généré à partir du  [!DNL Airship] tableau de bord.
* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : saisissez une description pour cette destination.
* **[!UICONTROL Domaine]** : sélectionnez un centre de données des États-Unis ou de l’UE, en fonction du centre  [!DNL Airship] de données qui s’applique à cette destination.


## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de segments en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

[!DNL Airship] Les balises peuvent être définies sur un canal, qui représente l’instance de l’appareil, par exemple l’iPhone, ou un utilisateur nommé, qui mappe tous les appareils d’un utilisateur à un identifiant commun tel qu’un ID de client. Si votre schéma contient des adresses électroniques en texte brut (non hachées) comme identité Principale, sélectionnez le champ de l’adresse électronique dans vos **[!UICONTROL Attributs source]** et mappez-les à l’utilisateur [!DNL Airship] nommé dans la colonne de droite sous **[!UICONTROL Identités cibles]**, comme illustré ci-dessous.

![Mappage des utilisateurs nommés](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire un appareil, mappez-les au canal approprié en fonction de la source. Les images suivantes montrent comment mapper un identifiant Google Advertising à un canal Android [!DNL Airship].

![Connexion à Airship ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![TagsConnexion à Airship ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Tags Channel Mapping](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](../../../data-governance/home.md).
