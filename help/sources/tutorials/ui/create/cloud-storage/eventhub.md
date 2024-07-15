---
title: Création d’une connexion Source Azure Event Hubs dans l’interface utilisateur
description: Découvrez comment créer une connexion source Azure Event Hubs à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1256f0c76b29edad4808fc4be1d61399bfbae8fa
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 17%

---

# Créer une connexion source [!DNL Azure Event Hubs] dans l’interface utilisateur

>[!IMPORTANT]
>
>La source [!DNL Azure Event Hubs] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce tutoriel pour apprendre à créer un compte [!DNL Azure Event Hubs] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Event Hubs] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/streaming/cloud-storage-streaming.md).

### Collecter les informations d’identification requises

Pour authentifier votre connecteur source [!DNL Event Hubs], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB Authentification standard]

| Informations d’identification | Description |
| --- | --- |
| Nom de la clé SAS | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| Clé SAS | Clé primaire de l’espace de noms [!DNL Event Hubs]. Les droits `sasPolicy` auxquels correspond `sasKey` doivent être `manage` configurés pour que la liste [!DNL Event Hubs] soit renseignée. |
| Espace de noms | L’espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

>[!TAB Authentification SAS]

| Informations d’identification | Description |
| --- | --- |
| Nom de la clé SAS | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| Clé SAS | Clé primaire de l’espace de noms [!DNL Event Hub]. Les droits `sasPolicy` auxquels correspond `sasKey` doivent être `manage` configurés pour que la liste [!DNL Event Hubs] soit renseignée. |
| Espace de noms | L’espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| Nom de la plateforme d’événements | Renseignez votre nom [!DNL Azure Event Hub]. Lisez la [documentation Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) pour plus d’informations sur les [!DNL Event Hub] noms. |

>[!TAB Event Hub Azure Active Directory Auth]

| Informations d’identification | Description |
| --- | --- |
| Identifiant du client | Identifiant du tenant auprès duquel vous souhaitez demander une autorisation. Votre ID de tenant peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque** : L’ID de client est appelé &quot;ID de répertoire&quot; dans l’interface [!DNL Microsoft Azure]. |
| Identifiant client | ID d’application affecté à votre application. Vous pouvez récupérer cet ID à partir du portail [!DNL Microsoft Entra ID] sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Valeur secrète du client | Le secret client utilisé avec l’ID client pour authentifier votre application. Vous pouvez récupérer votre secret client à partir du portail [!DNL Microsoft Entra ID] sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Espace de noms | L’espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

Pour plus d’informations sur [!DNL Azure Active Directory], consultez le [guide Azure sur l’utilisation de l’ID d’entrée Microsoft](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Event Hub Portée Azure Active Directory Auth]

| Informations d’identification | Description |
| --- | --- |
| Identifiant du client | Identifiant du tenant auprès duquel vous souhaitez demander une autorisation. Votre ID de tenant peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque** : L’ID de client est appelé &quot;ID de répertoire&quot; dans l’interface [!DNL Microsoft Azure]. |
| Identifiant client | ID d’application affecté à votre application. Vous pouvez récupérer cet ID à partir du portail [!DNL Microsoft Entra ID] sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Valeur secrète du client | Le secret client utilisé avec l’ID client pour authentifier votre application. Vous pouvez récupérer votre secret client à partir du portail [!DNL Microsoft Entra ID] sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Espace de noms | L’espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| Nom de la plateforme d’événements | Renseignez votre nom [!DNL Azure Event Hub]. Lisez la [documentation Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) pour plus d’informations sur les [!DNL Event Hub] noms. |

Pour plus d’informations sur [!DNL Azure Active Directory], consultez le [guide Azure sur l’utilisation de l’ID d’entrée Microsoft](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Event Hubs] à l’Experience Platform.

## Connecter votre compte [!DNL Event Hubs]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie [!UICONTROL Stockage dans le cloud], sélectionnez **[!UICONTROL Azure Event Hubs]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources avec les centres d’événements Azure sélectionnés.](../../../../images/tutorials/create/eventhub/catalog.png)

La boîte de dialogue **[!UICONTROL Se connecter aux centres d’événements Azure]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Event Hubs] à utiliser, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Liste des comptes source Azure Event Hubs existants.](../../../../images/tutorials/create/eventhub/existing.png)

### Nouveau compte

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;une connexion de base [!DNL Event Hubs]. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

Pour créer un nouveau compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouveau compte [!DNL Event Hubs].

![Nouvelle interface de création de compte pour les centres d’événements Azure.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Authentification standard]

Pour créer un compte [!DNL Event Hubs] avec authentification standard, utilisez le menu déroulant [!UICONTROL Authentification du compte] et sélectionnez ensuite **[!UICONTROL Authentification standard]**. Ensuite, fournissez les valeurs de votre [!UICONTROL nom de clé SAS], [!UICONTROL clé SAS] et [!UICONTROL espace de noms].

Une fois que vous avez saisi vos informations d’authentification, sélectionnez **[!UICONTROL Se connecter à la source]**.

![Interface d’authentification standard pour les centres d’événements Azure.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB Authentification SAS]

Pour créer un compte [!DNL Event Hubs] avec authentification SAS, utilisez le menu déroulant [!UICONTROL Authentification du compte] et sélectionnez ensuite **[!UICONTROL Authentification SAS]**. Ensuite, fournissez les valeurs de votre [!UICONTROL nom de clé SAS], [!UICONTROL clé SAS], [!UICONTROL espace de noms] et [!UICONTROL nom de centre d’événements].

Une fois que vous avez saisi vos informations d’authentification, sélectionnez **[!UICONTROL Se connecter à la source]**.

![Interface d’authentification SAS pour les centres d’événements Azure.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Event Hub Azure Active Directory Auth]

Pour créer un compte [!DNL Event Hubs] avec l’authentification Event Hub Azure Active Directory, utilisez le menu déroulant [!UICONTROL Authentification du compte] , puis sélectionnez **[!UICONTROL Event Hub Azure Active Directory]**. Ensuite, fournissez les valeurs de vos [!UICONTROL ID de tenant], [!UICONTROL ID de client], [!UICONTROL Valeur secrète client] et [!UICONTROL Espace de noms].

![Authentification Azure Event Hub Azure Active Directory](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Event Hub Portée Azure Active Directory Auth]

Pour créer un compte [!DNL Event Hubs] avec l’authentification Azure Active Directory à la portée de Event Hub, utilisez le menu déroulant [!UICONTROL Authentification du compte], puis sélectionnez **[!UICONTROL Event Hub Scoped Azure Active Directory]**. Ensuite, fournissez les valeurs de vos [!UICONTROL ID de tenant], [!UICONTROL ID de client], [!UICONTROL Valeur secrète client], [!UICONTROL Espace de noms] et [!UICONTROL Nom du hub d’événement].

![Authentification Azure Event Hub étendues Azure Activity Directory](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Étapes suivantes

En suivant ce tutoriel, vous avez connecté votre compte [!DNL Event Hubs] à Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
