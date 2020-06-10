---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Couchbase dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: adb9c46e7337897e2336971e58ebc90b0e497ea0
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Création d’un connecteur source Couchbase dans l’interface utilisateur

> [!NOTE]
> Le connecteur Couchbase est en version bêta. Les fonctionnalités et la documentation peuvent être modifiées.

Les connecteurs source dans [!DNL Adobe Experience Platform] permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Couchbase à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants de [!DNL Platform]:

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion Couchbase valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour authentifier votre connecteur source Couchbase, vous devez fournir des valeurs pour la propriété de connexion suivante :

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour la connexion à votre instance Couchbase. Le modèle de chaîne de connexion pour Couchbase est `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Pour plus d&#39;informations sur l&#39;acquisition d&#39;une chaîne de connexion, consultez la documentation relative à la connexion [](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)Couchbase. |

## Connecter votre compte Couchbase

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau compte Couchbase auquel vous connecter [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant et chaque source affiche le nombre de comptes et de flux de jeux de données existants qui y sont associés.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie *[!UICONTROL Bases de données]* , sélectionnez **[!UICONTROL Bases de données]** , cliquez **sur l&#39;icône + (+)** pour créer un nouveau connecteur Couchbase.

![catalogue](../../../../images/tutorials/create/couchbase/catalog.png)

La page *[!UICONTROL Se connecter à Couchbase]* s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez le nom de la connexion, une description facultative et vos informations d’identification Couchbase. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** , puis accordez du temps au nouveau compte pour établir.

![connecter](../../../../images/tutorials/create/couchbase/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte Couchbase avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![existant](../../../../images/tutorials/create/couchbase/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte Couchbase. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans la plate-forme](../../dataflow/databases.md).