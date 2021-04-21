---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement d'objet Oracle ; enregistrement d'objet oracle
solution: Experience Platform
title: Création d’une connexion à la source de l’Enregistrement d’objet d’Oracle dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion à la source de l’Enregistrement d’objets d’Oracle à l’aide de l’interface utilisateur Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 10%

---

# Créer une connexion à la source [!DNL Oracle Object Storage] dans l&#39;interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer une connexion à la source [!DNL Oracle Object Storage] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Collecte des informations d’identification requises

Pour vous connecter à [!DNL Oracle Object Storage], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `serviceUrl` | Point de terminaison [!DNL Oracle Object Storage] requis pour l&#39;authentification. Le format de point de terminaison est : `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | ID de clé d&#39;accès [!DNL Oracle Object Storage] requis pour l&#39;authentification. |
| `secretKey` | Mot de passe [!DNL Oracle Object Storage] requis pour l&#39;authentification. |
| `bucketName` | Nom du compartiment autorisé requis si l’utilisateur dispose d’un accès restreint. Le nom du compartiment doit comporter entre trois et 63 caractères, commencer et se terminer par une lettre ou un nombre et ne peut contenir que des lettres minuscules, des chiffres ou des tirets (`-`). Le nom du compartiment ne peut pas être formaté comme une adresse IP. |
| `folderPath` | chemin d’accès au dossier autorisé requis si l’utilisateur dispose d’un accès restreint. |

Pour plus d&#39;informations sur la façon d&#39;obtenir ces valeurs, consultez le [Oracle Object Enregistrement authentication guide](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau compte d’Enregistrement d’objet d’Oracle pour vous connecter à la plate-forme.

## Se connecter à l&#39;Enregistrement d&#39;objet d&#39;Oracle

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l&#39;aide de la barre de recherche.

Sous la catégorie [!UICONTROL enregistrement de cloud], sélectionnez **[!UICONTROL Enregistrement d’objet d’Oracle]**, puis **[!UICONTROL Ajouter les données]**.

![catalogue](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Oracle Object Storage] avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nouveau compte

Si vous créez un nouveau compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis indiquez un nom, une description facultative et vos informations d&#39;identification [!DNL Oracle Object Storage]. Une fois terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis attendez un certain temps pour que la nouvelle connexion s&#39;établisse.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL Oracle Object Storage]. Vous pouvez maintenant passer au didacticiel suivant sur [la configuration d’un flux de données pour importer des données de votre enregistrement cloud dans Platform](../../dataflow/batch/cloud-storage.md).
