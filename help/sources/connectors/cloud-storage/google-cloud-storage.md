---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur d’Enregistrement Google Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Connecteur d’Enregistrement Google Cloud

Adobe Experience Platform fournit une connectivité native aux fournisseurs de cloud tels que AWS, [!DNL Google Cloud Platform]et [!DNL Azure]vous permet d’importer vos données à partir de ces systèmes.

Les sources d’enregistrement Cloud peuvent importer vos propres données [!DNL Platform] sans avoir à les télécharger, les mettre en forme ou les télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. [!DNL Platform] vous permet d’importer des données à partir de [!DNL Google Cloud Storage] lots.

## Configuration requise pour la connexion de votre [!DNL Google Cloud Storage] compte

Pour vous connecter à [!DNL Platform], vous devez d&#39;abord activer l&#39;interopérabilité pour votre [!DNL Google Cloud Storage] compte. Pour accéder au paramètre d’interopérabilité, ouvrez [!DNL Google Cloud Platform] et sélectionnez **[!UICONTROL Paramètres]** dans l’option **[!UICONTROL Enregistrement]** du panneau de navigation.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

La page **[!UICONTROL Paramètres]** s’affiche. A partir de là, vous pouvez voir des informations concernant l&#39;ID de votre [!DNL Google] projet et des détails sur votre [!DNL Google Cloud Storage] compte. Pour accéder aux paramètres d&#39;interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l&#39;en-tête supérieur.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La page **[!UICONTROL Interopérabilité]** contient des informations sur l’authentification, les clés d’accès et le projet par défaut associé à votre compte utilisateur. Si vous n&#39;avez pas encore établi de projet par défaut pour l&#39;accès interopérable, vous pouvez en configurer un dans la section *[!UICONTROL Par défaut pour l&#39;accès]* interopérable. Si un projet par défaut a déjà été établi, la section affiche la confirmation qu&#39;un projet a été défini comme projet par défaut.

Pour générer un nouvel ID de clé d’accès et une clé d’accès secret pour votre compte d’utilisateur, sélectionnez **[!UICONTROL Créer une clé]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d’accès nouvellement généré et votre clé d’accès secret pour connecter votre [!DNL Google Cloud Storage] compte à [!DNL Platform].

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Google Cloud Storage] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

## Se connecter [!DNL Google Cloud Storage] à [!DNL Platform]

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Google Cloud Storage] à [!DNL Platform] l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’un connecteur d’Enregistrement Google Cloud à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/google.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’un connecteur source d’Enregistrement Google Cloud dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)