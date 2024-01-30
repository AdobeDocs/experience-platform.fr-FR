---
title: Création d’un flux de données pour les données de Braze dans l’interface utilisateur
description: Découvrez comment créer un flux de données pour votre compte Braze à l’aide de l’interface utilisateur de Adobe Experience Platform.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Version Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 23%

---

# Créer une connexion source [!DNL Braze] dans l’interface utilisateur

>[!NOTE]
>
>La source [!DNL Braze] est en version Beta. Veuillez lire la [présentation des sources](../../../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL Braze] alimente en temps réel les interactions centrées sur les clients entre les consommateurs et les marques. [!DNL Braze Currents] est un flux de données en temps réel d’événements d’engagement de la plateforme Braze, qui constitue l’exportation la plus robuste mais la plus granulaire de la [!DNL Braze] plateforme.

Lisez le tutoriel suivant pour savoir comment importer des données d’événements d’engagement de votre [!DNL Braze] compte vers Adobe Experience Platform dans l’interface utilisateur.

## Conditions préalables

Pour suivre les étapes de ce guide, vous aurez besoin des éléments suivants :

* Une connexion à [Adobe Experience Platform](https://platform.adobe.com) et l’autorisation de créer une nouvelle connexion source en continu.
* Une connexion à [[!DNL Braze] tableau de bord](https://dashboard.braze.com/sign_in), une valeur inutilisée [Licence currents Connector](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)et les autorisations pour créer un connecteur. Pour plus d’informations, consultez la section [conditions requises pour configurer [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : le cadre normalisé en fonction duquel [!DNL Experience Platform] organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

Ce tutoriel nécessite également une compréhension pratique de [[!DNL Braze] Courants](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Si vous disposez déjà d’une [!DNL Braze] vous pouvez ignorer le reste de ce document et passer au tutoriel sur [configuration d’un flux de données](../../dataflow/marketing-automation.md).

## Connectez-vous à [!DNL Braze] compte à Experience Platform

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , *Automatisation du marketing* catégorie, sélectionnez **[!UICONTROL Braze]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources sur l’interface utilisateur Experience Platform avec la source Courants de braze sélectionnée.](../../../../images/tutorials/create/braze/catalog.png)

Ensuite, chargez le [Exemple de fichier Courants de braquage](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Ce fichier contient tous les champs que Braze peut envoyer dans le cadre d’un événement.

![L’écran &quot;Ajouter des données&quot;.](../../../../images/tutorials/create/braze/select-data.png)

Une fois votre fichier chargé, vous devez fournir les détails de votre flux de données, y compris des informations sur votre jeu de données et le schéma vers lequel vous mappez.
![L’écran &quot;Détails du flux de données&quot; surlignant &quot;Détails du jeu de données&quot;.](../../../../images/tutorials/create/braze/dataflow-detail.png)

Ensuite, configurez le mappage pour vos données à l’aide de l’interface de mappage.

![L’écran &quot;Mappage&quot;.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>Les horodatages de Braze ne sont pas exprimés en millisecondes, mais en secondes. Pour que les horodatages dans Experience Platform soient reflétés avec précision, vous devez créer des champs calculés en millisecondes. Un calcul de &quot;time * 1000&quot; sera correctement converti en millisecondes, approprié pour le mappage à un champ d’horodatage dans Experience Platform.
>
>![Création d’un champ calculé pour l’horodatage ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Collecter les informations d’identification requises

Une fois votre connexion créée, vous devez collecter les valeurs d’informations d’identification suivantes, que vous fournissez ensuite dans le tableau de bord Braser pour envoyer des données à [!DNL Platform]. Pour plus d’informations, consultez la section [!DNL Braze] [guide sur la navigation vers les courants](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Champ | Description |
| ---------- | ----------- |
| `Client ID` | L’ID client associé à votre [!DNL Platform] source. |
| `Client Secret` | Le secret client associé à votre [!DNL Platform] source. |
| `Tenant ID` | L’identifiant du client associé à votre [!DNL Platform] source. |
| `Sandbox Name` | L’environnement de test associé à votre [!DNL Platform] source. |
| `Dataflow ID` | L’identifiant de flux de données associé à votre [!DNL Platform] source. |
| `Streaming Endpoint` | Le point de terminaison de diffusion en continu associé à votre [!DNL Platform] source. Notez que Braze convertira automatiquement cette information vers le point de terminaison de la diffusion par lots. |

### Configurer [!DNL Braze Currents] pour diffuser des données vers votre source de données

Dans le [!DNL Braze Dashboard], accédez à Intégrations des partenaires . **->** Exportation de données, puis sélectionnez **[!DNL Create New Current]**. Vous serez invité à attribuer un nom au connecteur, à contacter les notifications concernant le connecteur et aux informations d’identification répertoriées ci-dessus. Sélectionnez les événements que vous souhaitez recevoir, configurez éventuellement les exclusions/transformations de champ souhaitées, puis sélectionnez **[!DNL Launch Current]**.

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte [!DNL Braze]. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données du système d’automatisation du marketing dans [!DNL Platform]](../../dataflow/marketing-automation.md).