---
keywords: balises d’avion;destination du navire d’aviation
title: Connexion Balises Airship
description: Transmettez en toute transparence les données d’audience Adobe à Airship en tant que balises d’audience pour le ciblage dans Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 38%

---

# Connexion [!DNL Airship Tags] {#airship-tags-destination}

## Présentation

[!DNL Airship] est la principale plateforme d’engagement client, qui vous aide à diffuser des messages omnicanaux personnalisés et pertinents à vos utilisateurs à chaque étape du cycle de vie des clients.

Cette intégration transmet les données de segment Adobe Experience Platform dans [!DNL Airship] as [Balises](https://docs.airship.com/guides/audience/tags/) pour le ciblage ou le déclenchement.

Pour en savoir plus sur [!DNL Airship], reportez-vous à la section [Documents de navigation](https://docs.airship.com).


>[!TIP]
>
>Cette page de documentation a été créée par la fonction [!DNL Airship] l&#39;équipe. Pour toute demande de mise à jour ou de renseignements, contactez-les directement à l’adresse [support.airship.com](https://support.airship.com/).

## Conditions préalables

Avant d’envoyer vos segments Adobe Experience Platform vers [!DNL Airship], vous devez :

* Créez un groupe de balises dans votre [!DNL Airship] projet.
* Générez un jeton porteur pour l’authentification.

>[!TIP]
> 
>Créez un [!DNL Airship] Compte via [ce lien d’inscription](https://go.airship.eu/accounts/register/plan/starter/) si vous ne l&#39;avez pas déjà fait.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants utilisés dans la destination des balises de navigation. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Groupes de balises

Le concept de segments dans Adobe Experience Platform est similaire à [Balises](https://docs.airship.com/guides/audience/tags/) dans Airship, avec de légères différences de mise en oeuvre. Cette intégration mappe l’état d’un utilisateur. [appartenance à un segment Experience Platform](../../../xdm/field-groups/profile/segmentation.md) à la présence ou à la non-présence d’un [!DNL Airship] balise . Par exemple, dans un segment Platform où la variable `xdm:status` change en `realized`, la balise est ajoutée à la fonction [!DNL Airship] canal ou utilisateur nommé auquel ce profil est mappé. Si la variable `xdm:status` change en `exited`, la balise est supprimée.

Pour activer cette intégration, créez une *groupe de balises* in [!DNL Airship] named `adobe-segments`.

>[!IMPORTANT]
>
>Lors de la création d’un groupe de balises **Ne pas cocher** le bouton radio qui indique &quot;[!DNL Allow these tags to be set only from your server]&quot;. Ce faisant, l’intégration des balises d’Adobe échouera.

Voir [Gestion des groupes de balises](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) pour obtenir des instructions sur la création du groupe de balises.

## Générer un jeton porteur

Accédez à **[!UICONTROL Paramètres]** &quot; **[!UICONTROL API et intégrations]** dans le [Tableau de bord des appareils](https://go.airship.com) et sélectionnez **[!UICONTROL Jetons]** dans le menu de gauche.

Cliquez sur **[!UICONTROL Créer un jeton]**.

Attribuez un nom convivial à votre jeton, par exemple &quot;Destination des balises d’Adobe&quot;, puis sélectionnez &quot;Accès complet&quot; pour le rôle.

Cliquez sur **[!UICONTROL Créer un jeton]** et enregistrez les informations comme confidentielles.

## Cas d’utilisation

Pour découvrir les avantages de la destination [!DNL Airship Tags] et son utilisation, consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1

Les clients au détail ou les plateformes de divertissement peuvent créer des profils utilisateur sur leurs clients fidèles et transmettre ces segments dans [!DNL Airship] pour le ciblage des messages sur les campagnes mobiles.

### Cas d’utilisation #2

Déclenchez des messages un-à-un en temps réel lorsque les utilisateurs entrent ou sortent de segments spécifiques dans Adobe Experience Platform.

Par exemple, un détaillant configure un segment spécifique à la marque jeans dans Platform. Ce détaillant peut désormais déclencher un message mobile dès que quelqu’un définit la préférence de son jean sur une marque spécifique.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL Jeton de porteur]**: le jeton porteur que vous avez généré à partir de la fonction [!DNL Airship] tableau de bord.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]**: saisissez une description pour cette destination.
* **[!UICONTROL Domaine]**: sélectionner un centre de données américain ou européen, selon le [!DNL Airship] le centre de données s’applique à cette destination.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activer les données d’audience vers des destinations d’exportation de segments de diffusion en continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Considérations relatives au mappage {#mapping-considerations}

[!DNL Airship] Les balises peuvent être définies sur un canal, qui représente l’instance de l’appareil, par exemple iPhone, ou un utilisateur nommé, qui mappe tous les appareils d’un utilisateur à un identifiant commun tel qu’un ID de client. Si votre schéma comporte des adresses électroniques en texte brut (non hachées) comme identité Principale, sélectionnez le champ d’adresse électronique dans votre **[!UICONTROL Attributs source]** et mappez sur le [!DNL Airship] utilisateur nommé dans la colonne de droite sous **[!UICONTROL Identités cibles]**, comme illustré ci-dessous.

![Mappage des utilisateurs nommés](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Pour les identifiants qui doivent être mappés à un canal, c’est-à-dire un appareil, mappez-les au canal approprié en fonction de la source. Les images suivantes montrent comment mapper un identifiant publicitaire Google à un [!DNL Airship] Canal Android.

![Connexion aux balises Airship](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Connexion aux balises Airship](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mappage de canaux](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](../../../data-governance/home.md).
