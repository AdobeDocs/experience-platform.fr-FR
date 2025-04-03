---
title: Créer une connexion Source Mixpanel dans l’interface utilisateur
description: Découvrez comment créer une connexion source Mixpanel à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 33%

---

# Créer une connexion source [!DNL Mixpanel] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL Mixpanel] à l’aide de l’interface utilisateur de Adobe Experience Platform Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

### Collecter les informations d’identification requises

Pour connecter [!DNL Mixpanel] à Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Nom d’utilisateur | Nom d’utilisateur du compte de service qui correspond à votre compte [!DNL Mixpanel]. Pour plus d’informations, consultez la [[!DNL Mixpanel] documentation sur les comptes de service](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account). | `Test8.6d4ee7.mp-service-account` |
| Mot de passe | Mot de passe du compte de service qui correspond à votre compte [!DNL Mixpanel]. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| ID de projet | Identifiant de projet [!DNL Mixpanel]. Cet identifiant est requis pour créer une connexion source. Pour plus d’informations](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) consultez la [[!DNL Mixpanel] documentation sur les paramètres de projet et le [[!DNL Mixpanel] guide sur la création et la gestion de projets](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects). | `2384945` |
| Fuseau horaire | Fuseau horaire qui correspond à votre projet [!DNL Mixpanel]. Le fuseau horaire est requis pour créer une connexion source. Pour plus d’informations, consultez la [documentation sur les paramètres du projet Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings). | `Pacific Standard Time` |

Pour plus d’informations sur l’authentification de votre source [!DNL Mixpanel], consultez la [[!DNL Mixpanel] présentation de la source](../../../../connectors/analytics/mixpanel.md).

## Connecter votre compte [!DNL Mixpanel]

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie *Analytics*, sélectionnez [!DNL Mixpanel], puis **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

La page **[!UICONTROL Connecter le compte Mixpanel]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte [!DNL Mixpanel] avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![new](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## Sélectionner l’ID et le fuseau horaire de votre projet {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Définir un fuseau horaire pour l&#39;ingestion de Mixpanel"
>abstract="Le fuseau horaire doit être identique à celui du profil Mixpanel, car Experience Platform utilise le fuseau horaire du projet désigné pour ingérer les données pertinentes à partir de Mixpanel. Mixpanel adaptera son fuseau horaire afin de le coordonner à celui de votre projet avant d&#39;enregistrer l&#39;événement dans un entrepôt de données Mixpanel."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=fr#project-id-and-timezone" text="En savoir plus dans la documentation."

Une fois votre source authentifiée, indiquez votre ID de projet et votre fuseau horaire, puis sélectionnez **[!UICONTROL Sélectionner]**.

Le fuseau horaire que vous désignez avant d’ingérer les données [!DNL Mixpanel] dans Experience Platform doit être identique au paramètre de fuseau horaire de votre profil de [!DNL Mixpanel]. Toute modification du fuseau horaire de vos données sera appliquée uniquement aux nouveaux événements et les anciens événements resteront dans le fuseau horaire que vous avez précédemment désigné. [!DNL Mixpanel] prend en charge l’heure d’été et adapte correctement l’horodatage de votre ingestion. Pour plus d’informations sur l’impact des fuseaux horaires sur vos données, consultez le guide [!DNL Mixpanel] sur la [gestion des fuseaux horaires pour les projets](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

Après quelques instants, l’interface de droite se met à jour vers un panneau de prévisualisation, ce qui vous permet d’examiner votre schéma avant de créer un flux de données. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![configuration](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Mixpanel]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données d’analyse dans Experience Platform](../../dataflow/analytics.md).

## Ressources supplémentaires {#additional-resources}

Les sections ci-dessous fournissent des ressources supplémentaires auxquelles vous pouvez vous référer lors de l’utilisation de la source [!DNL Mixpanel].

### Validation {#validation}

Vous trouverez ci-dessous un aperçu des étapes que vous pouvez suivre pour vérifier que vous avez réussi à connecter votre source [!DNL Mixpanel] et que [!DNL Mixpanel] événements sont ingérés dans Experience Platform.

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Jeux de données]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Jeux de données]. L’écran [!UICONTROL Activité du jeu de données] affiche les détails des exécutions.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

Sélectionnez ensuite l’identifiant d’exécution du flux de données du flux de données que vous souhaitez afficher pour afficher des détails spécifiques sur cette exécution.

![surveillance des flux de données](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

Enfin, sélectionnez **[!UICONTROL Prévisualiser le jeu de données]** pour afficher les données ingérées.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

Vous pouvez vérifier ces données par rapport aux données de la page [!DNL Mixpanel] > [!DNL Events] . Voir le [[!DNL Mixpanel] document sur les événements](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) pour plus d’informations.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Schéma Mixpanel

Le tableau ci-dessous répertorie les mappages pris en charge qui doivent être configurés pour [!DNL Mixpanel].

>[!TIP]
>
>Voir [API d’exportation d’événements > Télécharger](https://developer.mixpanel.com/reference/raw-event-export) pour plus d’informations sur l’API.


| Source | Type |
|---|---|
| `distinct_id` | chaîne |
| `event_name` | chaîne |
| `import` | booléen |
| `insert_id` | chaîne |
| `item_id` | chaîne |
| `item_name` | chaîne |
| `item_price` | chaîne |
| `mp_api_endpoint` | chaîne |
| `mp_api_timestamp_ms` | nombre entier |
| `mp_processing_time_ms` | Entier |
| `time` | Entier |

### Limites {#limits}

* Vous disposez d’un maximum de 100 requêtes simultanées et de 60 requêtes par heure, comme indiqué dans la section [Limites de taux d’API d’exportation](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
