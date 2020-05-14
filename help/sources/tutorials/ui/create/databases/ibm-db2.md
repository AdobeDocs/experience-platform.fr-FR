---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source IBM DB2 dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---



# Création d’un connecteur source IBM DB2 dans l’interface utilisateur

> [!NOTE]
> Le connecteur IBM DB2 est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source IBM DB2 (ci-après dénommé &quot;DB2&quot;) à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion DB2 valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Les sections suivantes contiennent des informations supplémentaires dont vous aurez besoin pour vous connecter à DB2 à l’aide de l’API Flow Service.

| Informations d’identification | Description |
| ---------- | ----------- |
| `server` | Nom du serveur DB2. Vous pouvez spécifier le numéro de port suivant le nom du serveur délimité par deux points. Par exemple : server:port. |
| `database` | Nom de la base de données DB2. |
| `username` | Nom d’utilisateur utilisé pour la connexion à la base de données DB2. |
| `password` | mot de passe du compte utilisateur que vous avez spécifié pour le nom d’utilisateur. |

Pour plus d’informations sur la prise en main, reportez-vous à [ce document](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)DB2.

## Connexion de votre compte IBM DB2

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau compte DB2 pour vous connecter à Platform.

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui y sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie *[!UICONTROL Bases de données]* , sélectionnez **[!UICONTROL IBM DB2]** et cliquez **sur l’icône + (+)** pour créer un connecteur DB2.

![catalogue](../../../../images/tutorials/create/ibm-db2/catalog.png)

La page *[!UICONTROL Se connecter à IBM DB2]* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos informations d’identification DB2. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à l’établissement du nouveau compte.

![connecter](../../../../images/tutorials/create/ibm-db2/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte DB2 avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/ibm-db2/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte DB2. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans la plate-forme](../../dataflow/databases.md).