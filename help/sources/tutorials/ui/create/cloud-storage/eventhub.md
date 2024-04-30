---
title: Créer une connexion source Azure Event Hubs dans l’interface utilisateur
description: Découvrez comment créer une connexion source Azure Event Hubs à l’aide de l’interface utilisateur de Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: e4ea21af3f0d9e810959330488dc06bc559cf72c
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 17%

---

# Créez un [!DNL Azure Event Hubs] connexion source dans l’interface utilisateur

>[!IMPORTANT]
>
>La variable [!DNL Azure Event Hubs] source est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Ce tutoriel décrit les étapes à suivre pour créer une [!DNL Azure Event Hubs] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion [!DNL Event Hubs] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/streaming/cloud-storage-streaming.md).

### Collecter les informations d’identification requises

Pour authentifier votre [!DNL Event Hubs] connecteur source, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB Authentification standard]

| Informations d’identification | Description |
| --- | --- |
| Nom de la clé SAS | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| Clé SAS | La clé primaire de la variable [!DNL Event Hubs] espace de noms. La variable `sasPolicy` que la variable `sasKey` correspond à doit avoir `manage` les droits configurés pour [!DNL Event Hubs] liste à renseigner. |
| Espace de noms | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

>[!TAB Authentification SAS]

| Informations d’identification | Description |
| --- | --- |
| Nom de la clé SAS | Nom de la règle d’autorisation, également connu sous le nom de clé SAS. |
| Clé SAS | La clé primaire de la variable [!DNL Event Hubs] espace de noms. La variable `sasPolicy` que la variable `sasKey` correspond à doit avoir `manage` les droits configurés pour [!DNL Event Hubs] liste à renseigner. |
| Espace de noms | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| Nom de la plateforme d’événements | Le nom de votre [!DNL Event Hubs] source. |

Pour plus d’informations sur l’authentification SAS (Shared Access Signatures) pour [!DNL Event Hubs], lisez le [[!DNL Azure] guide sur l&#39;utilisation de SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

>[!TAB Event Hub Azure Active Directory Auth]

| Informations d’identification | Description |
| --- | --- |
| Identifiant du client | Identifiant du tenant auprès duquel vous souhaitez demander une autorisation. Votre ID de tenant peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque**: l’identifiant du client est appelé &quot;ID d’annuaire&quot; dans la variable [!DNL Microsoft Azure] . |
| Identifiant client | ID d’application affecté à votre application. Vous pouvez récupérer cet ID à partir de la variable [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Valeur secrète du client | Le secret client utilisé avec l’ID client pour authentifier votre application. Vous pouvez récupérer votre secret client à partir de la fonction [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Espace de noms | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |

Pour plus d’informations sur [!DNL Azure Active Directory], lisez le [Guide Azure sur l’utilisation de Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Event Hub Portée par Azure Active Directory Auth]

| Informations d’identification | Description |
| --- | --- |
| Identifiant du client | Identifiant du tenant auprès duquel vous souhaitez demander une autorisation. Votre ID de tenant peut être formaté sous la forme d’un GUID ou d’un nom convivial. **Remarque**: l’identifiant du client est appelé &quot;ID d’annuaire&quot; dans la variable [!DNL Microsoft Azure] . |
| Identifiant client | ID d’application affecté à votre application. Vous pouvez récupérer cet ID à partir de la variable [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Valeur secrète du client | Le secret client utilisé avec l’ID client pour authentifier votre application. Vous pouvez récupérer votre secret client à partir de la fonction [!DNL Microsoft Entra ID] le portail sur lequel vous avez enregistré votre [!DNL Azure Active Directory]. |
| Espace de noms | L’espace de noms de la variable [!DNL Event Hubs] vous y accédez. Un [!DNL Event Hubs] L’espace de noms fournit un conteneur d’étendue unique, dans lequel vous pouvez créer un ou plusieurs [!DNL Event Hubs]. |
| Nom de la plateforme d’événements | Le nom de votre [!DNL Event Hubs] source. |

Pour plus d’informations sur [!DNL Azure Active Directory], lisez le [Guide Azure sur l’utilisation de Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour lier votre [!DNL Event Hubs] compte à Experience Platform.

## Connecter votre compte [!DNL Event Hubs]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. La variable [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , [!UICONTROL Stockage dans le cloud] catégorie, sélectionnez **[!UICONTROL Centre d’événements Azure]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources avec les centres d’événements Azure sélectionnés.](../../../../images/tutorials/create/eventhub/catalog.png)

La variable **[!UICONTROL Connexion aux centres d’événements Azure]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable [!DNL Event Hubs] compte que vous souhaitez utiliser, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Liste des comptes sources Azure Event Hubs existants.](../../../../images/tutorials/create/eventhub/existing.png)

### Nouveau compte

>[!TIP]
>
>Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;un [!DNL Event Hubs] connexion de base. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouvelle [!DNL Event Hubs] compte .

![Nouvelle interface de création de compte pour les centres d’événements Azure.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Authentification standard]

Pour créer une [!DNL Event Hubs] compte avec authentification standard, utilisez la méthode [!UICONTROL Authentification du compte] menu déroulant, puis sélectionnez **[!UICONTROL Authentification standard]**. Ensuite, indiquez les valeurs de votre [!UICONTROL Nom de la clé SAS], [!UICONTROL Clé SAS], et [!UICONTROL Espace de noms].

Une fois que vous avez saisi vos informations d’authentification, sélectionnez **[!UICONTROL Connexion à la source]**.

![Interface d’authentification standard pour les centres d’événements Azure.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB Authentification SAS]

Pour créer une [!DNL Event Hubs] compte avec authentification SAS, utilisez [!UICONTROL Authentification du compte] menu déroulant, puis sélectionnez **[!UICONTROL Authentification SAS]**. Ensuite, indiquez les valeurs de votre [!UICONTROL Nom de la clé SAS], [!UICONTROL Clé SAS], [!UICONTROL Espace de noms], et [!UICONTROL Nom des centres d’événements].

Une fois que vous avez saisi vos informations d’authentification, sélectionnez **[!UICONTROL Connexion à la source]**.

![Interface d’authentification SAS pour les centres d’événements Azure.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Event Hub Azure Active Directory Auth]

Pour créer une [!DNL Event Hubs] Compte avec authentification Event Hub Azure Active Directory, utilisez [!UICONTROL Authentification du compte] menu déroulant, puis sélectionnez **[!UICONTROL Centre d’événements Azure Active Directory]**. Ensuite, indiquez les valeurs de votre [!UICONTROL Identifiant du client], [!UICONTROL ID client], [!UICONTROL Valeur secrète du client], et [!UICONTROL Espace de noms].

![Authentification Azure Event Hub Azure Active Directory](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Event Hub Portée par Azure Active Directory Auth]

Pour créer une [!DNL Event Hubs] Compte avec authentification Azure Active Directory étendue à Event Hub, utilisez [!UICONTROL Authentification du compte] menu déroulant, puis sélectionnez **[!UICONTROL Centre D’Événements Porté Sur Azure Active Directory]**. Ensuite, indiquez les valeurs de votre [!UICONTROL Identifiant du client], [!UICONTROL ID client], [!UICONTROL Valeur secrète du client], [!UICONTROL Espace de noms], et [!UICONTROL Nom du noeud d’événement].

![Authentification Azure Event Hub Portée Par Azure Activity Directory](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Étapes suivantes

En suivant ce tutoriel, vous avez connecté votre [!DNL Event Hubs] compte à Experience Platform. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer dans Experience Platform les données provenant de votre espace de stockage dans le cloud](../../dataflow/streaming/cloud-storage-streaming.md).
