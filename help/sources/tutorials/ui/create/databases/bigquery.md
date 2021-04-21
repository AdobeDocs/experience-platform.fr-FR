---
keywords: Experience Platform ; accueil ; sujets populaires ; Google Big Requête ; google big requête ; GBQ ; gbq
solution: Experience Platform
title: Création d’une connexion à une source de Requête Google Big dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion à la source Google Big Requête à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 11%

---

# Créer une connexion source [!DNL Google Big Query] dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur [!DNL Google BigQuery] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Google Big Query] (ci-après appelé &quot;BigQuery&quot;) à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion BigQuery valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte BigQuery sur [!DNL Platform], vous devez fournir les valeurs d&#39;authentification OAuth 2.0 suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `project` | ID du projet [!DNL BigQuery] par défaut à requête. |
| `clientID` | Valeur d’ID utilisée pour générer le jeton d’actualisation. |
| `clientSecret` | Valeur secrète utilisée pour générer le jeton d’actualisation. |
| `refreshToken` | Jeton d’actualisation obtenu à partir de [!DNL Google] utilisé pour autoriser l’accès à [!DNL BigQuery]. |

Pour plus d&#39;informations sur ces valeurs, consultez [ce document BigQuery](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Connectez votre compte Google BigQuery

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte BigQuery à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Google Big Requête]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un connecteur BigQuery.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

La page **[!UICONTROL Se connecter à Google Big Requête]** apparaît. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification BigQuery. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte BigQuery avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte GBQ. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans  [!DNL Platform]](../../dataflow/databases.md).
