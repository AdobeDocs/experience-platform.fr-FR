---
keywords: e-mail ; e-mail ; e-mail ; destinations e-mail ; oracle eloqua ; oracle
title: Oracle Eloqua
description: Oracle Eloqua est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par Oracle, qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
translation-type: tm+mt
source-git-commit: 29b4eaca06e2f1032584a0b4720490934a6e1fa7
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 30%

---

# [!DNL Oracle Eloqua] connexion

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/)[!DNL Oracle] est une plateforme de logiciel en tant que service (SaaS, Software as a service) pour l’automatisation du marketing proposée par , qui vise à aider les spécialistes marketing et les entreprises B2B à gérer les campagnes marketing et la génération de pistes commerciales.

Pour envoyer des données de segment à [!DNL Oracle Eloqua], vous devez tout d&#39;abord [connecter la destination](#connect-destination) à Adobe Experience Platform, puis [configurer une importation de données](#import-data-into-eloqua) à partir de votre emplacement d&#39;enregistrement dans [!DNL Oracle Eloqua].

## Type d&#39;exportation {#export-type}

**Basé sur**  le profil : vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom de famille), tel que choisi dans l’écran de sélection des attributs du processus [ d’activation de ](../../ui/activate-destinations.md#select-attributes)destination.

## LISTE AUTORISÉE d&#39;adresse IP {#allow-list}

Lors de la configuration de destinations de marketing par courriel avec l’enregistrement SFTP, l’Adobe vous recommande d’ajouter certaines plages d’adresses IP à votre liste autorisée.

Reportez-vous à la [liste autorisée d&#39;adresse IP pour les destinations d&#39;enregistrement cloud](../cloud-storage/ip-address-allow-list.md) si vous devez ajouter des adresses IP d&#39;Adobe à votre liste autorisée.

## Se connecter à la destination {#connect-destination}

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Oracle Eloqua], puis **[!UICONTROL Configurer]**.

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre [!UICONTROL Activer] et [!UICONTROL Configurer], consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

![Se connecter à Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

À l’étape **[!UICONTROL Compte]**, si vous aviez précédemment configuré une connexion à la destination de votre enregistrement cloud, sélectionnez **[!UICONTROL Compte existant]** et sélectionnez l’une de vos connexions existantes. Vous pouvez aussi sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion. Renseignez les informations d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. Pour [!DNL Oracle Eloqua], vous pouvez choisir entre **[!UICONTROL SFTP avec mot de passe]** et **[!UICONTROL SFTP avec clé SSH]**.

![Connecter un compte Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/connection-type.png)

Renseignez les informations ci-dessous en fonction du type de connexion, puis sélectionnez **[!UICONTROL Se connecter à la destination]**.

- Pour les connexions **[!UICONTROL SFTP avec mot de passe]**, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d&#39;utilisateur] et [!UICONTROL Mot de passe].
- Pour les connexions **[!UICONTROL SFTP avec la clé SSH]**, vous devez fournir [!UICONTROL Domaine], [!UICONTROL Port], [!UICONTROL Nom d&#39;utilisateur] et [!UICONTROL Clé SSH].

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement avec PGP/GPG à vos fichiers exportés sous la section **[!UICONTROL Clé]**. Votre clé publique doit être écrite en tant que chaîne codée [!DNL Base64].

![Eloqua se connecte à destination](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

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

![Informations de base sur Eloqua](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Cliquez sur **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus. Votre destination est maintenant créée et vous pouvez [activer des segments](../../ui/activate-destinations.md) vers la destination.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).

## Attributs de destination {#destination-attributes}

Lorsque [active des segments](../../ui/activate-destinations.md) vers la destination [!DNL Oracle Eloqua], l&#39;Adobe vous recommande de sélectionner un identifiant unique dans votre [schéma d&#39;union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination. Pour plus d’informations, voir [Sélectionner les champs de schéma à utiliser comme attributs de destination dans vos fichiers exportés](./overview.md#destination-attributes).

## Données exportées {#exported-data}

Pour les destinations [!DNL Oracle Eloqua], Platform crée un fichier délimité par des tabulations `.txt` ou `.csv` à l&#39;emplacement de l&#39;enregistrement que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Destinations du marketing par courriel et Destinations de l’enregistrement Cloud](../../ui/activate-destinations.md#esp-and-cloud-storage) dans le didacticiel sur l’activation des segments.

## Configurez l&#39;importation des données dans [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Après avoir connecté [!DNL Platform] à votre enregistrement SFTP, vous devez configurer l&#39;importation des données à partir de votre emplacement d&#39;enregistrement dans [!DNL Oracle Eloqua]. Pour savoir comment y parvenir, voir [Importation de contacts ou de comptes](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) dans le [!DNL Oracle Eloqua Help Center].
