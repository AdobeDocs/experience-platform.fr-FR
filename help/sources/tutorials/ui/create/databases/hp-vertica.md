---
keywords: Experience Platform;accueil;rubriques les plus consultées;HP Vertica
solution: Experience Platform
title: Création d’une connexion HP Vertica Source dans l’interface utilisateur
type: Tutorial
description: Découvrez comment créer une connexion source HP Vertica à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 32%

---

# Créer une connexion source HP [!DNL Vertica] dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur HP [!DNL Vertica] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../../../home.md#terms-and-conditions) .

Les connecteurs Source dans Adobe Experience Platform permettent d’ingérer des données provenant de l’extérieur de manière planifiée. Ce tutoriel décrit les étapes à suivre pour créer un connecteur source HP [!DNL Vertica] à l’aide de l’interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion HP [!DNL Vertica] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecter les informations d’identification requises

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour vous connecter correctement à HP [!DNL Vertica] à l’aide de l’API [!DNL Flow Service].

| Informations d’identification | Description |
| ---------- | ----------- |
| `connectionString` | Chaîne de connexion utilisée pour se connecter à votre instance HP [!DNL Vertica]. Le modèle de chaîne de connexion pour HP [!DNL Vertica] est `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Pour plus d’informations sur la prise en main, reportez-vous à [ce document HP [!DNL Vertica] ](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Connectez votre compte HP [!DNL Vertica]

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte HP [!DNL Vertica] à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL HP Vertica]**. Si c&#39;est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un nouveau connecteur HP [!DNL Vertica].

![catalogue](../../../../images/tutorials/create/hp-vertica/catalog.png)

La page **[!UICONTROL Se connecter à HP Vertica]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**.  Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification HP [!DNL Vertica]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** et laissez un certain temps à la nouvelle connexion pour établir.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte HP [!DNL Vertica] avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** dans le coin supérieur droit pour continuer.

![existant](../../../../images/tutorials/create/hp-vertica/existing.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte HP [!DNL Vertica]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans [!DNL Platform]](../../dataflow/databases.md).
