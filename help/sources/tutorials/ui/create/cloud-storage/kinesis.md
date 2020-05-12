---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Amazon Kinesis dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# Création d’un connecteur source Amazon Kinesis dans l’interface utilisateur

>[!NOTE]
> Le connecteur Amazon Kinesis est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source Amazon Kinesis (ci-après appelé &quot;Kinesis&quot;) à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte Kinesis, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux](../../dataflow/streaming/cloud-storage.md)de données.

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source Kinesis, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `accessKeyId` | ID de clé d&#39;accès pour votre compte Kinesis. |
| `Secret access key` | Clé d’accès secrète pour votre compte Kinesis. |
| `region` | Région de votre serveur AWS. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)Kinesis.

## Connecter votre compte Kinesis

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte Kinesis à la plate-forme.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’onglet *Catalogue* affiche diverses sources pour lesquelles il est possible de se connecter à Plateforme. Chaque source affiche le nombre de comptes existants qui lui sont associés.

Sous *Cloud Enregistrement* catégorie, sélectionnez **Amazon Kinesis** et cliquez sur **l’icône + (+)** pour créer un nouveau connecteur Kinesis.

![](../../../../images/tutorials/create/eventhub/catalog.png)

La boîte de dialogue *Se connecter à Amazon Kinesis* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification Kinesis. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un peu de temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/eventhub/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Kinesis avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous vous êtes connecté à votre compte Kinesis sur la plate-forme. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données afin d’importer des données de votre enregistrement cloud dans la plate-forme](../../dataflow/streaming/cloud-storage.md).