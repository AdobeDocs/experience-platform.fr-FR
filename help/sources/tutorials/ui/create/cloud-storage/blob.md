---
keywords: Experience Platform;accueil;rubriques populaires;Azure Blob;Azure Blob;connecteur Azure Blob
solution: Experience Platform
title: Création d’une connexion source Azure Blob dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer un connecteur source Azure Blob à l’aide de l’interface utilisateur de Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 39%

---

# Créez un [!DNL Azure Blob] connexion source dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Azure Blob] (ci-après dénommés &quot;[!DNL Blob]&quot;) à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Blob] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

- Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La valeur des en-têtes de champ des fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.
- Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être conformes à XDM.
- Apache Parquet : Les fichiers de données au format parquet doivent être conformes à XDM.

### Collecter les informations d’identification requises

Pour accéder à [!DNL Blob] sur Platform, vous devez fournir une valeur valide pour les informations d’identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne contenant les informations d’autorisation nécessaires à l’authentification [!DNL Blob] à Experience Platform. Le [!DNL Blob] Le modèle de chaîne de connexion est le suivant : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Pour plus d’informations sur les chaînes de connexion, voir [!DNL Blob] document on [configuration des chaînes de connexion](https://docs.microsoft.com/fr-fr/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre [!DNL Blob] compte . Le [!DNL Blob] Le modèle URI SAS est : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Pour plus d’informations, voir [!DNL Blob] document on [URI de signature d’accès partagé](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Connecter votre compte [!DNL Blob]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Blob] à Platform.

Dans l’[interface utilisateur de Platform](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à lʼespace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche plusieurs sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous , [!UICONTROL Stockage dans le cloud] catégorie, sélectionnez **[!UICONTROL Stockage Azure Blob]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/blob/catalog.png)

Le **[!UICONTROL Connexion au stockage Azure Blob]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Blob] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/blob/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description d’option pour votre nouvelle [!DNL Blob] compte .

**Authentification à l’aide d’une chaîne de connexion**

Le [!DNL Blob] Connector vous fournit différents types d’authentification pour l’accès. Sous [!UICONTROL Authentification du compte] select **[!UICONTROL ConnectionString]** pour utiliser des informations d’identification basées sur des chaînes.

![chaîne de connexion](../../../../images/tutorials/create/blob/connectionstring.png)

**Authentification à l’aide d’un URI de signature d’accès partagé**

Un URI de signature d’accès partagé (SAS) permet une délégation sécurisée des autorisations à votre [!DNL Blob] compte . Vous pouvez utiliser SAS pour créer des informations d’identification d’authentification avec des degrés d’accès différents, car une authentification SAS vous permet de définir des autorisations, des dates de début et d’expiration, ainsi que des dispositions sur des ressources spécifiques.

Sélectionner **[!UICONTROL SasURIAuthentication]** puis fournissez votre [!DNL Blob] URI SAS. Sélectionner **[!UICONTROL Connexion à la source]** pour continuer.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Blob]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Platform ;](../../dataflow/batch/cloud-storage.md).
