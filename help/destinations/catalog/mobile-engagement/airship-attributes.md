---
keywords: attributs de navire d’aviation;destination du navire d’aviation
title: Connexion aux attributs du navire
description: Transférez en toute transparence les données d’audience Adobe à Airship en tant qu’attributs d’audience pour le ciblage au sein de Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# (Version bêta) [!DNL Airship Attributes] connexion {#airship-attributes-destination}

>[!IMPORTANT]
>
>La destination [!DNL Airship Attributes] de Adobe Experience Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

[!DNL Airship] est la principale plateforme d’engagement client, qui vous aide à diffuser des messages omnicanaux personnalisés et pertinents à vos utilisateurs à chaque étape du cycle de vie des clients.

Cette intégration transmet les données de profil d’Adobe dans [!DNL Airship] sous la forme [Attributs](https://docs.airship.com/guides/audience/attributes/) pour le ciblage ou le déclenchement.

Pour en savoir plus sur [!DNL Airship], voir [Documents de navigation ](https://docs.airship.com).

>[!TIP]
>
>Cette page de documentation a été créée par l’équipe [!DNL Airship]. Pour toute demande de mise à jour ou de mise à jour, contactez-les directement à l’adresse [support.airship.com](https://support.airship.com/).

## Conditions préalables {#prerequisites}

Avant de pouvoir envoyer vos segments d’audience à [!DNL Airship], vous devez :

* Activez les attributs dans votre projet [!DNL Airship].
* Générez un jeton porteur pour l’authentification.

>[!TIP]
>
>Créez un compte [!DNL Airship] via [ce lien d’inscription](https://go.airship.eu/accounts/register/plan/starter/) si ce n’est déjà fait.

## Activation des attributs {#enable-attributes}

Les attributs de profil Adobe Experience Platform sont similaires aux attributs [!DNL Airship] et peuvent être facilement mappés les uns aux autres dans Platform à l’aide de l’outil de mappage présenté ci-dessous sur cette page.

[!DNL Airship] les projets comportent plusieurs attributs prédéfinis et par défaut. Si vous disposez d’un attribut personnalisé, vous devez d’abord le définir dans [!DNL Airship]. Voir [Configuration et gestion des attributs](https://docs.airship.com/tutorials/audience/attributes/) pour plus d’informations.

## Générer un jeton porteur {#bearer-token}

Accédez à **[!UICONTROL Paramètres]**&quot; **[!UICONTROL API et intégrations]** dans le [Tableau de bord de la navigation](https://go.airship.com) et sélectionnez **[!UICONTROL Jetons]** dans le menu de gauche.

Cliquez sur **[!UICONTROL Créer un jeton]**.

Attribuez un nom convivial à votre jeton, par exemple &quot;Destination des attributs d’Adobe&quot;, puis sélectionnez &quot;Accès complet&quot; pour le rôle.

Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les détails comme confidentiels.

## Cas d&#39;utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Airship Attributes], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1

Tirez parti des données de profil collectées dans Adobe Experience Platform pour personnaliser le message et le contenu riche dans l’un des canaux de [!DNL Airship]. Par exemple, utilisez les données de profil [!DNL Experience Platform] pour définir les attributs d’emplacement dans [!DNL Airship]. Cela permet à une marque d’hôtel d’afficher une image pour l’emplacement d’hôtel le plus proche pour chaque utilisateur.

### Cas d’utilisation #2

Tirez parti des attributs de Adobe Experience Platform pour enrichir davantage les profils [!DNL Airship] et les combiner à des données prédictives SDK ou [!DNL Airship]. Par exemple, un détaillant peut créer un segment avec le statut de fidélité et les données de localisation (attributs de Platform) et [!DNL Airship] prévu pour générer des données afin d’envoyer des messages très ciblés aux utilisateurs ayant le statut de fidélité à l’or qui vivent à Las Vegas, NV, et ont une forte probabilité d’attrition.

## Connexion à la destination {#connect}

Voir [Activation des données d’audience vers les destinations d’exportation de segments en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Jeton]** porteur : le jeton porteur que vous avez généré à partir du  [!DNL Airship] tableau de bord.
* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : saisissez une description pour cette destination.
* **[!UICONTROL Domaine]** : sélectionnez un centre de données des États-Unis ou de l’UE, en fonction du centre  [!DNL Airship] de données qui s’applique à cette destination.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de segments en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

[!DNL Airship] Les attributs peuvent être définis sur un canal, qui représente l’instance de l’appareil, par exemple l’iPhone, ou un utilisateur nommé, qui mappe tous les appareils d’un utilisateur à un identifiant commun, tel qu’un ID de client. Si votre schéma contient des adresses électroniques en texte brut (non hachées) comme identité Principale, sélectionnez le champ de l’adresse électronique dans vos **[!UICONTROL Attributs source]** et mappez-les à l’utilisateur [!DNL Airship] nommé dans la colonne de droite sous **[!UICONTROL Identités cibles]**, comme illustré ci-dessous.

![Mappage des utilisateurs nommés](../../assets/catalog/mobile-engagement/airship/mapping.png)

Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire un appareil, mappez-les au canal approprié en fonction de la source. Les images suivantes montrent comment deux mappages sont créés :

* IDFA iOS Advertising ID sur un canal iOS [!DNL Airship]
* Attribut `fullName` d’Adobe à [!DNL Airship] attribut &quot;Nom complet&quot;

>[!NOTE]
>
>Utilisez le nom convivial qui apparaît dans le tableau de bord [!DNL Airship] lors de la sélection du champ cible pour votre mappage d’attributs.

**Mappage d’identité**

Sélectionner le champ source :

![Connexion aux attributs des navires](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Sélectionnez le champ cible :

![Connexion aux attributs des navires](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Attribut Map**

Sélectionner l’attribut source :

![Sélectionner le champ source](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Sélectionnez l’attribut cible :

![Sélectionner le champ cible](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Vérification du mappage :

![Mappage des canaux](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](../../../data-governance/home.md).
