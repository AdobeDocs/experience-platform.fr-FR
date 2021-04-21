---
keywords: Experience Platform ; accueil ; sujets populaires ; Phoenix ; phoenix
solution: Experience Platform
title: Création d’une connexion à la source Phoenix dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source Phoenix à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 11%

---

# Créer une connexion source [!DNL Phoenix] dans l’interface utilisateur

>[!NOTE]
>
> Le connecteur [!DNL Phoenix] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source [!DNL Phoenix] à l&#39;aide de l&#39;interface utilisateur [!DNL Platform].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel  [!DNL Experience Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Si vous disposez déjà d&#39;une connexion [!DNL Phoenix] valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d&#39;un flux de données](../../dataflow/databases.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Phoenix] sur [!DNL Platform], vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Adresse IP ou nom d’hôte du serveur [!DNL Phoenix]. |
| `port` | port TCP utilisé par le serveur [!DNL Phoenix] pour écouter les connexions client. Si vous vous connectez à [!DNL Azure HDInsights], spécifiez le port 443. |
| `httpPath` | URL partielle correspondant au serveur [!DNL Phoenix]. Spécifiez /hbasephoenix0 si vous utilisez la grappe [!DNL Azure HDInsights]. |
| `username` | Nom d’utilisateur utilisé pour accéder au serveur [!DNL Phoenix]. |
| `password` | Mot de passe correspondant à l’utilisateur. |
| `enableSsl` | Bascule qui spécifie si les connexions au serveur sont chiffrées à l’aide de SSL. |

Pour plus d&#39;informations sur la prise en main, consultez [ce [!DNL Phoenix] document](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Connectez votre compte [!DNL Phoenix]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Phoenix] afin de vous connecter à [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail **[!UICONTROL Sources]**. L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]**, sélectionnez **[!UICONTROL Phoenix]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer un nouveau compte [!DNL Phoenix].

![catalogue](../../../../images/tutorials/create/phoenix/catalog.png)

La page **[!UICONTROL Se connecter à Phoenix]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification [!DNL Phoenix]. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

![connecter](../../../../images/tutorials/create/phoenix/new.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte [!DNL Phoenix] auquel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/phoenix/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte [!DNL Phoenix]. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans  [!DNL Platform]](../../dataflow/databases.md).
