---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Amazon Kinesis dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Création d’un connecteur [!DNL Amazon Kinesis] source dans l’interface utilisateur

>[!NOTE]
>Le [!DNL Amazon Kinesis] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source dans l’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur [!DNL Amazon Kinesis] (ci-après appelé [!DNL "Kinesis"]) source à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de l&#39;Adobe Experience Platform :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un [!DNL Kinesis] compte, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/streaming/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur [!DNL Kinesis] source, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `accessKeyId` | ID de clé d’accès pour votre [!DNL Kinesis] compte. |
| `Secret access key` | Clé d’accès secrète pour votre [!DNL Kinesis] compte. |
| `region` | Région de votre serveur AWS. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)Kinesis.

## Connecter votre [!DNL Kinesis] compte

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Kinesis] compte à [!DNL Platform].

Connectez-vous à [l’Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’onglet *Catalogue* affiche diverses sources auxquelles il est possible de se connecter [!DNL Platform]. Chaque source affiche le nombre de comptes existants qui lui sont associés.

Sous *[!UICONTROL Cloud Enregistrement]* catégorie, sélectionnez **[!UICONTROL Amazon Kinesis]** et cliquez sur **l’icône + (+)** pour créer un nouveau [!DNL Kinesis] connecteur.

![](../../../../images/tutorials/create/kinesis/catalog.png)

La boîte de dialogue *[!UICONTROL Se connecter à Amazon Kinesis]* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos [!DNL Kinesis] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/kinesis/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Kinesis] compte auquel vous voulez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous vous êtes connecté à votre [!DNL Kinesis] compte [!DNL Platform]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données de votre enregistrement cloud dans Platform](../../dataflow/streaming/cloud-storage.md).