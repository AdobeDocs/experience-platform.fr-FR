---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connecteur d’Enregistrement Google Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Connecteur d’Enregistrement Google Cloud

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de cloud tels que AWS, Google Cloud Platform et Azure, ce qui vous permet d’importer vos données à partir de ces systèmes.

Les sources d’enregistrement Cloud peuvent importer vos propres données dans Platform sans avoir à télécharger, mettre en forme ou télécharger. Les données insérées peuvent être formatées sous la forme XDM JSON, XDM parquet ou délimitées. Chaque étape du processus est intégrée dans le processus Sources. Plateforme vous permet d’importer des données de l’Enregistrement Google Cloud par lots.

## Configuration requise pour la connexion de votre compte d’Enregistrement Google Cloud

Pour vous connecter à la plate-forme, vous devez d’abord activer l’interopérabilité pour votre compte d’Enregistrement Google Cloud. Pour accéder au paramètre d’interopérabilité, ouvrez la plate-forme Google Cloud et sélectionnez **[!UICONTROL Paramètres]** dans l’option **[!UICONTROL Enregistrement]** du panneau de navigation.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

La page **[!UICONTROL Paramètres]** s’affiche. Vous trouverez ici des informations concernant votre ID de projet Google et des détails sur votre compte d’Enregistrement Google Cloud. Pour accéder aux paramètres d&#39;interopérabilité, sélectionnez **[!UICONTROL Interopérabilité]** dans l&#39;en-tête supérieur.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La page **[!UICONTROL Interopérabilité]** contient des informations sur l’authentification, les clés d’accès et le projet par défaut associé à votre compte utilisateur. Si vous n&#39;avez pas encore établi de projet par défaut pour l&#39;accès interopérable, vous pouvez en configurer un dans la section *[!UICONTROL Par défaut pour l&#39;accès]* interopérable. Si un projet par défaut a déjà été établi, la section affiche la confirmation qu&#39;un projet a été défini comme projet par défaut.

Pour générer un nouvel ID de clé d’accès et une clé d’accès secret pour votre compte d’utilisateur, sélectionnez **[!UICONTROL Créer une clé]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Vous pouvez utiliser votre identifiant de clé d’accès nouvellement généré et votre clé d’accès secret pour connecter votre compte d’Enregistrement Google Cloud à la plate-forme.

La documentation ci-dessous fournit des informations sur la connexion de l’Enregistrement Google Cloud à la plate-forme à l’aide des API ou de l’interface utilisateur :

## Connexion de l’Enregistrement Google Cloud à la plate-forme

La documentation ci-dessous fournit des informations sur la connexion de l’Enregistrement Google Cloud à la plate-forme à l’aide des API ou de l’interface utilisateur :

### Utilisation des API

- [Création d’un connecteur d’Enregistrement Google Cloud à l’aide de l’API du service de flux](../../tutorials/api/create/cloud-storage/google.md)
- [Explorez un système d’enregistrement cloud à l’aide de l’API de service de flux.](../../tutorials/api/explore/cloud-storage.md)
- [Collecte de données d’enregistrement Cloud à l’aide de l’API Flow Service](../../tutorials/api/collect/cloud-storage.md)

### Utilisation de l’interface utilisateur

- [Création d’un connecteur source d’Enregistrement Google Cloud dans l’interface utilisateur](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configuration d’un flux de données pour un connecteur d’enregistrement cloud dans l’interface utilisateur](../../tutorials/ui/dataflow/batch/cloud-storage.md)