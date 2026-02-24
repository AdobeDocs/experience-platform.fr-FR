---
title: Connecteur de profil Pega
description: Utilisez le connecteur de profil Pega pour Amazon S3 dans Adobe Experience Platform pour exporter des données de profil complètes ou incrémentielles, ou les deux, vers l’espace de stockage dans le cloud d’Amazon S3. Dans Pega Customer Decision Hub, les tâches de données peuvent être planifiées dans Customer Profile Designer pour importer régulièrement des données de profil à partir du stockage Amazon S3.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 28%

---

# Connecteur de profil Pega

## Vue d’ensemble {#overview}

Utilisez le [!DNL Pega Profile Connector] dans Adobe Experience Platform pour créer une connexion sortante active vers votre stockage S3 [!DNL Amazon Web Services] (AWS) afin d’exporter périodiquement des données de profil vers des fichiers CSV à partir de Adobe Experience Platform dans vos propres compartiments S3. Dans [!DNL Pega Customer Decision Hub], vous pouvez planifier des tâches de données pour importer ces données de profil à partir du stockage S3 afin de mettre à jour le profil [!DNL Pega Customer Decision Hub].

Ce connecteur permet de configurer l’exportation initiale des données de profil et de synchroniser régulièrement les nouveaux profils dans [!DNL Pega Customer Decision Hub].  Disposer de données à jour dans Customer Decision Hub offre une vue meilleure et mise à jour de votre base de clients pour la prise de décision la plus appropriée.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par Pegasystems. Pour toute demande ou information, veuillez contacter Pega directement [ici](mailto:support@pega.com).

## Cas d’utilisation

Pour mieux comprendre quand et comment utiliser la destination [!DNL Pega Profile Connector], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation 1

Un spécialiste marketing souhaite configurer initialement des [!DNL Pega Customer Decision Hub] avec des données de profil chargées à partir de Adobe Experience Platform. Il s’agit d’une charge complète initiale suivie de charges delta selon un calendrier précis.

### Cas d’utilisation 2

Un spécialiste marketing souhaite que les données de profil Adobe Experience Platform à jour soient disponibles en [!DNL Pega Customer Decision Hub] afin d’améliorer de manière continue les informations Pega sur les profils clients.

## Conditions préalables {#prerequisites}

Avant de pouvoir utiliser cette destination pour exporter des données hors de Adobe Experience Platform et importer des profils dans [!DNL Pega Customer Decision Hub], veillez à remplir les conditions préalables suivantes :

* Configurez [!DNL Amazon S3] compartiment et le chemin d’accès au dossier à utiliser pour l’exportation et l’importation de fichiers de données.
* Configurez la clé d’accès [!DNL Amazon S3] et [!DNL Amazon S3] clé secrète : en [!DNL Amazon S3], générez une paire de `access key - secret access key` pour accorder à Experience Platform l’accès à votre compte [!DNL Amazon S3].
* Pour établir une connexion et exporter des données vers votre emplacement de stockage [!DNL Amazon S3], créez un utilisateur de gestion des identités et des accès (IAM) pour les [!DNL Experience Platform] dans [!DNL Amazon S3] et attribuez des autorisations telles que `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Assurez-vous que votre instance [!DNL Pega Customer Decision Hub] est mise à niveau vers la version 8.8 ou ultérieure.

## Identités prises en charge {#supported-identities}

[!DNL Pega Customer Decision Hub] prend en charge l’activation des ID utilisateur personnalisés décrits dans le tableau ci-dessous. Pour plus d’informations, voir [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description |
|---|---|
| *CustomerID* | Identifiant utilisateur commun qui identifie de manière unique un profil dans [!DNL Pega Customer Decision Hub] et Adobe Experience Platform |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Profile-based]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Batch]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

* Clé d’accès **[!DNL Amazon S3]** et clé secrète **[!DNL Amazon S3]** : dans [!DNL Amazon S3], générez une paire de `access key - secret access key` pour accorder à Adobe Experience Platform l’accès à votre compte [!DNL Amazon S3]. En savoir plus dans la [Documentation Amazon Web Services](https://docs.aws.amazon.com/fr_fr/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Renseigner les détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à [!DNL Amazon S3], fournissez les informations suivantes pour la destination :

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination du connecteur de profil Pega](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Next]**. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : saisissez une description de cette destination.
* **[!UICONTROL Bucket name]** : saisissez le nom de l’intervalle de [!DNL Amazon S3] à utiliser par cette destination.
* **[!UICONTROL Folder path]** : saisissez le chemin d’accès au dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL Compression Type]** : sélectionnez le type de compression GZIP ou AUCUN.

>[!TIP]
>
>Dans le workflow de connexion à la destination , vous pouvez créer un dossier personnalisé dans votre stockage Amazon S3 par fichier d’audience exporté. Lisez [Utiliser les macros pour créer un dossier à l’emplacement de stockage](/help/destinations/catalog/cloud-storage/overview.md#use-macros) pour obtenir des instructions.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [&#x200B; Activer les données d’audience vers des destinations d’exportation de profils par lots &#x200B;](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

L’étape **[!UICONTROL Mapping]** vous permet de sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activer l’interface utilisateur des destinations par lot.

## Valider l’exportation des données {#exported-data}

Pour les destinations [!DNL Pega Profile Connector], [!DNL Experience Platform] crée un fichier `.csv` à l’emplacement de stockage Amazon S3 que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activer les données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation des audiences.

Une importation réussie des données de profil à partir de S3 insère des données dans le magasin de données de profil [!DNL Pega Customer]. Les données de profil client importées peuvent être validées dans [!DNL Pega Customer Profile Designer] , comme le montre la figure suivante.
![Image de l’écran de l’interface utilisateur où vous pouvez valider les données de profil Adobe dans Customer Profile Designer](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

Dans [!DNL Pega Customer Decision Hub], les administrateurs de données peuvent configurer les tâches de données dans [!DNL Customer Profile Designer] pour importer régulièrement des données de profil à partir de S3, comme le montre la figure suivante. Consultez la [ressources supplémentaires](#additional-resources) pour plus d’informations sur la configuration des tâches de données afin d’importer des données de profil depuis [!DNL Amazon S3].
![Image de l’écran de l’interface utilisateur pour configurer les tâches de données dans le Designer du profil client](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Ressources supplémentaires {#additional-resources}

Voir [Importation de tâches de données](https://academy.pega.com/topic/import-data-jobs/v1) dans [!DNL Pega Customer Decision Hub].

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
