---
title: Création d’une connexion source Azure Blob dans l’interface utilisateur
description: Découvrez comment créer un connecteur source Azure Blob à l’aide de l’interface utilisateur de Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 30%

---

# Créez un [!DNL Azure Blob] connexion source dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Azure Blob] (ci-après dénommés &quot;[!DNL Blob]&quot;) connexion source à l’aide de l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md): Cadre normalisé pour l’organisation des données d’expérience client dans Experience Platform.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Blob] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

Experience Platform prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

* Valeurs séparées par des délimiteurs (DSV) : Vous pouvez utiliser n’importe quel délimiteur de colonne, tel qu’une tabulation, une virgule, une barre verticale, un point-virgule ou un hachage, pour collecter des fichiers plats dans n’importe quel format.
* Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être conformes à XDM.
* Apache Parquet : Les fichiers de données au format parquet doivent être conformes à XDM.

### Collecter les informations d’identification requises

Pour accéder à [!DNL Blob] sur Platform, vous devez fournir une valeur valide pour les informations d’identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Chaîne de connexion | Chaîne contenant les informations d’autorisation nécessaires à l’authentification [!DNL Blob] à Experience Platform. Le [!DNL Blob] Le modèle de chaîne de connexion est le suivant : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Pour plus d’informations sur les chaînes de connexion, voir [!DNL Blob] document on [configuration des chaînes de connexion](https://docs.microsoft.com/fr-fr/azure/storage/common/storage-configure-connection-string). |
| URI SAS | URI de signature d’accès partagé que vous pouvez utiliser comme autre type d’authentification pour connecter votre [!DNL Blob] compte . Le [!DNL Blob] Le modèle URI SAS est : `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Pour plus d’informations, voir [!DNL Blob] document on [URI de signature d’accès partagé](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Conteneur | Nom du conteneur auquel vous souhaitez attribuer l’accès. Lors de la création d’un compte avec l’événement [!DNL Blob] source, vous pouvez fournir un nom de conteneur pour spécifier l’accès utilisateur au sous-dossier de votre choix. |
| Chemin du dossier | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Blob] à Platform.

## Connecter votre compte [!DNL Blob]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également sélectionner la source de votre choix à l’aide de la barre de recherche.

Sous , [!UICONTROL Stockage dans le cloud] catégorie, sélectionnez **[!UICONTROL Stockage Azure Blob]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources Experience Platform avec la source de stockage Azure Blob sélectionnée.](../../../../images/tutorials/create/blob/catalog.png)

Le **[!UICONTROL Connexion au stockage Azure Blob]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Blob] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/blob/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouvelle [!DNL Blob] compte .

![Nouvel écran du compte pour la source de stockage Azure Blob.](../../../../images/tutorials/create/blob/new.png)

Le [!DNL Blob] source prend en charge l’authentification par clé de compte et l’authentification par signature d’accès partagée (SAS). Une authentification par clé de compte nécessite une chaîne de connexion pour la vérification, tandis qu’une authentification SAS utilise un URI qui permet une autorisation déléguée sécurisée de votre compte.

Au cours de cette étape, vous pouvez également désigner les sous-dossiers auxquels votre compte aura accès en définissant le nom du conteneur et le chemin d’accès au sous-dossier.

>[!BEGINTABS]

>[!TAB Chaîne de connexion]

Pour vous authentifier à l’aide d’une clé de compte, sélectionnez **[!UICONTROL Authentification par clé de compte]** et indiquez votre chaîne de connexion. Au cours de cette étape, vous pouvez également désigner le nom du conteneur et le chemin d’accès au sous-dossier auquel vous souhaitez accéder. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**.

![chaîne de connexion](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS]

Vous pouvez utiliser SAS pour créer des informations d’identification d’authentification avec des degrés d’accès différents, car une authentification SAS vous permet de définir des autorisations, des dates de début et d’expiration, ainsi que des dispositions sur des ressources spécifiques.

Pour vous authentifier avec une signature d’accès partagé, sélectionnez **[!UICONTROL Authentification de signature d’accès partagé]** puis fournissez votre URI SAS. Au cours de cette étape, vous pouvez également désigner le nom du conteneur et le chemin d’accès au sous-dossier auquel vous souhaitez accéder. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Blob]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Platform ;](../../dataflow/batch/cloud-storage.md).
