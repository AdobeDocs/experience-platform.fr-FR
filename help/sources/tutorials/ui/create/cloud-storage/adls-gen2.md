---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Créer un connecteur source Azure Data Lake Enregistrement Gen2 dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 799445eca080175e2bffc49c6714f0c812b9bbea
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Créer un connecteur source Azure Data Lake Enregistrement Gen2 dans l&#39;interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour authentifier un connecteur source Azure Data Lake Enregistrement Gen2 (ci-après dénommé &quot;ADLS Gen2&quot;) à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   - [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   - [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
- [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion de base ADLS Gen2, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source ADLS Gen2, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | Point de terminaison pour ADLS Gen2. |
| `servicePrincipalId` | ID client de l’application. |
| `servicePrincipalKey` | La clé de l&#39;application. |
| `tenant` | Informations sur le client qui contient votre application. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)ADLS Gen2.

## Connectez votre compte ADLS Gen2.

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte ADLS Gen2 à la plate-forme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’onglet *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes. Chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie d&#39;Enregistrement ** Cloud, sélectionnez **Azure Data Lake Gen2** pour afficher une barre d&#39;informations sur le côté droit de l&#39;écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la vue source de sa documentation. Pour créer une connexion de base entrante, cliquez sur **Connexion source**.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

La boîte de dialogue *Se connecter à Azure Data Lake Gen2* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, fournissez la connexion de base avec un nom, une description facultative et vos informations d’identification ADLS Gen2. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte ADLS Gen2 avec lequel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte ADLS Gen2. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données afin d’importer des données de votre enregistrement cloud dans la plate-forme](../../dataflow/batch/cloud-storage.md).