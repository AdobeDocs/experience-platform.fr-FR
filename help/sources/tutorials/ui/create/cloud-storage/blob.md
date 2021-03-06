---
keywords: Experience Platform;accueil;rubriques populaires;Azure Blob;Azure Blob;connecteur Azure Blob
solution: Experience Platform
title: Création d’une connexion source Azure Blob dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer un connecteur source Azure Blob à l’aide de l’interface utilisateur de Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 9%

---

# Création d’une connexion source [!DNL Azure Blob] dans l’interface utilisateur

Ce tutoriel décrit les étapes de création d’un [!DNL Azure Blob] (ci-après appelé &quot;[!DNL Blob]&quot;) à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Blob] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

- Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La valeur des en-têtes de champ des fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.
- Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être conformes à XDM.
- Apache Parquet : Les fichiers de données au format parquet doivent être conformes à XDM.

### Collecte des informations d’identification requises

Pour accéder à votre stockage [!DNL Blob] sur Platform, vous devez fournir une valeur valide pour les informations d’identification suivantes :

| Credential | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne contenant les informations d’autorisation nécessaires pour authentifier [!DNL Blob] auprès de l’Experience Platform. Le modèle de chaîne de connexion [!DNL Blob] est le suivant : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Pour plus d’informations sur les chaînes de connexion, consultez ce [!DNL Blob] document sur [la configuration des chaînes de connexion](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre compte [!DNL Blob]. Le modèle d’URI SAS [!DNL Blob] est le suivant : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Pour plus d’informations, consultez ce [!DNL Blob] document sur les [URI de signature d’accès partagé](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Connectez votre compte [!DNL Blob]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Blob] à Platform.

Dans l’ [interface utilisateur de la plateforme](https://platform.adobe.com), sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources] . L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Stockage cloud] , sélectionnez **[!UICONTROL Stockage Azure Blob]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/blob/catalog.png)

La page **[!UICONTROL Se connecter au stockage Azure Blob]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Blob] avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/blob/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description d’option pour votre nouveau compte [!DNL Blob].

**Authentification à l’aide d’une chaîne de connexion**

Le connecteur [!DNL Blob] vous fournit différents types d’authentification pour l’accès. Sous [!UICONTROL Authentification du compte] sélectionnez **[!UICONTROL ConnectionString]** pour utiliser les informations d’identification basées sur des chaînes de connexion.

![chaîne de connexion](../../../../images/tutorials/create/blob/connectionstring.png)

**Authentification à l’aide d’un URI de signature d’accès partagé**

Un URI de signature d’accès partagé (SAS) permet une délégation sécurisée de l’autorisation à votre compte [!DNL Blob]. Vous pouvez utiliser SAS pour créer des informations d’identification d’authentification avec des degrés d’accès différents, car une authentification SAS vous permet de définir des autorisations, des dates de début et d’expiration, ainsi que des dispositions sur des ressources spécifiques.

Sélectionnez **[!UICONTROL SasURIAuthentication]**, puis fournissez l’URI SAS [!DNL Blob]. Sélectionnez **[!UICONTROL Se connecter à la source]** pour continuer.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Blob]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Platform](../../dataflow/batch/cloud-storage.md).
