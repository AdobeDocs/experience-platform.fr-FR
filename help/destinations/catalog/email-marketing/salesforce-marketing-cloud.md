---
keywords: e-mail ; e-mail ; e-mail ; destinations e-mail ; salesforce ; destination salesforce
title: Connexion Marketing Cloud Salesforce
seo-description: Salesforce Marketing Cloud est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 33%

---


# [!DNL Salesforce Marketing Cloud] connexion

## Présentation {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/fr/products/marketing-cloud/email-marketing/) est une suite de marketing numérique anciennement connue sous le nom d’ExactTarget qui vous permet de créer et de personnaliser les parcours des visiteurs et des clients afin d’offrir une expérience personnalisée.

Pour envoyer des données de segment à [!DNL Salesforce Marketing Cloud], vous devez tout d&#39;abord [connecter la destination](#connect-destination) dans la plate-forme, puis [configurer une importation de données](#import-data-into-salesforce) à partir de votre emplacement d&#39;enregistrement dans [!DNL Salesforce Marketing Cloud].

## Type d&#39;exportation {#export-type}

**Basé sur**  le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [ d’activation de ](../../ui/activate-destinations.md#select-attributes)destination.

## Connexion à la destination {#connect-destination}

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Salesforce Marketing Cloud], puis **[!UICONTROL Configurer]**.

![Connexion à Salesforce](../../assets/catalog/email-marketing/salesforce/catalog.png)

À l’étape **[!UICONTROL Compte]**, si vous aviez précédemment configuré une connexion à la destination de votre enregistrement cloud, sélectionnez **[!UICONTROL Compte existant]** et sélectionnez l’une de vos connexions existantes. Vous pouvez aussi sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion. Renseignez les informations d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. Pour [!DNL Salesforce Marketing Cloud], vous pouvez choisir entre **[!UICONTROL SFTP avec mot de passe]** et **[!UICONTROL SFTP avec clé SSH]**.

![Connecter le compte de Marketing Cloud Salesforce](../../assets/catalog/email-marketing/salesforce/connection-type.png)

Renseignez les informations ci-dessous, en fonction du type de connexion, et sélectionnez **[!UICONTROL Configurer]**.

- Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d&#39;utilisateur] et [!UICONTROL Mot de passe].
- Pour les connexions **[!UICONTROL SFTP avec la clé SSH]**, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d&#39;utilisateur] et [!UICONTROL Clé SSH].

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]**. Votre clé publique doit être écrite en tant que chaîne codée [!DNL Base64].

![Renseignement des informations sur Salesforce](../../assets/catalog/email-marketing/salesforce/account-info.png)

À l’étape **[!UICONTROL Authentification]**, renseignez les informations appropriées pour votre destination, comme indiqué ci-dessous :
- **[!UICONTROL Nom]** : choisissez un nom pertinent pour votre destination.
- **[!UICONTROL Description]** : saisissez une description pour votre destination.
- **[!UICONTROL Chemin]** du dossier : Indiquez le chemin d’accès à l’emplacement de votre enregistrement où Platform déposera vos données d’exportation au format CSV ou tabulé.
- **[!UICONTROL Format du fichier]** : **CSV** ou **séparé par des tabulations**. Sélectionnez le format du fichier à exporter vers l’emplacement de stockage.
- **[!UICONTROL Actions]** marketing : Les actions marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer votre propre action marketing. Pour plus d&#39;informations sur les actions marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Informations de base sur Salesforce](../../assets/catalog/email-marketing/salesforce/basic-information.png)

Cliquez sur **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus. Votre destination est maintenant connectée et vous pouvez [activer des segments](../../ui/activate-destinations.md) vers la destination.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).

## Attributs de destination {#destination-attributes}

Lorsque [active des segments](../../ui/activate-destinations.md) vers la destination [!DNL Salesforce Marketing Cloud], l&#39;Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d&#39;union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](./overview.md#destination-attributes).

## Données exportées {#exported-data}

Pour les destinations [!DNL Salesforce Marketing Cloud], Platform crée un fichier délimité par des tabulations `.txt` ou `.csv` à l&#39;emplacement de l&#39;enregistrement que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Destinations du marketing par courriel et Destinations de l’enregistrement Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) dans le didacticiel sur l’activation des segments.

## Configurez l&#39;importation des données dans [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Après avoir connecté [!DNL Platform] à votre enregistrement SFTP, vous devez configurer l&#39;importation des données à partir de votre emplacement d&#39;enregistrement dans [!DNL Salesforce Marketing Cloud]. Pour savoir comment y parvenir, voir [Importation d&#39;abonnés dans un Marketing Cloud à partir d&#39;un fichier ](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) dans le [!DNL Salesforce Help Center].