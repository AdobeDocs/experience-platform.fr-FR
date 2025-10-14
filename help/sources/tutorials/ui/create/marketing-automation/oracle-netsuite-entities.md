---
title: Créer une connexion source  [!DNL Oracle NetSuite Entities]  dans l’interface utilisateur
description: Découvrez comment créer une connexion source Oracle NetSuite Entities à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: ce0ea37f-16e0-4aef-9809-72c0b11e0440
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 36%

---

# Créer une connexion source [!DNL Oracle NetSuite Entities] dans l’interface utilisateur

Lisez le tutoriel suivant pour savoir comment importer des données de contacts et de clients de votre compte [!DNL Oracle NetSuite Entities] à Adobe Experience Platform dans l’interface utilisateur.

## Prise en main {#getting-started}

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’un compte [!DNL Oracle NetSuite], vous pouvez ignorer le reste de ce document et passer au tutoriel expliquant comment [Configurer un flux de données](../../dataflow/marketing-automation.md).

>[!TIP]
>
>Lisez la [[!DNL Oracle NetSuite] présentation](../../../../connectors/marketing-automation/oracle-netsuite.md) pour plus d’informations sur la manière de récupérer vos informations d’authentification.

## Connecter votre compte [!DNL Oracle NetSuite Activities] {#connect-account}

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie *Automatisation du marketing*, sélectionnez **[!DNL Oracle NetSuite Entities]**, puis **[!UICONTROL Ajouter des données]**.

![Capture d’écran de l’interface utilisateur Experience Platform pour le catalogue avec la carte Oracle NetSuite Entities](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/catalog-card.png)

La page **[!UICONTROL Connecter le compte Oracle NetSuite Entities]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

>[!IMPORTANT]
>
>Le jeton d’actualisation expire au bout de sept jours. Une fois que votre jeton expire, vous devez créer un compte sur Experience Platform avec votre jeton mis à jour. Si vous ne créez pas de compte avec votre jeton mis à jour, le message d’erreur suivant risque de s’afficher : `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Compte existant {#existing-account}

Pour utiliser un compte existant, sélectionnez le compte [!DNL Oracle NetSuite Entities] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour connecter le compte Oracle NetSuite Entities à un compte existant](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/existing.png)

### Nouveau compte {#new-account}

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** puis attendez que la nouvelle connexion s’établisse.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour connecter le compte Oracle NetSuite Entities à un nouveau compte](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/new.png)

### Sélectionner les données

Sélectionnez ensuite le type d’objet à ingérer dans Experience Platform.

| Type d’entité | Description |
| --- | --- |
| Contact | Récupérez les noms de contacts, les e-mails, les numéros de téléphone et tout champ personnalisé associé aux contacts associé aux clients. |
| Client | Récupérez des données client spécifiques, y compris des détails tels que les noms, adresses et identifiants clés du client. |

>[!BEGINTABS]

>[!TAB  Contact ]

![Capture d’écran de l’interface utilisateur Experience Platform pour les entités Oracle Netsuite affichant la configuration avec l’option Contact sélectionnée](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-contact.png)

>[!TAB Client]

![Capture d’écran de l’interface utilisateur Experience Platform pour les entités Oracle Netsuite présentant la configuration avec l’option Client sélectionnée](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/select-data-customer.png)

>[!ENDTABS]

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Oracle NetSuite Entities]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données d’automatisation du marketing dans Experience Platform](../../dataflow/marketing-automation.md).

## Ressources supplémentaires {#additional-resources}

Les sections ci-dessous fournissent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la source [!DNL Oracle NetSuite Entities].

### Mappage {#mapping}

Experience Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [&#x200B; Guide de l’interface utilisateur de la préparation des données &#x200B;](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>Les champs affichés dépendent des abonnements auxquels votre compte [!DNL Oracle NetSuite] a accès. Par exemple, si vous n’avez pas accès à la facturation, les champs liés à la facturation ne s’affichent pas.

### Planification {#scheduling}

Lors de la planification de votre flux de données [!DNL Oracle NetSuite Entities] pour l’ingestion, vous devez sélectionner la configuration de fréquence et d’intervalle suivante :

| Fréquence | Intervalle |
| --- | --- |
| `Once` | 1 |

Lors de la récupération des données, le [!DNL Oracle NetSuite] répond avec la date de dernière modification ou création sous la forme d’un format de date au lieu d’un horodatage. Par conséquent, la planification est limitée à un jour.

Une fois que vous avez fourni les valeurs de votre planification, sélectionnez **[!UICONTROL Suivant]**.

![Étape de planification du workflow des sources.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-entities/scheduling.png)
