---
keywords: Experience Platform;accueil;rubriques populaires;[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: Créer une connexion Source PostgreSQL dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source PostgreSQL à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 47%

---

# Créer une connexion source [!DNL PostgreSQL] dans l’interface utilisateur

Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL PostgreSQL] à l’aide de l’interface utilisateur de [!DNL Experience Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL PostgreSQL] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL PostgreSQL] sur [!DNL Experience Platform], vous devez fournir la valeur suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion associée à votre compte [!DNL PostgreSQL]. Le modèle de chaîne de connexion [!DNL PostgreSQL] est : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Pour plus d’informations sur la prise en main, reportez-vous à ce [[!DNL PostgreSQL] document](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Activer le chiffrement SSL pour votre chaîne de connexion

Vous pouvez activer le chiffrement SSL pour votre chaîne de connexion [!DNL PostgreSQL] en ajoutant votre chaîne de connexion avec les propriétés suivantes :

| Propriété | Description | Exemple |
| --- | --- | --- |
| `EncryptionMethod` | Permet d’activer le chiffrement SSL sur vos données [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(Désactivé)</li><li>`EncryptionMethod=1`(Activé)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valide le certificat envoyé par votre base de données [!DNL PostgreSQL] lorsque la `EncryptionMethod` est appliquée. | <uL><li>`ValidationServerCertificate=0`(Désactivé)</li><li>`ValidationServerCertificate=1`(Activé)</li></ul> |

Voici un exemple de chaîne de connexion [!DNL PostgreSQL] ajoutée avec le chiffrement SSL : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Connecter votre compte [!DNL PostgreSQL]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL PostgreSQL] à [!DNL Experience Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Base de données PostgreSQL]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur [!DNL PostgreSQL].

![](../../../../images/tutorials/create/postgresql/catalog.png)

La page **[!UICONTROL Connexion à[!DNL PostgreSQL]]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL PostgreSQL]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis patientez quelques instants le temps d’établir la nouvelle connexion.

![](../../../../images/tutorials/create/postgresql/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL PostgreSQL] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/postgresql/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL PostgreSQL]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Experience Platform]](../../dataflow/databases.md).
