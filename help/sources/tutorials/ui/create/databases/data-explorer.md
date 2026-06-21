---
keywords: Experience Platform;accueil;rubriques populaires;Azure Data Explorer;explorateur de données azure;explorateur de données;Data Explorer
solution: Experience Platform
title: Création d’une connexion Source Azure Data Explorer dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source Azure Data Explorer à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
TQID: https://experienceleague.adobe.com/pyv3NeZQ9vGoR3inAHDY09dUsjRjgvXP-r-nvNRPi1k
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 504
ht-degree: 39%

---

# Créer une connexion source [!DNL Azure Data Explorer] dans l’interface utilisateur

Les connecteurs Source de Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur selon un calendrier précis. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source [!DNL Azure Data Explorer] (ci-après dénommé « [!DNL Data Explorer] ») à l’aide de l’interface utilisateur [!DNL Experience Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Data Explorer] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Pour accéder à votre compte [!DNL Data Explorer] sur [!DNL Experience Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `endpoint` | Point d’entrée du serveur [!DNL Data Explorer]. |
| `database` | Nom de la base de données [!DNL Data Explorer]. |
| `tenant` | Identifiant client unique utilisé pour la connexion à la base de données [!DNL Data Explorer]. |
| `servicePrincipalId` | Identifiant principal de service unique utilisé pour la connexion à la base de données [!DNL Data Explorer]. |
| `servicePrincipalKey` | Clé principale de service unique utilisée pour la connexion à la base de données [!DNL Data Explorer]. |

Pour plus d’informations sur la prise en main, consultez [ce [!DNL Data Explorer] document](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Connecter votre compte [!DNL Azure Data Explorer]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Data Explorer] à [!DNL Experience Platform].

Connectez-vous à [&#128279;](https://platform.adobe.com) puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Azure Data Explorer]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur Data Explorer.

![catalogue](../../../../images/tutorials/create/data-explorer/catalog.png)

La page **[!UICONTROL Connexion à Azure Data Explorer]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Data Explorer]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion]** puis patientez quelques instants le temps d’établir la nouvelle connexion.

![connexion](../../../../images/tutorials/create/data-explorer/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Data Explorer] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/data-explorer/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Data Explorer]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Experience Platform]](../../dataflow/databases.md).
