---
title: LiveRamp - Connexion de distribution
description: Découvrez comment utiliser le connecteur LiveRamp - Distribution pour orchestrer et activer les audiences précédemment intégrées dans LiveRamp, vers les destinations publicitaires en aval.
exl-id: 1b11a743-1ef9-4b01-90ef-cc072bc03c91
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '2722'
ht-degree: 45%

---

# Connexion [!DNL LiveRamp - Distribution]

La connexion [!DNL LiveRamp - Distribution] vous permet d’activer les audiences des éditeurs Experience Platform aux éditeurs Premium sur les médias mobiles, web, d’affichage et de télévision connectés.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par LiveRamp. Pour toute demande de mise à jour ou de demande de mise à jour, contactez LiveRamp directement [ici](mailto:adobertcdp@liveramp.com).

## Destinations prises en charge {#supported-destinations}

[!DNL LiveRamp - Distribution] prend actuellement en charge l’activation de l’audience sur les plateformes suivantes :

* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL LiveRamp - Distribution], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

L’équipe marketing d’un détaillant de vêtements de sport a utilisé la connexion [LiveRamp - Intégration](liveramp-onboarding.md) pour envoyer des audiences d’Experience Platform vers son compte LiveRamp.

Grâce à la connexion [!DNL LiveRamp - Distribution], ils peuvent désormais déclencher l’activation des audiences intégrées vers les [destinations prises en charge](#supported-destinations). Ensuite, ils peuvent cibler les utilisateurs sur les plateformes mobiles, web ouvertes, sociales et [!DNL CTV].

## Audiences intégrées à LiveRamp {#onboarding}

Avant d’activer les audiences par le biais de la connexion [!DNL LiveRamp - Distribution], utilisez la connexion [LiveRamp - Intégration](liveramp-onboarding.md) pour exporter les audiences Experience Platform vers LiveRamp.

Une fois que vous avez intégré vos audiences à LiveRamp, continuez le processus d’activation à partir de l’étape [se connecter à la destination](#connect) pour sélectionner et configurer vos plateformes de destination cibles pour l’activation des données.

## Se connecter à la destination {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Paramètres d’identifiant"
>abstract="Sélectionnez les identifiants pris en charge par votre destination. Consultez la documentation pour obtenir la liste complète des identifiants pris en charge pour chaque destination."

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Authentification à LiveRamp {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Image de l’interface utilisateur de la plateforme montrant l’écran de connexion de destination. l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL ID d’organisation LiveRamp]** : ID d’organisation de votre compte LiveRamp (répertorié comme _propriétaire_org_ dans vos informations d’identification LiveRamp fournies).
* **[!UICONTROL Mot de passe]** : mot de passe de votre compte LiveRamp (répertorié comme _secret_key_ dans vos informations d’identification LiveRamp fournies).
* **[!UICONTROL URL du jeton]** : votre URL de jeton LiveRamp.
* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur de votre compte LiveRamp (répertorié en tant que _compte_id_ dans vos informations d’identification LiveRamp fournies).

### Configuration des détails de destination {#destination-details}

Une fois que vous êtes connecté à votre compte LiveRamp, saisissez les informations requises pour vous connecter à la destination vers laquelle vous souhaitez activer les audiences.

![ Image de l’interface utilisateur de la plateforme montrant l’écran des détails de la destination. l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Nom]** : renseignez le nom préféré de votre connexion de destination.

>[!NOTE]
>
>Lorsque vous nommez votre destination, Adobe recommande de suivre ce format : `LiveRamp - Downstream Destination Name`. Ce modèle de dénomination vous permet d’identifier rapidement vos destinations dans l’onglet [Parcourir](../../ui/destinations-workspace.md#browse) de l’espace de travail des destinations.
><br>
>Exemple : `LiveRamp - Roku`.

* **[!UICONTROL Description]** : saisissez une description pour votre destination. Utilisez une description qui vous aide à identifier facilement l’objectif de cette destination.
* **[!UICONTROL Destination]** : utilisez le menu déroulant pour sélectionner la destination vers laquelle vous souhaitez activer les audiences. La destination que vous sélectionnez ici affecte directement ce que vous voyez dans l’écran [paramètres spécifiques à la destination](#destination-settings).
* **[!UICONTROL Intégration]** : sélectionnez le compte d’intégration que vous souhaitez utiliser pour votre destination.
* **[!UICONTROL Identifiant]** : sélectionnez les identifiants pris en charge par votre destination. Actuellement, les identifiants pris en charge de toutes les destinations sont préremplis dans le menu déroulant.

## Paramètres spécifiques à la destination {#destination-settings}

Chacune des destinations [prises en charge](#supported-destinations) par [!DNL LiveRamp - Distribution] nécessite que vous renseignez des options de configuration spécifiques.

Consultez les sections ci-dessous pour obtenir des instructions détaillées sur la configuration de chaque destination.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="Identifiant de profil de marque 4C"
>abstract="Saisissez l’identifiant numérique associé à votre profil de marque 4C. Si vous ne disposez pas de cet identifiant, contactez votre représentant ou représentante des services à la clientèle 4C."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination Statistiques 4C.](../../assets/catalog/advertising/liveramp-distribution/LR_4C_DestSpecific.png)

* **[!UICONTROL 4C Brand Profile ID]** : saisissez l’identifiant numérique associé à votre profil de marque 4C. Si vous ne disposez pas de cet identifiant, contactez votre représentant ou représentante des services à la clientèle 4C.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination Acast.](../../assets/catalog/advertising/liveramp-distribution/LR_Acast_DestSpecific.png)

* **[!UICONTROL Nom du client]** : nom de votre compte publicitaire, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Ampersand.tv] {#ampersand-tv}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_ampersand_company_name"
>title="Nom de votre société"
>abstract="Nom de votre société, tel que vous souhaitez le présenter au partenaire de destination. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données client pour la destination d’esperluette.](../../assets/catalog/advertising/liveramp-distribution/LR_Ampersand_DestSpecific.png)

* **[!UICONTROL Nom de votre société]** : nom de votre société, comme vous souhaitez qu’il soit présenté au partenaire de destination. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination de résumé.](../../assets/catalog/advertising/liveramp-distribution/LR_Captify_DestSpecific.png)

* **[!UICONTROL Nom du client]** : nom de votre compte publicitaire, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination Cardlytics.](../../assets/catalog/advertising/liveramp-distribution/LR_Cardlytics_DestSpecific.png)

* **[!UICONTROL Nom du client]** : nom de votre compte publicitaire, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Accord sur les conditions de destination des données des annonceurs"
>abstract="Cochez `I AGREE` pour confirmer la reconnaissance et l’acceptation des conditions d’utilisation des données de l’annonceur Disney."

<!-- >additional-url="<https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/>" text="Read the agreement" -->

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Votre adresse e-mail"
>abstract="Saisissez une adresse e-mail liée à une personne. Cette adresse e-mail sert de signature pour l’accord des conditions de données des annonceurs. Cette adresse e-mail est également utilisée pour vous contacter si nécessaire."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination Disney.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Contrat de destination des données des annonceurs]** : saisissez `I AGREE` pour confirmer l’accusé de réception et l’accord avec les termes de données des annonceurs Disney.
* **[!UICONTROL Nom du client]** : saisissez le nom de votre société tel que vous souhaitez le présenter au partenaire de destination.
* **[!UICONTROL Adresse électronique]** : saisissez une adresse électronique liée à un individu. Cette adresse électronique sert de signature au contrat de termes de données de l’annonceur.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination iHeartMedia.](../../assets/catalog/advertising/liveramp-distribution/LR_iHeart_DestSpecific.png)

* **[!UICONTROL Nom du client]** : nom de votre compte publicitaire, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Index Exchange] {#index-exchange}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_index_advertiseraccountname"
>title="Nom de compte"
>abstract="Nom de votre compte clientèle Index Exchange. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination de l’Exchange d’index.](../../assets/catalog/advertising/liveramp-distribution/LR_IndexExchange_DestSpecific.png)

* **[!UICONTROL Nom du compte]** : nom du compte client de votre Exchange d’index. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Magnite CTV Platform] {#magnite}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitectv_client"
>title="client"
>abstract="Nom de votre client ou cliente, tel que vous souhaitez le présenter au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données client pour la destination Magnite CTV.](../../assets/catalog/advertising/liveramp-distribution/LR_MagniteCTV_DestSpecific.png)

* **[!UICONTROL Client]** : votre nom de client, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitedv+_partnerid"
>title="Identifiant du partenaire"
>abstract="Identifiant du partenaire de projet Rubicon associé à l’éditeur propriétaire du segment/des données. Contactez le représentant ou la représentante de votre compte de projet Rubicon si vous ne savez pas la valeur que vous devez utiliser."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitedv+_seatid"
>title="Identifiant du siège"
>abstract="Identifiant du siège Magnite DV+ fourni par votre personne gestionnaire de compte Magnite"

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données client pour la destination Magnite DV+.](../../assets/catalog/advertising/liveramp-distribution/LR_MagniteDV_DestSpecific.png)

* **[!UICONTROL Identifiant de partenaire]** : identifiant de partenaire de projet Rubicon associé à l’éditeur propriétaire du segment/des données. Contactez le représentant ou la représentante de votre compte de projet Rubicon si vous ne savez pas la valeur que vous devez utiliser.
* **[!UICONTROL ID de siège]** : ID de siège Magnite DV+ fourni par votre gestionnaire de compte Magnite

### [!DNL Nexxen (formerly known as [!DNL Amobee])] {#nexxen}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_ratetype"
>title="Type de tarif"
>abstract="Le type de tarif représente la manière dont l’utilisation des données doit être facturée. Tous les tarifs de 0,00 $ doivent être fixes. Contactez votre représentant ou représentante Nexxen si vous ne savez pas quel type de tarif utiliser."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_marketid"
>title="Identifiant du marché"
>abstract="Saisissez l’identifiant du marché numérique où le contrat de données Nexxen doit être créé. Si vous effectuez une syndication « AlwaysOn » sur tous les marchés de la plateforme Nexxen, saisissez -1."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_advertiserid"
>title="Identifiant annonceur"
>abstract="Si vous envoyez des données à un seul annonceur sur la plateforme Nexxen, saisissez l’identifiant d’annonceur Amobee numérique. Si vous souhaitez que les données soient disponibles pour tous les annonceurs sur un marché ou si ces segments sont « AlwaysOn », saisissez -1."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_contactemail"
>title="E-mail de contact"
>abstract="Saisissez l&#39;adresse e-mail que Nexxen doit utiliser pour envoyer les détails du contrat de données. Il s’agit probablement de votre propre adresse e-mail, mais il peut également s’agir d’un alias de messagerie. Pour plusieurs personnes destinataires, effectuez la séparation à l’aide de virgules (`email1@domain.com`, `email2@domain.com`, etc.)."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![ Image de l&#39;interface utilisateur de la plateforme montrant les champs de données du client pour la prochaine destination.](../../assets/catalog/advertising/liveramp-distribution/LR_Nexxen_DestSpecific.png)

* **[!UICONTROL Type de taux]** : le type de taux représente la façon dont l’utilisation des données doit être facturée. Tous les tarifs de 0,00 $ doivent être fixes. Contactez votre représentant ou représentante Nexxen si vous ne savez pas quel type de tarif utiliser.
* **[!UICONTROL ID de marché]** : saisissez l’ID de marché numérique dans lequel le contrat de données Suivant doit être créé. Si vous effectuez une syndication « AlwaysOn » sur tous les marchés de la plateforme Nexxen, saisissez -1.
* **[!UICONTROL Identifiant publicitaire]** : si vous envoyez des données à un seul annonceur sur la plateforme Nexxen, saisissez l’identifiant publicitaire Nexxen numérique. Si vous souhaitez que les données soient disponibles pour tous les annonceurs sur un marché ou si ces segments sont &quot;AlwaysOn&quot;, saisissez -1.
* **[!UICONTROL Contact Email]** : saisissez l’adresse email que Nexxen doit utiliser pour envoyer les détails du contrat de données. Il s’agit probablement de votre propre adresse e-mail, mais il peut également s’agir d’un alias de messagerie. Pour plusieurs destinataires, séparez-les par des virgules ( `email1@domain.com`, `email2@domain.com`).

### [!DNL One Fox] {#fox}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_fox_client"
>title="client"
>abstract="Nom de votre société/compte de distribution tel que vous souhaitez le voir apparaître pour le partenaire. Contactez le représentant ou la représentante de votre compte partenaire si vous ne savez pas quel nom utiliser. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination One Fox.](../../assets/catalog/advertising/liveramp-distribution/LR_Fox_DestSpecific.png)

* **[!UICONTROL Client]** : nom de votre société/compte de distribution tel que vous souhaitez le présenter au partenaire. Par défaut, utilisez le nom de votre société. Contactez le représentant ou la représentante de votre compte partenaire si vous ne savez pas quel nom utiliser. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Nom du compte"
>abstract="Nom de votre compte Pandora. Contactez le représentant ou la représentante de votre compte Pandora si vous ne savez pas quel est le nom de votre compte. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l&#39;interface utilisateur de Platform montrant les champs de données du client pour la destination Pandora.](../../assets/catalog/advertising/liveramp-distribution/LR_Pandora_DestSpecific.png)

* **[!UICONTROL Nom du compte]** : nom de votre compte Pandora. Contactez le représentant ou la représentante de votre compte Pandora si vous ne savez pas quel est le nom de votre compte. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Identifiant d’annonceur Reddit"
>abstract="Votre identifiant d’annonceur Reddit. Doit commencer par « t2_ » ou « a2_ ». Contactez le représentant ou la représentante de votre compte Reddit si vous ne connaissez pas votre identifiant d’annonceur."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Nom d&#39;annonceur Reddit"
>abstract="Votre nom d’annonceur Reddit. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données du client pour la destination Reddit.](../../assets/catalog/advertising/liveramp-distribution/LR_Reddit_DestSpecific.png)

* **[!UICONTROL Reddit advertiser ID]** : votre identifiant Reddit advertiser. Doit commencer par « t2_ » ou « a2_ ». Contactez le représentant ou la représentante de votre compte Reddit si vous ne connaissez pas votre identifiant d’annonceur.
* **[!UICONTROL Reddit advertiser name]** : nom de votre publicitaire Reddit. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Roku] {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="Adresse e-mail du compte Roku"
>abstract="Saisissez l’adresse e-mail liée à votre compte Roku."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="Adresse e-mail du représentant ou de la représentante du compte Roku"
>abstract="Saisissez l’adresse e-mail du représentant ou de la représentante de votre compte Roku. Cette adresse est utilisée pour envoyer des mises à jour de taxonomie. Pour saisir plusieurs adresses, séparez-les par des virgules."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les identifiants pris en charge pour la destination Roku.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Adresse électronique du compte Roku]** : saisissez l’adresse électronique liée à votre compte Roku.
* **[!UICONTROL Adresse électronique du représentant du compte Roku]** : saisissez l’adresse électronique de votre représentant du compte Roku. Pour saisir plusieurs adresses, séparez-les par des virgules.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les identifiants pris en charge pour la destination Spotify.](../../assets/catalog/advertising/liveramp-distribution/LR_Spotify_DestSpecific.png)

* **[!UICONTROL Nom du client]** : nom de votre compte publicitaire, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="Adresse e-mail du ou de la gestionnaire de compte"
>abstract="Adresse e-mail du ou de la gestionnaire de votre compte Taboola."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_seg_type"
>title="Type de segment"
>abstract="Type de segment. Seuls les segments propriétaires sont actuellement pris en charge."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les identifiants pris en charge pour la destination de tabola.](../../assets/catalog/advertising/liveramp-distribution/LR_Taboola_DestSpecific.png)

* **[!UICONTROL Adresse électronique du gestionnaire de compte]** : adresse électronique de votre gestionnaire de compte Taboola.
* **[!UICONTROL Type de segment]** : type de segment. Seuls les segments propriétaires sont actuellement pris en charge.

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les identifiants pris en charge pour la destination TargetSpot.](../../assets/catalog/advertising/liveramp-distribution/LR_TargetSpot_DestSpecific.png)

* **[!UICONTROL Nom du client]** : nom de votre compte publicitaire, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### [!DNL Teads] {#teads}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_teads_teadsid"
>title="ID de Teads"
>abstract="Identifiant de Teads"

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les identifiants pris en charge pour la destination TargetSpot.](../../assets/catalog/advertising/liveramp-distribution/LR_Teads_DestSpecific.png)

* **[!UICONTROL ID de teads]** : ID de vos Teads

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les identifiants pris en charge pour la destination de détection de flux de travaux.](../../assets/catalog/advertising/liveramp-distribution/LR_WBD_DestSpecific.png)

* **[!UICONTROL Nom du client]** : nom de votre compte publicitaire, comme vous souhaitez qu’il soit présenté au partenaire de destination. Utilisez le nom de votre société. N’utilisez ni espaces ni caractères spéciaux.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Pour recevoir des notifications sur l’état de votre flux de données, sélectionnez une alerte dans la liste. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

La connexion [!DNL LiveRamp - Distribution] active les audiences qui ont déjà été intégrées à votre compte LiveRamp par le biais de la connexion [LiveRamp - Intégration](liveramp-onboarding.md).

Pour activer correctement vos audiences, vous devez sélectionner les **mêmes audiences** que celles [précédemment intégrées](liveramp-onboarding.md) vers LiveRamp.

>[!IMPORTANT]
>
>La sélection d’audiences qui n’ont pas été intégrées auparavant par le biais de la connexion [LiveRamp - Intégration](liveramp-onboarding.md) ne déclenche pas l’intégration des nouvelles audiences.

## Données exportées / Valider l’exportation des données {#exported-data}

Pour vérifier et surveiller l’activation de vos audiences, connectez-vous à votre compte LiveRamp et vérifiez les mesures d’activation.

Si vous avez des questions sur l’activation de l’audience, contactez votre gestionnaire de compte LiveRamp.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur la configuration de votre destination [!DNL LiveRamp - Onboarding], consultez la [documentation LiveRamp - Intégration](liveramp-onboarding.md).
