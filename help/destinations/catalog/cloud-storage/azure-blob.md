---
keywords: Blob Azure ; Blob destination;s3;azure blob destination
title: Connexion Blob Azure
description: Créez une connexion sortante en direct à votre enregistrement Azure Blob pour exporter périodiquement des fichiers de données CSV ou délimités par des tabulations à partir de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 10%

---


# [!DNL Azure Blob] connexion

## Présentation {#overview}

[!DNL Azure Blob] (ci-après dénommés &quot;[!DNL Blob]&quot;) est la solution d&#39;enregistrement d&#39;objets de Microsoft pour le cloud. Ce didacticiel décrit les étapes à suivre pour créer une destination [!DNL Blob] à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une destination Blob valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [l’activation des segments vers votre destination](../../ui/activate-destinations.md).

## Formats de fichiers pris en charge {#file-formats}

[!DNL Experience Platform] prend en charge le format de fichier suivant à exporter vers  [!DNL Blob]:

- Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La prise en charge des fichiers DSV généraux sera assurée à l’avenir. Pour plus d’informations sur les fichiers pris en charge, consultez la section enregistrement de cloud du didacticiel sur [l’activation des destinations](../../ui/activate-destinations.md#esp-and-cloud-storage).

## Connecter votre compte Blob {#connect-destination}

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Destinations]**. L’écran **[!UICONTROL Catalogue]** affiche diverses destinations pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la destination spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Enregistrement de cloud]**, sélectionnez **[!UICONTROL Enregistrement de blocage Azure]**, puis **[!UICONTROL Configurer]**.

![Catalogue](../../assets/catalog/cloud-storage/blob/catalog.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

La page **[!UICONTROL Se connecter à l&#39;Enregistrement Blob Azure]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

## Nouveau compte {#new-account}

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Sur le formulaire d’entrée qui s’affiche, indiquez la chaîne de connexion. La chaîne de connexion est requise pour accéder aux données de votre enregistrement Blob. Le modèle de chaîne de connexion [!DNL Blob] s&#39;début avec : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

Pour plus d&#39;informations sur la configuration de votre chaîne de connexion [!DNL Blob], voir [Configurer une chaîne de connexion pour un compte d&#39;enregistrement Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) dans la documentation Microsoft.

Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Votre clé publique doit être écrite en tant que chaîne codée [!DNL Base64].

![Nouveau compte](../../assets/catalog/cloud-storage/blob/new.png)

## Compte existant {#existing-account}

Pour connecter un compte existant, sélectionnez le compte [!DNL Blob] auquel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![Compte existant](../../assets/catalog/cloud-storage/blob/existing.png)

## Authentification {#authentication}

La page **Authentification** s&#39;affiche. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative, le chemin d’accès au dossier et le conteneur de vos fichiers.

Au cours de cette étape, vous pouvez également sélectionner toute **[!UICONTROL action marketing]** qui doit s’appliquer à cette destination. Les actions marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer votre propre action marketing. Pour plus d&#39;informations sur les actions marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

Une fois terminé, sélectionnez **[!UICONTROL Créer une destination]**.

![Authentification](../../assets/catalog/cloud-storage/blob/authentication.png)

## Étapes suivantes {#activate-segments}

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL Blob]. Vous pouvez maintenant passer au didacticiel suivant et [activer les segments vers votre destination](../../ui/activate-destinations.md).
