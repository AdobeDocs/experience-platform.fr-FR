---
keywords: Experience Platform ; accueil ; sujets populaires ; Amazon ; amazon kinesis ; Kinesis ; kinesis
solution: Experience Platform
title: Création d’une connexion à la source Amazon dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Amazon à l’aide de l’interface utilisateur Adobe Experience Platform.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
translation-type: tm+mt
source-git-commit: d6f1521470b8dc630060584189690545c724de6b
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 12%

---

# Créer une connexion source [!DNL Amazon Kinesis] dans l’interface utilisateur

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source [!DNL Amazon Kinesis] (ci-après dénommé [!DNL "Kinesis"]) à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion [!DNL Kinesis] valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/streaming/cloud-storage-streaming.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source [!DNL Kinesis], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `accessKeyId` | ID de clé d&#39;accès pour votre compte [!DNL Kinesis]. |
| `Secret access key` | Clé d&#39;accès secrète pour votre compte [!DNL Kinesis]. |
| `region` | Région de votre serveur AWS. |

Pour plus d’informations sur ces valeurs, voir [this [!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Connectez votre compte [!DNL Kinesis]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Kinesis] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Enregistrement de cloud]**, sélectionnez **[!UICONTROL Amazon]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur [!DNL Kinesis].

![](../../../../images/tutorials/create/kinesis/catalog.png)

La boîte de dialogue **[!UICONTROL Se connecter à Kinesis]** apparaît. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Kinesis]. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/kinesis/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Kinesis] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous vous êtes connecté à votre compte [!DNL Kinesis] à [!DNL Platform]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer les données de votre enregistrement cloud dans  [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
