---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Google Big Requête dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 14%

---


# Create a [!DNL Google Big Query] source connector in the UI

>[!NOTE]
> Le [!DNL Google BigQuery] connecteur est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Google Big Query] (ci-après appelé &quot;GBQ&quot;) à l’aide de l’ [!DNL Platform] interface utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Système de modèle de données d’expérience (XDM)](../../../../../xdm/home.md)[!DNL Experience Platform] : cadre normalisé selon lequel organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Real-time Customer Profile](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d’une connexion de base GBQ, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte GBQ sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `project` | ID du projet par défaut sur lequel le [!DNL BigQuery] projet doit être requête. |
| `clientID` | Valeur d’ID utilisée pour générer le jeton d’actualisation. |
| `clientSecret` | Valeur secrète utilisée pour générer le jeton d’actualisation. |
| `refreshToken` | Jeton d’actualisation obtenu à partir de [!DNL Google] utilisé pour autoriser l’accès à [!DNL BigQuery]. |

Pour plus d’informations sur ces valeurs, consultez [ce document](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)GBQ.

## Connecter votre compte GBQ

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte GBQ à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]* . L’écran *[!UICONTROL Catalogue]* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes et chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie *[!UICONTROL Bases de données]* , sélectionnez **[!UICONTROL Google Big Requête]** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou à la vue de sa documentation. Pour créer une connexion de base entrante, sélectionnez **[!UICONTROL Ajouter des données]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

La page *[!UICONTROL Se connecter à Google Big Requête]* s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification GBQ pour la connexion de base. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte GBQ avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte GBQ. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans la plate-forme](../../dataflow/databases.md).