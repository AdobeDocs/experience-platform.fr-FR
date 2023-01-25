---
title: Création d’une connexion à la source de stockage dans le cloud Google dans l’interface utilisateur
description: Découvrez comment créer une connexion source de stockage dans le cloud Google à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 49%

---

# Créer une connexion source [!DNL Google Cloud Storage] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Google Cloud Storage] connexion source à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Google Cloud Storage] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

* Valeurs séparées par des délimiteurs (DSV) : N’importe quelle valeur de caractère unique peut être utilisée comme délimiteur pour les fichiers de données au format DSV.
* Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être conformes à XDM.
* Apache Parquet : Les fichiers de données au format parquet doivent être conformes à XDM.

### Collecter les informations d’identification requises

Pour accéder à [!DNL Google Cloud Storage] sur Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Accès à l’ID de clé | Chaîne alphanumérique de 61 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte à Platform. |
| Clé d’accès secrète | Chaîne codée en base 64 caractères de 40 caractères utilisée pour authentifier votre [!DNL Google Cloud Storage] compte à Platform. |
| Nom du compartiment | Le nom de votre [!DNL Google Cloud Storage] du compartiment. Vous devez spécifier un nom de compartiment si vous souhaitez accorder l’accès à un sous-dossier spécifique de votre espace de stockage dans le cloud. |
| Chemin du dossier | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |

Pour plus d’informations sur ces valeurs, consultez le guide [Clés HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre identifiant de clé d’accès et votre clé d’accès secrète, reportez-vous à la section [[!DNL Google Cloud Storage] Présentation de la ](../../../../connectors/cloud-storage/google-cloud-storage.md).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre la procédure ci-dessous et lier votre compte [!DNL Google Cloud Storage] à Platform.

## Connecter votre compte [!DNL Google Cloud Storage]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL Stockage dans le cloud] catégorie, sélectionnez **[!UICONTROL Stockage dans le cloud Google]** puis sélectionnez **[!UICONTROL Ajouter des données]**.

![L’écran de l’interface utilisateur de Platform affiche la page du catalogue des sources.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Le **[!UICONTROL Connexion à Google Cloud Storage]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Google Cloud Storage] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![L’écran de l’interface utilisateur de Platform affichant la page de compte existante pour une source de stockage dans le cloud Google](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL Google Cloud Storage] informations d’identification. Au cours de cette étape, vous pouvez également désigner les sous-dossiers auxquels votre compte aura accès en définissant le nom du chemin d’accès au sous-dossier.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![L’écran de l’interface utilisateur de Platform affichant la nouvelle page de compte pour une source de stockage dans le cloud Google.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Google Cloud Storage]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Platform ;](../../dataflow/batch/cloud-storage.md).
