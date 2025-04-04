---
title: Créer une connexion Source Azure Event Hubs dans l’interface utilisateur
description: Découvrez comment créer une connexion source Azure Event Hubs à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 16%

---

# Créer une connexion source [!DNL Azure Event Hubs] dans l’interface utilisateur

>[!IMPORTANT]
>
>La source [!DNL Azure Event Hubs] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Lisez ce tutoriel pour savoir comment créer un compte [!DNL Azure Event Hubs] à l’aide de l’interface utilisateur de Adobe Experience Platform.

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

>[!TAB  Authentification standard ]

| Informations d’identification | Description |
| --- | --- |
| Nom de la clé SAS | Nom de la règle d’autorisation, également appelé nom de la clé SAS. |
| Clé SAS | Clé primaire de l’espace de noms [!DNL Event Hubs]. La `sasPolicy` à laquelle correspond le `sasKey` doit disposer de droits `manage` configurés pour que la liste [!DNL Event Hubs] soit renseignée. |
| Espace de noms | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

>[!TAB authentification SAS]

| Informations d’identification | Description |
| --- | --- |
| Nom de la clé SAS | Nom de la règle d’autorisation, également appelé nom de la clé SAS. |
| Clé SAS | Clé primaire de l’espace de noms [!DNL Event Hub]. La `sasPolicy` à laquelle correspond le `sasKey` doit disposer de droits `manage` configurés pour que la liste [!DNL Event Hubs] soit renseignée. |
| Espace de noms | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| Nom du hub d’événements | Renseignez votre nom de [!DNL Azure Event Hub]. Lisez la documentation de [Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) pour plus d&#39;informations sur les noms de [!DNL Event Hub]. |

>[!TAB Authentification Azure Active Directory Event Hub]

| Informations d’identification | Description |
| --- | --- |
| ID du client | L’identifiant du client auprès duquel vous souhaitez demander une autorisation. Votre identifiant client peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque** : l’ID client est appelé « ID de répertoire » dans l’interface [!DNL Microsoft Azure]. |
| Identifiant client | Identifiant d’application attribué à votre application. Vous pouvez récupérer cet identifiant à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| Valeur du secret client | Secret client utilisé avec l’identifiant client pour authentifier votre application . Vous pouvez récupérer votre secret client à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| Espace de noms | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

Pour plus d’informations sur [!DNL Azure Active Directory], consultez le guide [Azure sur l’utilisation de l’Entra ID de Microsoft](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Authentification Azure Active Directory étendue Event Hub]

| Informations d’identification | Description |
| --- | --- |
| ID du client | L’identifiant du client auprès duquel vous souhaitez demander une autorisation. Votre identifiant client peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque** : l’ID client est appelé « ID de répertoire » dans l’interface [!DNL Microsoft Azure]. |
| Identifiant client | Identifiant d’application attribué à votre application. Vous pouvez récupérer cet identifiant à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| Valeur du secret client | Secret client utilisé avec l’identifiant client pour authentifier votre application . Vous pouvez récupérer votre secret client à partir du portail [!DNL Microsoft Entra ID] où vous avez enregistré votre [!DNL Azure Active Directory]. |
| Espace de noms | Espace de noms du [!DNL Event Hub] auquel vous accédez. Un espace de noms [!DNL Event Hub] fournit un conteneur de définition de portée unique dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| Nom du hub d’événements | Renseignez votre nom de [!DNL Azure Event Hub]. Lisez la documentation de [Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) pour plus d&#39;informations sur les noms de [!DNL Event Hub]. |

Pour plus d’informations sur [!DNL Azure Active Directory], consultez le guide [Azure sur l’utilisation de l’Entra ID de Microsoft](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

Une fois les informations d’identification requises collectées, vous pouvez suivre les étapes ci-dessous pour lier votre compte [!DNL Event Hubs] à Experience Platform.

## Connecter votre compte [!DNL Event Hubs]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL Espace de stockage], sélectionnez **[!UICONTROL Azure Event Hubs]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Le catalogue de sources avec Azure Event Hubs sélectionné.](../../../../images/tutorials/create/eventhub/catalog.png)

La boîte de dialogue **[!UICONTROL Se connecter à Azure Event Hubs]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Event Hubs] que vous souhaitez utiliser, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Liste des comptes sources Azure Event Hubs existants.](../../../../images/tutorials/create/eventhub/existing.png)

### Nouveau compte

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d’authentification d’une connexion de base [!DNL Event Hubs]. Pour modifier le type d’authentification, vous devez créer une connexion de base.

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative pour votre nouveau compte [!DNL Event Hubs].

![Nouvelle interface de création de compte pour Azure Event Hubs.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB  Authentification standard ]

Pour créer un compte [!DNL Event Hubs] avec l’authentification standard, utilisez le menu déroulant [!UICONTROL Authentification du compte] puis sélectionnez **[!UICONTROL Authentification standard]**. Indiquez ensuite les valeurs de votre [!UICONTROL nom de la clé SAS], [!UICONTROL clé SAS] et [!UICONTROL espace de noms].

Une fois vos informations d’authentification saisies, sélectionnez **[!UICONTROL Se connecter à la source]**.

![L’interface d’authentification standard pour Azure Event Hubs.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB authentification SAS]

Pour créer un compte [!DNL Event Hubs] avec authentification SAS, utilisez le menu déroulant [!UICONTROL Authentification du compte] puis sélectionnez **[!UICONTROL Authentification SAS]**. Indiquez ensuite les valeurs de votre [!UICONTROL nom de la clé SAS], [!UICONTROL clé SAS], [!UICONTROL espace de noms] et [!UICONTROL nom des concentrateurs d’événements].

Une fois vos informations d’authentification saisies, sélectionnez **[!UICONTROL Se connecter à la source]**.

![L’interface d’authentification SAS pour Azure Event Hubs.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Authentification Azure Active Directory Event Hub]

Pour créer un compte [!DNL Event Hubs] avec l’authentification Azure Active Directory Event Hub, utilisez le menu déroulant [!UICONTROL Authentification du compte] puis sélectionnez **[!UICONTROL Azure Active Directory Event Hub]**. Indiquez ensuite les valeurs de vos [!UICONTROL ID client], [!UICONTROL ID client], [!UICONTROL Valeur secrète client] et [!UICONTROL Espace de noms].

![Authentification Azure Event Hub Active Directory](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Authentification Azure Active Directory étendue Event Hub]

Pour créer un compte [!DNL Event Hubs] avec l’authentification Azure Active Directory étendue Event Hub, utilisez le menu déroulant [!UICONTROL Authentification du compte] puis sélectionnez **[!UICONTROL Azure Active Directory étendue Event Hub]**. Indiquez ensuite les valeurs de vos [!UICONTROL ID client], [!UICONTROL ID client], [!UICONTROL Valeur secrète client], [!UICONTROL Espace de noms] et [!UICONTROL Nom du hub d’événements].

![Authentification Azure Activity Directory étendue Azure Event Hub](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Étapes suivantes

Ce tutoriel vous a permis de connecter votre compte [!DNL Event Hubs] à Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données de votre espace de stockage dans Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
