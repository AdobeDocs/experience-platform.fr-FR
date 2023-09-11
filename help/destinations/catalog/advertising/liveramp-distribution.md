---
title: LiveRamp - Connexion de distribution
description: Découvrez comment utiliser le connecteur LiveRamp - Distribution pour activer les audiences précédemment intégrées à LiveRamp, vers d’autres destinations publicitaires.
hide: true
hidefromtoc: true
source-git-commit: c04c7ff4f1ab45d944f4ab516d7842df536fae40
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 60%

---


# Connexion [!DNL LiveRamp - Distribution] {#liveramp-onboarding}

La variable [!DNL LiveRamp - Distribution] La connexion vous permet d’activer les audiences des éditeurs Experience Platform aux éditeurs Premium sur les médias mobiles, web, d’affichage et de télévision connectés.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par LiveRamp. Pour toute question ou demande de mise à jour, contactez directement LiveRamp [here](mailto:example@email.com).

## Destinations prises en charge {#supported-destinations}

[!DNL LiveRamp - Distribution] prend actuellement en charge l’activation de l’audience sur les plateformes suivantes :

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL LiveRamp - Distribution], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

L’équipe marketing d’un détaillant de vêtements de sport a utilisé la variable [LiveRamp - Intégration](liveramp-onboarding.md) connexion pour envoyer des audiences d’Experience Platform vers leur compte LiveRamp.

Par le biais de la [!DNL LiveRamp - Distribution] connexion ils peuvent désormais déclencher l’activation des audiences intégrées vers les destinations mentionnées dans la partie supérieure de cette page, de sorte qu’ils puissent cibler les utilisateurs sur mobile, sur le web ouvert, sur les réseaux sociaux et [!DNL CTV] plateformes.

## Audiences intégrées à LiveRamp {#onboarding}

Avant d’activer des audiences via le [!DNL LiveRamp - Distribution] connexion, utilisez [LiveRamp - Intégration](liveramp-onboarding.md) connexion pour exporter vos audiences Experience Platform vers LiveRamp.

Une fois les audiences intégrées à LiveRamp, continuez le processus d’activation à partir de la [se connecter à la destination](#connect) étape .

## Se connecter à la destination {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Paramètres d’identifiant"
>abstract="Sélectionnez les identifiants pris en charge par votre destination. Consultez la documentation pour obtenir la liste complète des identifiants pris en charge pour chaque destination."

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Authentification à LiveRamp {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Image de l’interface utilisateur de Platform affichant l’écran de connexion de destination.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL URL du jeton]**: votre URL de jeton LiveRamp.
* **[!UICONTROL ID d’organisation LiveRamp]**: ID d’organisation de votre compte LiveRamp.
* **[!UICONTROL Nom d’utilisateur]**: votre nom d’utilisateur de compte LiveRamp.
* **[!UICONTROL Password]**: mot de passe de votre compte LiveRamp.

### Configuration des détails de destination {#destination-details}

Une fois que vous êtes connecté à votre compte LiveRamp, saisissez les informations requises pour vous connecter à la destination vers laquelle vous souhaitez activer les audiences.

![Image de l’interface utilisateur de Platform affichant l’écran des détails de la destination.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Nom]**: renseignez le nom de votre choix pour la connexion à la destination.
* **[!UICONTROL Description]** : saisissez une description pour votre destination. Utilisez une description qui vous aidera à identifier facilement l’objectif de cette destination.
* **[!UICONTROL Destination]**: utilisez le menu déroulant pour sélectionner la destination vers laquelle vous souhaitez activer les audiences. La destination sélectionnée ici affecte directement ce que vous voyez dans la variable [paramètres spécifiques à la destination](#destination-settings) écran.
* **[!UICONTROL Intégration]**: sélectionnez le compte d’intégration à utiliser pour votre destination.
* **[!UICONTROL Identifiant]**: sélectionnez les identifiants pris en charge par votre destination. Actuellement, les identifiants pris en charge de toutes les destinations sont préremplis dans le menu déroulant.

## Paramètres spécifiques à la destination {#destination-settings}

Chacune des destinations [pris en charge](#supported-destinations) par [!DNL LiveRamp - Onboarding] nécessite de renseigner des options de configuration spécifiques.

Consultez les sections ci-dessous pour obtenir des instructions détaillées sur la configuration de chaque destination.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="Identifiant de profil de marque 4C"
>abstract="Saisissez l’identifiant numérique associé à votre profil de marque 4C. Si vous ne disposez pas de cet identifiant, contactez votre représentant ou représentante des services à la clientèle 4C."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Accord sur les conditions de destination des données des annonceurs"
>abstract="Cochez `I AGREE` pour confirmer la reconnaissance et l’acceptation des conditions d’utilisation des données de l’annonceur Disney."
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Lire l’accord"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Votre adresse e-mail"
>abstract="Saisissez une adresse e-mail liée à une personne. Cette adresse e-mail sert de signature pour l’accord des conditions de données des annonceurs. Cette adresse e-mail sera également utilisée pour vous contacter si nécessaire."

Pour configurer les détails de la destination, renseignez les champs ci-dessous.

![Image de l’interface utilisateur de Platform montrant les champs de données client pour la destination Disney.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Contrat des termes de destination des données du annonceur]**: saisissez `I AGREE` pour confirmer l’accusé de réception et l’accord avec les termes de données de l’annonceur Disney.
* **[!UICONTROL Nom du client]**: saisissez le nom de votre société tel que vous souhaitez le présenter au partenaire de destination.
* **[!UICONTROL Adresse électronique]**: saisissez une adresse électronique liée à un individu. Cette adresse e-mail sert de signature pour l’accord des conditions de données des annonceurs.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="Nom du fournisseur de données"
>abstract="Nom de votre entreprise tel que vous souhaitez le montrer à Pandora. Le nom peut contenir, au maximum, 40 caractères minuscules et alphanumériques (par exemple, My_Company)."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="Adresse e-mail du représentant ou de la représentante du compte"
>abstract="Adresse e-mail du représentant ou de la représentante de votre compte Pandora. Cette adresse est utilisée pour envoyer des mises à jour de taxonomie. Pour saisir plusieurs adresses, séparez-les par des virgules."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="Adresse e-mail"
>abstract="Cette adresse est utilisée pour envoyer des mises à jour de taxonomie. Pour saisir plusieurs adresses, séparez-les par des virgules."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Nom du compte"
>abstract="Nom de votre compte Pandora. Contactez le représentant ou la représentante de votre compte Pandora si vous ne savez pas quel est le nom de votre compte. N&#39;utilisez ni espaces ni caractères spéciaux."

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Identifiant d’annonceur Reddit"
>abstract="Votre identifiant d’annonceur Reddit. Doit commencer par « t2_ » ou « a2_ ». Contactez le représentant ou la représentante de votre compte Reddit si vous ne connaissez pas votre identifiant d’annonceur."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Nom d&#39;annonceur Reddit"
>abstract="Votre nom d’annonceur Reddit. N&#39;utilisez ni espaces ni caractères spéciaux."

### Roku {#roku}

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

* **[!UICONTROL Adresse électronique du compte Roku]**: saisissez l’adresse électronique associée à votre compte Roku.
* **[!UICONTROL Adresse électronique du représentant du compte Roku]**: saisissez l’adresse électronique du représentant de votre compte Roku. Pour saisir plusieurs adresses, séparez-les par des virgules.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="Jeton de compte"
>abstract="Identifiant alphanumérique qui informe Spotify où porter les données et que l’utilisation de ce workflow est vérifiée. Contactez le ou la gestionnaire de votre compte Spotify pour obtenir ce jeton."

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="Adresse e-mail du ou de la gestionnaire de compte"
>abstract="Adresse e-mail du ou de la gestionnaire de votre compte Taboola."

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Nom du client ou de la cliente"
>abstract="Nom de votre compte publicitaire, tel que vous souhaitez le présenter au partenaire ou à la partenaire de destination. Utilisez le nom de votre société. N&#39;utilisez ni espaces ni caractères spéciaux."

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

La variable [!DNL LiveRamp - Distribution] La connexion active les audiences qui ont déjà été intégrées à votre compte LiveRamp via le [LiveRamp - Intégration](liveramp-onboarding.md) connexion.

Pour activer correctement vos audiences, vous devez, à cette étape, sélectionner la variable **mêmes audiences** que vous avez précédemment intégré à LiveRamp.

>[!IMPORTANT]
>
>La sélection d’audiences qui n’ont pas été intégrées à LiveRamp ne déclenche pas l’intégration des nouvelles audiences.

## Données exportées / Valider l’exportation des données {#exported-data}

Pour vérifier et surveiller l’activation de vos audiences, connectez-vous à votre compte LiveRamp et vérifiez les mesures d’activation.

Si vous avez des questions sur l’activation de l’audience, contactez votre gestionnaire de compte LiveRamp.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur la configuration de votre stockage [!DNL LiveRamp - Onboarding], consultez la [documentation officielle](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
