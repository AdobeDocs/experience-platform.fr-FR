---
keywords: Experience Platform;accueil;rubriques populaires;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Création d’une connexion Source Apache HDFS dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Apache Hadoop Distributed File System à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 35%

---

# Créer une connexion source HDFS [!DNL Apache] dans l’interface utilisateur

>[!NOTE]
>
>Le connecteur HDFS [!DNL Apache] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Les connecteurs Source de [!DNL Adobe Experience Platform] permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes d’authentification d’un connecteur source [!DNL Apache Hadoop Distributed File System] (ci-après appelé &quot;HDFS&quot;) à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une connaissance pratique des composants suivants de [!DNL Platform] :

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion HDFS valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecter les informations d’identification requises

Pour authentifier votre connecteur source HDFS, vous devez fournir des valeurs pour la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | L’URL définit les paramètres d’authentification requis pour la connexion anonyme à HDFS. Pour plus d’informations sur la manière d’obtenir cette valeur, reportez-vous au document suivant sur l’ [authentification HTTPS pour HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Connexion à votre compte HDFS

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte HDFS à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Stockage dans le cloud]**, sélectionnez **[!UICONTROL Apache HDFS]**. Si c&#39;est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur HDFS.

![catalogue](../../../../images/tutorials/create/hdfs/catalog.png)

La page **[!UICONTROL Se connecter à HDFS]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification HDFS. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte HDFS avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/hdfs/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte HDFS. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
