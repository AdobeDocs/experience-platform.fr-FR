---
title: Créer une connexion Source Google Cloud Storage dans l’interface utilisateur
description: Découvrez comment créer une connexion source Google Cloud Storage à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 40%

---

# Créer une connexion source [!DNL Google Cloud Storage] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Google Cloud Storage] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Google Cloud Storage] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichiers suivants à ingérer à partir de stockages externes :

* Valeurs séparées par un délimiteur (DSV) : toute valeur à un seul caractère peut être utilisée comme délimiteur pour les fichiers de données au format DSV.
* JavaScript Object Notation (JSON) : les fichiers de données au format JSON doivent être conformes à XDM.
* Apache Parquet : les fichiers de données au format Parquet doivent être conformes à XDM.

### Collecter les informations d’identification requises

Pour accéder à vos données [!DNL Google Cloud Storage] sur Experience Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| Identifiant de la clé d’accès | Chaîne alphanumérique de 61 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] à Experience Platform. |
| Clé d’accès secrète | Chaîne codée en base 64 de 40 caractères utilisée pour authentifier votre compte [!DNL Google Cloud Storage] auprès d’Experience Platform. |
| Nom du compartiment | Nom de votre compartiment [!DNL Google Cloud Storage]. Vous devez spécifier un nom de compartiment si vous souhaitez fournir l’accès à un sous-dossier spécifique dans votre espace de stockage dans le cloud. |
| Chemin du dossier | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. |

Pour plus d’informations sur ces valeurs, consultez le guide [Clés HMAC de Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Pour savoir comment générer votre propre identifiant de clé d’accès et votre clé d’accès secrète, reportez-vous à la [[!DNL Google Cloud Storage] présentation](../../../../connectors/cloud-storage/google-cloud-storage.md).

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Google Cloud Storage] à Experience Platform.

## Connecter votre compte [!DNL Google Cloud Storage]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL Espace de stockage], sélectionnez **[!UICONTROL Espace de stockage Google]** puis **[!UICONTROL Ajouter des données]**.

![Écran de l’interface utilisateur d’Experience Platform affichant la page du catalogue des sources.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

La page **[!UICONTROL Se connecter à Google Cloud Storage]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Google Cloud Storage] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Écran de l’interface utilisateur d’Experience Platform affichant la page du compte existant pour une source Google Cloud Storage](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Google Cloud Storage]. Au cours de cette étape, vous pouvez également désigner les sous-dossiers auxquels votre compte aura accès en définissant le nom du chemin d’accès au sous-dossier.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Écran de l’interface utilisateur d’Experience Platform affichant la nouvelle page de compte pour une source Google Cloud Storage.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Google Cloud Storage]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de votre espace de stockage dans Experience Platform](../../dataflow/batch/cloud-storage.md).
