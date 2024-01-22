---
title: Connecteur de profil Pega
description: Utilisez Pega Profile Connector for Amazon S3 dans Adobe Experience Platform pour exporter des données de profil complètes ou incrémentielles, ou les deux, vers l’espace de stockage dans le cloud Amazon S3. Dans Pega Customer Decision Hub, les tâches de données peuvent être planifiées dans Customer Profile Designer pour importer régulièrement des données de profil à partir du stockage Amazon S3.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 39%

---

# Connecteur de profil Pega

## Vue d’ensemble {#overview}

Utilisez la variable [!DNL Pega Profile Connector] dans Adobe Experience Platform pour créer une connexion sortante active à votre [!DNL Amazon Web Services] (AWS) Stockage S3 pour exporter périodiquement des données de profil vers des fichiers CSV à partir de Adobe Experience Platform dans vos propres compartiments S3. Dans [!DNL Pega Customer Decision Hub], vous pouvez planifier des tâches de données pour importer ces données de profil à partir du stockage S3 afin de mettre à jour le profil [!DNL Pega Customer Decision Hub].

Ce connecteur permet de configurer l’exportation initiale des données de profil et de synchroniser régulièrement les nouveaux profils dans [!DNL Pega Customer Decision Hub].  Disposer de données à jour dans Customer Decision Hub offre une vue meilleure et mise à jour de votre base de clients pour la prise de décision la plus adaptée.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et conservés par les systèmes Pegasystems. Pour toute demande d&#39;information ou de mise à jour, veuillez contacter directement Pega. [here](mailto:support@pega.com).

## Cas d’utilisation

Pour mieux comprendre comment et à quel moment utiliser la variable [!DNL Pega Profile Connector] destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation 1

Un marketeur souhaite commencer par configurer [!DNL Pega Customer Decision Hub] avec les données de profil chargées à partir de Adobe Experience Platform. Il s’agit d’une charge complète initiale suivie de chargements delta programmés.

### Cas d’utilisation 2

Un spécialiste du marketing souhaite que les données de profil à jour de Adobe Experience Platform soient disponibles dans [!DNL Pega Customer Decision Hub] qui améliore continuellement les informations Pega sur les profils client.

## Conditions préalables {#prerequisites}

Avant d’utiliser cette destination pour exporter des données en dehors de Adobe Experience Platform et importer des profils dans [!DNL Pega Customer Decision Hub], assurez-vous de remplir les conditions préalables suivantes :

* Configurer [!DNL Amazon S3] et le chemin d’accès au dossier à utiliser pour l’exportation et l’importation de fichiers de données.
* Configurez la variable [!DNL Amazon S3] clé d’accès et [!DNL Amazon S3] clé secrète : Dans [!DNL Amazon S3], générez une `access key - secret access key` pour accorder l’accès à Platform à votre [!DNL Amazon S3] compte .
* Pour établir une connexion et exporter des données vers [!DNL Amazon S3] emplacement de stockage, créez un utilisateur de gestion des identités et des accès (IAM) pour [!DNL Platform] in [!DNL Amazon S3] et attribuer des autorisations telles que `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Assurez-vous que les [!DNL Pega Customer Decision Hub] est mise à niveau vers la version 8.8 ou ultérieure.

## Identités prises en charge {#supported-identities}

[!DNL Pega Customer Decision Hub] prend en charge l’activation des ID utilisateur personnalisés décrits dans le tableau ci-dessous. Pour plus d’informations, voir [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| *CustomerID* | Identifiant utilisateur commun qui identifie de manière unique un profil dans [!DNL Pega Customer Decision Hub] et Adobe Experience Platform |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres d’un segment, ainsi que les champs de schéma de votre choix (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!DNL Amazon S3]clé d&#39;accès** et **[!DNL Amazon S3]clé secrète**: dans [!DNL Amazon S3], générez une `access key - secret access key` pour accorder à Adobe Experience Platform l’accès à [!DNL Amazon S3] compte . En savoir plus dans la [Documentation Amazon Web Services](https://docs.aws.amazon.com/fr_fr/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Renseigner les détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à [!DNL Amazon S3], fournissez les informations suivantes pour la destination :

![Image de l’écran de l’interface utilisateur affichant les champs renseignés pour les détails de destination du connecteur de profil Pega](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Suivant]**. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : saisissez un nom qui vous aidera à identifier cette destination.
* **[!UICONTROL Description]** : saisissez une description de cette destination.
* **[!UICONTROL Nom du compartiment]** : saisissez le nom du compartiment [!DNL Amazon S3] que cette destination doit utiliser.
* **[!UICONTROL Chemin du dossier]** : saisissez le chemin du dossier de destination qui hébergera les fichiers exportés.
* **[!UICONTROL Type de compression]**: sélectionnez le type de compression GZIP ou NONE.

>[!TIP]
>
>Dans le workflow de connexion à la destination, vous pouvez créer un dossier personnalisé dans le stockage Amazon S3 par fichier d’audience exporté. Lisez [Utiliser les macros pour créer un dossier à l’emplacement de stockage](/help/destinations/catalog/cloud-storage/overview.md#use-macros) pour obtenir des instructions.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

Dans l’étape **[!UICONTROL Mappage]**, vous pouvez sélectionner les champs d’attribut et d’identité à exporter pour vos profils. Vous pouvez également choisir de remplacer les en-têtes du fichier exporté par un nom convivial de votre choix. Pour plus d’informations, voir l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) dans le tutoriel Activer l’interface utilisateur des destinations par lot.

## Valider l’exportation des données {#exported-data}

Pour [!DNL Pega Profile Connector] destinations, [!DNL Platform] crée une `.csv` dans l’emplacement de stockage Amazon S3 que vous avez fourni. Pour plus d’informations sur les fichiers, voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](../../ui/activate-batch-profile-destinations.md) dans le tutoriel sur l’activation de l’audience.

Une importation réussie des données de profil à partir de S3 insère des données dans la variable [!DNL Pega Customer] banque de données de profil. Les données de profil client importées peuvent être validées dans [!DNL Pega Customer Profile Designer] , comme illustré dans la figure suivante.
![Image de l’écran de l’interface utilisateur dans lequel vous pouvez valider les données de profil d’Adobe dans le Concepteur de profil client](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

Dans [!DNL Pega Customer Decision Hub], les administrateurs de données peuvent configurer des tâches de données dans [!DNL Customer Profile Designer] pour importer régulièrement des données de profil à partir de S3, comme illustré dans la figure suivante. Voir [ressources supplémentaires](#additional-resources) pour plus d’informations sur la configuration de tâches de données à partir desquelles importer des données de profil [!DNL Amazon S3].
![Image de l’écran de l’interface utilisateur pour configurer les tâches de données dans le Concepteur de profil client](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Ressources supplémentaires {#additional-resources}

Voir [Importation de traitements de données](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
