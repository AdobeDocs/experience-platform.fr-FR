---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur source Azure Data Lake   Gen2 dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Création d&#39;un connecteur source Azure Data Lake   Gen2 dans l&#39;interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source Azure Data Lake   Gen2 (ci-après dénommé &quot;ADLS Gen2&quot;) à l&#39;aide de l&#39;interface utilisateur de la plateforme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
- [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion de base ADLS Gen2, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source ADLS Gen2, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | Point de fin pour ADLS Gen2. |
| `servicePrincipalId` | ID client de l’application. |
| `servicePrincipalKey` | La clé de l&#39;application. |
| `tenant` | Informations sur le client qui contiennent votre application. |

Pour plus d&#39;informations sur ces valeurs, reportez-vous à [cette](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

## Connectez votre compte ADLS Gen2

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte ADLS Gen2 à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’onglet *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes. Chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous le  *Cloud* , sélectionnez **Azure Data Lake Gen2** pour afficher une barre d&#39;informations sur le côté droit de votre écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter au source  sa documentation. Pour créer une connexion de base entrante, cliquez sur **Connect source**.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

La boîte de dialogue *Connexion à Azure Data Lake Gen2* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion de base, une description facultative et vos informations d’identification ADLS Gen2. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un peu de temps pour que la nouvelle connexion de base s’établisse.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte ADLS Gen2 avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte ADLS Gen2. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données de votre cloud   dans Platform](../../dataflow/cloud-storage.md).