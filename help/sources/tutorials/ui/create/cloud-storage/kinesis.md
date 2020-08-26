---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Amazon dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 9%

---


# Create an [!DNL Amazon Kinesis] source connector in the UI

>[!NOTE]
>
>Le [!DNL Amazon Kinesis] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur [!DNL Amazon Kinesis] (ci-après appelé [!DNL "Kinesis"]) source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une [!DNL Kinesis] connexion valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/streaming/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur [!DNL Kinesis] source, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `accessKeyId` | ID de clé d’accès pour votre [!DNL Kinesis] compte. |
| `Secret access key` | Clé d’accès secrète pour votre [!DNL Kinesis] compte. |
| `region` | Région de votre serveur AWS. |

Pour plus d&#39;informations sur ces valeurs, consultez [ [!DNL Kinesis] ce document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Connecter votre [!DNL Kinesis] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Kinesis] compte à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie Enregistrement **** Cloud, sélectionnez **[!UICONTROL Amazon]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau [!DNL Kinesis] connecteur.

![](../../../../images/tutorials/create/kinesis/catalog.png)

La boîte de dialogue **[!UICONTROL Se connecter à Amazon]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos [!DNL Kinesis] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/kinesis/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Kinesis] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous vous êtes connecté à votre [!DNL Kinesis] compte [!DNL Platform]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer [!DNL Platform]](../../dataflow/streaming/cloud-storage.md)les données de votre enregistrement cloud.