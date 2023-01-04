---
keywords: Experience Platform;accueil;rubriques les plus consultées;espace de stockage Google;stockage dans le cloud Google;GCS;gcs
solution: Experience Platform
title: Création d’une connexion à la source de stockage dans le cloud Google dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source de stockage dans le cloud Google à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 39%

---

# Créer une connexion source [!DNL Google Cloud Storage] dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’ingérer des données externes selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Google Cloud Storage] (ci-après appelé &quot;GCS&quot;) Connecteur source à l’aide de la méthode [!DNL Platform] de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion GCS valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

* Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La valeur des en-têtes de champ des fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.
* Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être conformes à XDM.
* Apache Parquet : Les fichiers de données au format parquet doivent être conformes à XDM.

### Collecter les informations d’identification requises

Pour accéder à vos données GCS sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Accès à l’ID de clé | Chaîne alphanumérique de 61 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte à Platform. |
| Clé d’accès secrète | Chaîne codée en base 64 caractères de 40 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte à Platform. |

Pour plus d’informations sur ces valeurs, consultez le guide [Clés HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre identifiant de clé d’accès et votre clé d’accès secrète, reportez-vous à la section [[!DNL Google Cloud Storage] Présentation de la ](../../../../connectors/cloud-storage/google-cloud-storage.md).

## Connecter votre compte [!DNL Google Cloud Storage]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte GCS à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Sources]** workspace. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Bases de données]** catégorie, sélectionnez **[!UICONTROL Stockage dans le cloud Google]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur GCS.

![catalogue](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Le **[!UICONTROL Connexion à Google Cloud Storage]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification GCS. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte GCS auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte GCS. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
