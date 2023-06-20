---
title: Création d’une connexion source de redirection Amazon dans l’interface utilisateur
description: Découvrez comment créer une connexion source Amazon Redshift à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 41%

---

# Connectez-vous à [!DNL Amazon Redshift] compte à l’aide de l’espace de travail sources

>[!IMPORTANT]
>
>Le [!DNL Amazon Redshift] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour connecter votre [!DNL Amazon Redshift] (ci-après dénommés &quot;[!DNL Redshift]&quot;) à Adobe Experience Platform à l’aide de l’interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

- [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   - [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   - [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Redshift] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à [!DNL Redshift] sur Experience Platform, vous devez fournir les valeurs suivantes :

| **Informations d’identification** | **Description** |
| -------------- | --------------- |
| Serveur | Le serveur associé à votre [!DNL Redshift] compte . |
| Port | Le port TCP qu’un [!DNL Redshift] Le serveur utilise pour écouter les connexions client. |
| Nom d’utilisateur | Le nom d’utilisateur associé à votre [!DNL Redshift] compte . |
| Mot de passe | Le mot de passe associé à votre [!DNL Redshift] compte . |
| Base de données | Le [!DNL Redshift] base de données à laquelle vous accédez. |

Pour plus d’informations sur la prise en main, reportez-vous à la section [this [!DNL Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Redshift] compte à Experience Platform.

## Connecter votre compte [!DNL Redshift]

>[!NOTE]
>
>La norme de codage par défaut pour [!DNL Redshift] est Unicode. Cela ne peut pas être modifié.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au **[!UICONTROL Sources]** workspace. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **[!UICONTROL Bases de données]** catégorie, sélectionnez **[!UICONTROL Amazon Redshift]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer [!DNL Redshift] connecteur.

![](../../../../images/tutorials/create/redshift/catalog.png)

Le **[!UICONTROL Connexion à Amazon Redshift]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et [!DNL Redshift] informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis accorder un certain temps pour établir la nouvelle connexion.

![](../../../../images/tutorials/create/redshift/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le [!DNL Redshift] compte auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/redshift/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Redshift]. Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données dans Experience Platform](../../dataflow/databases.md).
