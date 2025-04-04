---
title: Créer une connexion Source Azure Blob dans l’interface utilisateur
description: Découvrez comment créer un connecteur source Azure Blob à l’aide de l’interface utilisateur Experience Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 25%

---

# Créer une connexion source [!DNL Azure Blob] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Azure Blob] (ci-après dénommée « [!DNL Blob] ») à l’aide de l’interface utilisateur d’Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : cadre normalisé pour organiser les données d’expérience client dans Experience Platform.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Blob] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

Experience Platform prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

* Valeurs séparées par un délimiteur (DSV) : vous pouvez utiliser n’importe quel délimiteur de colonne unique, tel qu’une tabulation, une virgule, une barre verticale, un point-virgule ou un hachage pour collecter des fichiers plats dans n’importe quel format.
* JavaScript Object Notation (JSON) : les fichiers de données au format JSON doivent être conformes à XDM.
* Apache Parquet : les fichiers de données au format Parquet doivent être conformes à XDM.

### Collecter les informations d’identification requises

Pour accéder à votre stockage [!DNL Blob] sur Experience Platform, vous devez fournir des valeurs valides pour les informations d’identification suivantes :

>[!BEGINTABS]

>[!TAB Authentification de chaîne de connexion]

| Informations d’identification | Description |
| --- | --- |
| Chaîne de connexion | Chaîne contenant les informations d’autorisation nécessaires pour authentifier les [!DNL Blob] dans Experience Platform. Le modèle de chaîne de connexion [!DNL Blob] est : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Pour plus d’informations sur les chaînes de connexion, consultez ce document [!DNL Blob] sur la [configuration des chaînes de connexion](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB authentification URI SAS]

| Informations d’identification | Description |
| --- | --- |
| URI SAS | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre compte [!DNL Blob]. Le modèle d’URI SAS [!DNL Blob] est le suivant : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Pour plus d’informations, consultez ce document [!DNL Blob] sur les [URI de signature à accès partagé](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Conteneur | Nom du conteneur auquel vous souhaitez désigner l’accès. Lors de la création d’un compte avec la source de [!DNL Blob], vous pouvez fournir un nom de conteneur pour spécifier l’accès utilisateur au sous-dossier de votre choix. |
| Chemin du dossier | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |

>[!ENDTABS]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour connecter votre espace de stockage [!DNL Blob] à Experience Platform

## Connecter votre compte [!DNL Blob]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Stockage dans le cloud], sélectionnez **[!UICONTROL Stockage Azure Blob]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources Experience Platform avec la source de stockage Blob Azure sélectionnée.](../../../../images/tutorials/create/blob/catalog.png)

La page **[!UICONTROL Se connecter au stockage Azure Blob]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Blob] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/blob/existing.png)

### Nouveau compte

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL Blob]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative pour votre nouveau compte [!DNL Blob].

![Écran du nouveau compte pour la source de stockage Blob Azure.](../../../../images/tutorials/create/blob/new.png)

La source [!DNL Blob] prend en charge l’authentification par clé de compte et l’authentification par signature d’accès partagé (SAS). Une authentification par clé de compte nécessite une chaîne de connexion pour la vérification, tandis qu’une authentification SAS utilise un URI qui permet une autorisation déléguée sécurisée de votre compte.

Au cours de cette étape, vous pouvez également désigner les sous-dossiers auxquels votre compte aura accès en définissant le nom du conteneur et le chemin d’accès au sous-dossier.

>[!BEGINTABS]

>[!TAB Chaîne de connexion]

Pour vous authentifier à l’aide d’une clé de compte, sélectionnez **[!UICONTROL Authentification par clé de compte]** et fournissez votre chaîne de connexion. Au cours de cette étape, vous pouvez également désigner le nom du conteneur et le chemin d’accès au sous-dossier auquel vous souhaitez accéder. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**.

![ chaîne de connexion ](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS ]

Vous pouvez utiliser SAS pour créer des informations d’identification d’authentification avec différents degrés d’accès, car une authentification SAS vous permet de définir des autorisations, des dates de début et d’expiration, ainsi que des dispositions pour des ressources spécifiques.

Pour vous authentifier avec une signature d’accès partagé, sélectionnez **[!UICONTROL Authentification de signature d’accès partagé]** puis fournissez votre URI SAS. Au cours de cette étape, vous pouvez également désigner le nom du conteneur et le chemin d’accès au sous-dossier auquel vous souhaitez accéder. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Blob]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de votre espace de stockage dans Experience Platform](../../dataflow/batch/cloud-storage.md).
