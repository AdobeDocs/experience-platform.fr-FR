---
keywords: Experience Platform;accueil;rubriques les plus consultées;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Création d’une connexion IBM DB2 Source dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source IBM DB2 à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 29%

---

# Créer une connexion source IBM DB2 dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur IBM DB2 est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Les connecteurs Source dans Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur de manière planifiée. Ce tutoriel décrit les étapes de création d’un connecteur source IBM DB2 (ci-après appelé &quot;DB2&quot;) à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion DB2 valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter à DB2 à l’aide de l’API [!DNL Flow Service].

| Informations d’identification | Description |
| ---------- | ----------- |
| `server` | Nom du serveur DB2. Vous pouvez spécifier le numéro de port suivant le nom du serveur délimité par deux points. Par exemple : server:port. |
| `database` | Nom de la base de données DB2. |
| `username` | Nom d’utilisateur utilisé pour se connecter à la base de données DB2. |
| `password` | mot de passe du compte utilisateur que vous avez spécifié pour le nom d’utilisateur. |

Pour plus d’informations sur la prise en main, reportez-vous à [ce document DB2](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Connexion à votre compte IBM DB2

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte DB2 à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL IBM DB2]**. Si c&#39;est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur DB2.

![catalogue](../../../../images/tutorials/create/ibm-db2/catalog.png)

La page **[!UICONTROL Se connecter à IBM DB2]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification DB2. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** et laissez un certain temps à la nouvelle connexion pour établir.

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte DB2 avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/ibm-db2/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte DB2. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
