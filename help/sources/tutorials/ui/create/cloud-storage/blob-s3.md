---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Azure Blob ou Amazon S3 dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 9fd00ec198f61843bb9a395103215e5441b23745
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 2%

---


# Création d’un connecteur source Azure Blob ou Amazon S3 dans l’interface utilisateur

Les connecteurs source dans Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Azure Blob (ci-après dénommé &quot;Blob&quot;) ou Amazon S3 (ci-après dénommé &quot;S3&quot;) à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de la plateforme d’expérience Adobe :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion de base Blob ou S3, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

Experience Platform prend en charge les formats de fichier suivants à assimiler à partir d’enregistrements externes :

- Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La valeur des en-têtes de champ des fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.
- Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être compatibles XDM.
- Apache Parquet : Les fichiers de données au format Parquet doivent être conformes à XDM.

### Collecte des informations d’identification requises

Pour accéder à votre enregistrement Blob sur la plate-forme, vous devez fournir une valeur valide pour les informations d’identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion requise pour accéder aux données dans votre enregistrement Blob. Le modèle de chaîne de connexion Blob est le suivant : `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Pour plus d&#39;informations sur la prise en main, consultez [ce document](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)Azure Blob.

De même, l’accès à votre compartiment S3 sur la plate-forme nécessite que vous fournissiez vos valeurs valides pour les informations d’identification suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `s3AccessKey` | ID de clé d&#39;accès pour votre enregistrement S3. |
| `s3SecretKey` | ID de clé secrète de votre enregistrement S3. |

Pour plus d’informations sur la prise en main, consultez [ce document](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/)AWS.

## Connecter votre compte Blob ou S3

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un compte Blob ou S3 pour vous connecter à la plate-forme.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de données existants qui y sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie *[!UICONTROL Bases de données]* , sélectionnez Enregistrement **[!UICONTROL Blob]** Azure ou **[!UICONTROL Amazon S3]** cliquez **sur l&#39;icône + (+) pour créer un connecteur Blob ou S3.**

![catalogue](../../../../images/tutorials/create/blob/catalog.png)

La page *[!UICONTROL Se connecter à l&#39;Enregistrement]* Blob Azure s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos informations d’identification Blob ou S3. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à l’établissement du nouveau compte.

![connecter](../../../../images/tutorials/create/blob/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Blob ou S3 avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/blob/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte Blob ou S3. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données afin d’importer des données de votre enregistrement cloud dans la plate-forme](../../dataflow/batch/cloud-storage.md).