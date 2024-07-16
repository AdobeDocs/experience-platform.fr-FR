---
title: Création d’une connexion Amazon Redshift à Source dans l’interface utilisateur
description: Découvrez comment créer une connexion source Amazon Redshift à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 41%

---

# Connectez votre compte [!DNL Amazon Redshift] à l’aide de l’espace de travail des sources

>[!IMPORTANT]
>
>La source [!DNL Amazon Redshift] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour connecter votre compte [!DNL Amazon Redshift] (ci-après appelé &quot;[!DNL Redshift]&quot;) à Adobe Experience Platform à l’aide de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Redshift] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL Redshift] sur Experience Platform, vous devez fournir les valeurs suivantes :

| **Credential** | **Description** |
| -------------- | --------------- |
| Serveur | Serveur associé à votre compte [!DNL Redshift]. |
| Port | Port TCP utilisé par un serveur [!DNL Redshift] pour écouter les connexions client. |
| Nom d’utilisateur | Nom d’utilisateur associé à votre compte [!DNL Redshift]. |
| Mot de passe | Mot de passe associé à votre compte [!DNL Redshift]. |
| Base de données | La base de données [!DNL Redshift] à laquelle vous accédez. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Redshift] à l’Experience Platform.

## Connecter votre compte [!DNL Redshift]

>[!NOTE]
>
>La norme de codage par défaut pour [!DNL Redshift] est Unicode. Cela ne peut pas être modifié.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Amazon Redshift]**. Si c&#39;est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur [!DNL Redshift].

![](../../../../images/tutorials/create/redshift/catalog.png)

La page **[!UICONTROL Se connecter à Amazon Redshift]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Redshift]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** et laissez un certain temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/redshift/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Redshift] auquel vous souhaitez vous connecter, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/redshift/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Redshift]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Experience Platform](../../dataflow/databases.md).
